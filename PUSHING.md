# Data Pushing
Sensor Logger supports HTTP Push and MQTT Publishing during a recording session. This can be enabled by tapping the gear icon on the Logger page. All supported sensors during a recording will be streamed in JSON, once every configurable batch period, to the specified web server / broker via the specified protocol.

Both HTTP Push and MQTT have the same schema, configurable batching period and supported sensors. The only difference is the protocol. HTTP has a simpler setup and is more widely supported. On the other hand, MQTT is more lightweight and popular for IoT applications. Sensor Logger also supports _simultaneous_ HTTP pushing and MQTT publishing. 

If you want to push to other protocols currently not supported by Sensor Logger, many managed MQTT brokers support out-of-the-box data forwarding to pretty much anything. For example, [EMQ X Cloud Data Integration](https://www.emqx.io/docs/en/latest/data-integration/data-bridges.html) supports message forwarding to Kafka, and GCP PubSub Sources.

## HTTP Push

<img width="667" alt="Screenshot 2023-10-25 at 15 09 43" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/19e800bb-3efd-40ae-b25b-22c92da1e071">

HTTP Push sends a POST request to the supplied URL with content-type "application/json". The request body is of the following format:
```
{
    messageId: 0,
    sessionId: "identifier",
    deviceId: "identifier",
    userId: "identifier",
    payload: [
        {
            "name": "accelerometer",
            "time": 1698501144401773000,
            <other fields depending on sensor>
        },
        {
            "name": "location",
            "time": 1698501145514000000,
            <other fields depending on sensor>
        },
    ],
}
```
- `messageId` is incremented for each message sent. The `messageId` is useful because the messages can be received out-of-order, which may need to be handled depending on your use case.
- `sessionId` is the same for all messages in a single recording.
- `deviceId` is the same for all messages from a single device.
- `userId` only exists if there is an active Study. This matches the `userId` that the investigator can use to reference against recordings and questionnaires. This is new in version 1.57. 

The time is always in UTC epoch nanoseconds.

Note: due to legacy reasons, on Android only, some sensors report accuracy alongside `name` and `time`. This is left in-place for backwards compatibility. Interpreting this field:
- 0 means unreliable
- 1 means low accuracy
- 2 means medium accuracy
- 3 means maximum accuracy

### Setting Up Server
There are many ways to setup a server that can accept messages pushed from Sensor Logger -- from off-the-shelf solutions to running the server yourself. Here are some pointers to get you started. It is recommended (but not required) for servers to respond with HTTP code 200. If the server responds with HTTP code 499 and the body contains text, then this message will be shown to the user (once per recording).

#### RequestBin
To simply consume and explore the data, you may want to use something like https://requestbin.com/. To plot the data in real-time, you may need something more custom. See https://github.com/mhaberler/sensorlogger-telegraf for a solution using telegraf. 

#### Timeplus
Also checkout Timeplus, a real-time streaming analytics platform: https://www.youtube.com/watch?v=iWA8FHjyatE. They also offer a dockerised solution. See https://github.com/timeplus-io/proton/tree/develop/examples/awesome-sensor-logger

![image](https://user-images.githubusercontent.com/30114997/224557365-dfe593f5-e84f-4fcf-9900-9bcfd31c5e44.png)

#### Javascript Webserver
Thanks to [Harshad Joshi](https://github.com/hj91), you can find a javascript implementation using nodejs for a webserver that is designed for Sensor Logger: https://github.com/hj91/json-server

#### Python Webserver
If you prefer sticking with Python, here is an implementation using Plotly Dash to get you started. Dash is powered by Flask under the hood, and provides an easy way to set up a web server for real-time, interactive data visualisation. This code listens on the `/data` endpoint, filters only the values from the accelerometer and plots it. The `update_graph()` callback is triggered every `UPDATE_FREQ_MS`, and updates the plot with any accumulated measurements so far. You will have to customise this script yourself if you want to plot measurements from other sensors. 

```
import dash
from dash.dependencies import Output, Input
from dash import dcc, html
from datetime import datetime
import json
import plotly.graph_objs as go
from collections import deque
from flask import Flask, request

server = Flask(__name__)
app = dash.Dash(__name__, server=server)

MAX_DATA_POINTS = 1000
UPDATE_FREQ_MS = 100

time = deque(maxlen=MAX_DATA_POINTS)
accel_x = deque(maxlen=MAX_DATA_POINTS)
accel_y = deque(maxlen=MAX_DATA_POINTS)
accel_z = deque(maxlen=MAX_DATA_POINTS)

app.layout = html.Div(
	[
		dcc.Markdown(
			children="""
			# Live Sensor Readings
			Streamed from Sensor Logger: tszheichoi.com/sensorlogger
		"""
		),
		dcc.Graph(id="live_graph"),
		dcc.Interval(id="counter", interval=UPDATE_FREQ_MS),
	]
)


@app.callback(Output("live_graph", "figure"), Input("counter", "n_intervals"))
def update_graph(_counter):
	data = [
		go.Scatter(x=list(time), y=list(d), name=name)
		for d, name in zip([accel_x, accel_y, accel_z], ["X", "Y", "Z"])
	]

	graph = {
		"data": data,
		"layout": go.Layout(
			{
				"xaxis": {"type": "date"},
				"yaxis": {"title": "Acceleration ms<sup>-2</sup>"},
			}
		),
	}
	if (
		len(time) > 0
	):  #  cannot adjust plot ranges until there is at least one data point
		graph["layout"]["xaxis"]["range"] = [min(time), max(time)]
		graph["layout"]["yaxis"]["range"] = [
			min(accel_x + accel_y + accel_z),
			max(accel_x + accel_y + accel_z),
		]

	return graph


@server.route("/data", methods=["POST"])
def data():  # listens to the data streamed from the sensor logger
	if str(request.method) == "POST":
		print(f'received data: {request.data}')
		data = json.loads(request.data)
		for d in data['payload']:
			if (
				d.get("name", None) == "accelerometer"
			):  #  modify to access different sensors
				ts = datetime.fromtimestamp(d["time"] / 1000000000)
				if len(time) == 0 or ts > time[-1]:
					time.append(ts)
					# modify the following based on which sensor is accessed, log the raw json for guidance
					accel_x.append(d["values"]["x"])
					accel_y.append(d["values"]["y"])
					accel_z.append(d["values"]["z"])
	return "success"


if __name__ == "__main__":
	app.run(port=8000, host="0.0.0.0")
```

Run this Python script and visit `http://localhost:8000/` on your computer. Then you have to enter the correct Push URL in Sensor Logger on your phone under the settings page. To find out the localhost of the device you are running the webserver on, you can, for example, do something like this in Python. 

```
import socket
hostname = socket.gethostname()
print(socket.gethostbyname(hostname))
```

For example, if it returns `192.168.1.168`, then you want to enter `http://192.168.1.168:8000/data` in Sensor Logger. Use the "Tap to Test Pushing" button to test whether Sensor Logger can properly reach the endpoint. If you get a 200 response, then you are good to go! Start a recording as usual, and you should begin to see data being streamed in:

<img width="1440" alt="Screenshot 2022-07-10 at 10 23 03" src="https://user-images.githubusercontent.com/30114997/178138947-8522be59-4c0b-4966-84ad-49416fda5fc0.png">

If "Tap to Test Pushing" fails, this usually indicates a networking issue between your phone and your computer. Check that both devices are on the same network (i.e. the same WiFi). Some WiFi networks, particularly corporate or university ones, may block cross-device connections. If you've entered the URL into your phone (e.g. http://192.168.x.xxx:8000/data) and it isn't working, it is most likely being blocked by the router. Note that if you're using the Python script as is, the URL must end with /data and must not include "localhost". If you're being blocked by the router, you can try using a tool like ngrok by installing it from here and running "ngrok http 8000", then entering the resulting URL (which usually ends in ngrok-free.app) into the Sensor Logger app as the HTTP push URL (e.g. https://xxx.ngrok-free.app/data).

## MQTT Publishing
MQTT (Message Queuing Telemetry Transport) is a lightweight messaging protocol that is widely used for IoT (Internet of Things) applications. It is more lightweight than HTTP, but requires a more involved setup. 

A simple web based demo app is available at https://github.com/tszheichoi/sensor-logger-streaming-demo-app. It connects to an MQTT broker, consumes streaming data, and visualizes it in an interactive plot. The demo also illustrates how to handle data from multiple devices simultaneously.

### Setting Up a Managed Broker
You can either run your own broker (e.g. Mosquitto, EMQX, HiveMQ, RabbitMQ, and VerneMQ), or use a managed and hosted one.

#### HiveMQ Cloud Example
For this example, we will use HiveMQ Cloud, which is free to use and does not require you to install anything on your computer. 

1. Visit https://www.hivemq.com/company/get-hivemq/ and then select HiveMQ Cloud. You will need to create a free account.
2. Select the free Serverless option.
3. Select AWS as the provider. A cluster will then be provisioned for you.
4. Navigate to Access Management at the top.
5. Create a username and password under the Credentials section. 

Copy the Broker URL, Username and Password as shown below. Make sure Use TLS is toggled on. You can change the topic name as you wish. The default is `sensor-logger`. 

<img width="1452" alt="Screenshot 2024-03-09 at 17 10 25" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/8d657c37-e4ed-4e08-8255-48727da7a931">

To test the connection, navigate to the Web Client at the top on HiveMQ. Connect to the client via the same username and password you have just created. Then, enter the topic you have configured on Sensor Logger. It is `sensor-logger` by default. On Sensor Logger, tap "Tap to Test Publish". If successful, it should say "Message Sent". On the web client, you should see an incoming test message.  

<img width="1544" alt="Screenshot 2024-03-09 at 17 24 38" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/7d77c471-e2bc-468a-8e82-46e1d0b90276">

It is also via this web client that you can see incoming messages during a recording session when MQTT Publishing is enabled.

#### EMQX Cloud Example
EMQX Cloud works very similarly to HiveMQ Cloud, and also provides a generous free tier for you to try things out. 

1. Sign up for a new account at https://www.emqx.com/en/cloud.
2. Choose and deploy the Serverless plan.
3. Select the newly created cluster in the Deployments.
4. Create a username and password under the Credentials section. 

Copy the Broker URL, Username and Password as shown below. Make sure Use TLS is toggled on. You can change the topic name as you wish. The default is `sensor-logger`. 
<img width="866" alt="Screenshot 2024-03-28 at 16 47 24" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/a88ac1da-0fa5-4a0e-ab27-bdbcea0c7328">

To test the connection, navigate to the Online Test section in the sidebar and enter the Topic the same as that configured in Sensor Logger. Then click Subscribe. On Sensor Logger, tap "Tap to Test Publish". If successful, it should say "Message Sent". On the web client, you should see an incoming test message.  

### Setting Up a Local Broker
You can also run EMQX locally if you do not want to use one of the managed cloud services. In this case, unless you expose your IP address, Sensor Logger should be on the same local network as your machine. 

#### EMQX Locally Using Docker
1. Install docker on your machine https://docs.docker.com/engine/install/
2. Get the docker image for EMQX following [these instructions](https://www.emqx.io/downloads). Specifically, run `docker pull emqx/emqx:5.6.0`.
3. Start the container `docker run -d --name emqx -p 1883:1883 -p 8083:8083 -p 8084:8084 -p 8883:8883 -p 18083:18083 emqx/emqx:5.6.0`.
4. Navigate to `http://localhost:18083/` on a browser. The default username and password are `admin` and `public`, which you can change.
5. Select Authentication from the sidebar and then click `+ Create`. Follow the workflow to create a Password-Based authentication. For most options, such as the backend and encryption mechanism, the defaults are fine.
6. Select Websocket Client in the sidebar. There, you should find the host and port number you should enter into Sensor Logger.
7. On that same page, you can connect and subscribe to the `sensor-logger` topic for testing. 

### Publishing to the Broker
Once you have setup your broker, you can toggle "Enable MQTT Publish" on and start a recording session as usual. The JSON schema for the published MQTT messages is the same as the HTTP Push ones, namely: 

```
{
    messageId: 0,
    sessionId: "identifier",
    deviceId: "identifier",
    payload: [
        {
            "name": "accelerometer",
            "time": 1698501144401773000,
            <other fields depending on sensor>
        },
        {
            "name": "location",
            "time": 1698501145514000000,
            <other fields depending on sensor>
        },
    ],
}
```
The `messageId` is incremented for each message sent. The `sessionId` is the same for all messages in a single recording, and the `deviceId` is the same for all messages from a single device. The time is in UTC epoch nanoseconds.

Further, note the following:
- Sensor Logger publishes with a quality of service level 0 (at most once).
- Sensor Logger supports both websockets and TCP. Typically websockets are on port 8000 (no TLS) or 8884 (TLS). Typically TCP connections are on port 1883 (no TLS) or 8883 (TLS).

### Real-Time Visualization
A simple web based demo app is available at https://github.com/tszheichoi/sensor-logger-streaming-demo-app. It connects to an MQTT broker, consumes streaming data, and visualizes it in an interactive plot. The demo also illustrates how to handle data from multiple devices simultaneously.

### Consuming From the Broker
Once your measurements have reached the broker, it is up to you how to use those messages. Typically, you would set up another client to consume these messages. As an example, you can do this via Python. 
```
pip install paho-mqtt
```
Then you can adapt the following Python script for your use cases. 
```
import paho.mqtt.client as mqtt

BROKER_URL = "your_broker.com"
BROKER_PORT = 8884
USERNAME = "your_username"
PASSWORD = "your_password"

def on_connect(*args):
    print(f"Connected with result code {args[3]}")
    client.subscribe("sensor-logger")

def on_message(client, userdata, msg):
    print(f"msg: {msg.topic} {msg.payload}")

client = mqtt.Client(mqtt.CallbackAPIVersion.VERSION2, transport="websockets")
client.username_pw_set(username=USERNAME, password=PASSWORD)
client.on_connect = on_connect
client.on_message = on_message
client.tls_set(tls_version=mqtt.ssl.PROTOCOL_TLSv1_2)
client.connect(BROKER_URL, BROKER_PORT, 60)
client.loop_forever()
```
See the HTTP Push documentation for an example of how to plot the sensor data live using Plotly Dash. 

## Typescript Payload Schema

Regardless of whether you are using MQTT or HTTP Push, you can use the following Typescript definitions.  

```js
type Message = {
  messageId: number;
  sessionId: string;
  deviceId: string;
  userId: string;
  payload: SensorReading[];
};

type SensorReading =
  | MicrophoneReading
  | LocationReading
  | XYZReading
  | OrientationReading
  | BarometerReading
  | BrightnessReading
  | NetworkReading
  | BatteryReading
  | BluetoothReading
  | BluetoothMetadataReading
  | WristMotionReading
  | PedometerReading
  | HeadphoneReading
  | AnnotationReading;

type MicrophoneReading = {
  name: "microphone";
  time: number;
  values: {
    dBFS: number;
  };
};

type LocationReading = {
  name: "location";
  time: number;
  values: {
    altitude: number;
    speedAccuracy: number;
    bearingAccuracy: number;
    latitude: number;
    altitudeAboveMeanSeaLevel: number;
    bearing: number;
    horizontalAccuracy: number;
    verticalAccuracy: number;
    longitude: number;
    speed: number;
  };
};

type XYZReading = {
  name:
    | "magnetometeruncalibrated"
    | "gyroscopeuncalibrated"
    | "accelerometeruncalibrated"
    | "magnetometer"
    | "gyroscope"
    | "accelerometer"
    | "gravity"
    | "magnetometer";
  time: number;
  values: {
    z: number;
    y: number;
    x: number;
  };
  accuracy?: number;
};

type OrientationReading = {
  name: "orientation";
  time: number;
  values: {
    yaw: number;
    qx: number;
    qz: number;
    roll: number;
    qw: number;
    qy: number;
    pitch: number;
  };
};
type BarometerReading = {
  name: "barometer";
  time: number;
  values: {
    relativeAltitude: number;
    pressure: number;
  };
};
type BrightnessReading = {
  name: "brightness";
  time: number;
  values: {
    brightness: number;
  };
};

type NetworkReading = {
  name: "network";
  time: number;
  values: {
    type?: string;
    isConnected?: boolean;
    isInternetReachable?: boolean;
    isWifiEnabled?: boolean;
    isConnectionExpensive?: boolean;
    ssid?: string;
    bssid?: string;
    strength?: number;
    ipAddress?: string;
    frequency?: number;
    cellularGeneration?: string;
    carrier?: string;
  };
};

type BatteryReading = {
  name: "battery";
  time: number;
  values: {
    batteryLevel: number;
    batteryState: "unknown" | "unplugged" | "charging" | "full";
    lowPowerMode: boolean;
  };
};

type BluetoothReading = {
  name: "bluetooth";
  time: number;
  values: {
    id: string;
    rssi: number | null;
    txPowerLevel?: number;
    manufacturerData?: string;
  };
};

type BluetoothMetadataReading = {
  name: "bluetoothmetadata";
  time: number;
  values: {
    id: string;
    name: string;
    isConnectable: number;
    localName?: string;
    serviceUUIDs?: string;
  };
};

type WristMotionReading = {
  name: "wrist motion";
  time: number;
  values: {
    rotationRateX: number;
    rotationRateY: number;
    rotationRateZ: number;
    gravityX: number;
    gravityY: number;
    gravityZ: number;
    accelerationX: number;
    accelerationY: number;
    accelerationZ: number;
    quaternionW: number;
    quaternionX: number;
    quaternionY: number;
    quaternionZ: number;
  };
};

type PedometerReading = {
  name: "pedometer";
  time: number;
  values: {
    steps: number;
  };
};
type HeadphoneReading = {
  name: "headphone";
  time: number;
  values: {
    devicelocation: "left" | "right";
    roll: number;
    yaw: number;
    pitch: number;
    rotationRateX: number;
    rotationRateY: number;
    rotationRateZ: number;
    quaternionW: number;
    quaternionX: number;
    quaternionY: number;
    quaternionZ: number;
    gravityX: number;
    gravityY: number;
    gravityZ: number;
    accelerationX: number;
    accelerationY: number;
    accelerationZ: number;
  };
};

type AnnotationReading = {
  name: "annotation";
  time: number;
  values: {
    text: string;
    millisecond_press_duration: number;
  };
};
```
