# Data Pushing
Sensor Logger supports HTTP Push and MQTT publishing during a recording session. This can be enabled by tapping the gear icon on the Logger page. All supported sensors during a recording will be streamed in JSON, once every configurable batch period, to the specified web server / broker via the specified protocol.

Both HTTP Push and MQTT have the same schema, configurable batching period and supported sensors. The only difference is the protocol. HTTP has a simpler setup and is more widely supported. On the other hand, MQTT is more lightweight and popular for IoT applications. Sensor Logger also supports simultaneous HTTP pushing and MQTT publishing. 

## HTTP Push
For HTTP Push, you have to set up a web server to receive the messages. For more information and sample code on how to set one up, see https://github.com/tszheichoi/awesome-sensor-logger?tab=readme-ov-file#live-data-streaming.

## MQTT Publishing
MQTT (Message Queuing Telemetry Transport) is a lightweight messaging protocol that is widely used for IoT (Internet of Things) applications. It is more lightweight than HTTP, but requires a more involved setup. 

### Setting Up a Broker
You can either run your own broker (e.g. Mosquitto, EMQ X, HiveMQ, RabbitMQ, and VerneMQ), or use a managed and hosted one. For this example, we will use HiveMQ Cloud, which is free to use and does not require you to install anything on your computer. 

1. Visit https://www.hivemq.com/company/get-hivemq/ and then select HiveMQ Cloud. You will need to create a free account.
2. Select the free Serverless option.
3. Select AWS as the provider. A cluster will then be provisioned for you.
4. Navigate to Access Management at the top.
5. Create a username and password under the Credentials section. 

Copy the Broker URL, Username and Password as shown below. Make sure Use TLS is toggled on. You can change the topic name as you wish. The default is `sensor-logger`. 

<img width="1452" alt="Screenshot 2024-03-09 at 17 10 25" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/8d657c37-e4ed-4e08-8255-48727da7a931">

### Testing the Connection
To test the connection, navigate to the Web Client at the top on HiveMQ. Connect to the client via the same username and password you have just created. Then, enter the topic you have configured on Sensor Logger. It is `sensor-logger` by default. On Sensor Logger, tap "Tap to Test Publish". If successful, it should say "Message Sent". On the web client, you should see an incoming test message.  

<img width="1544" alt="Screenshot 2024-03-09 at 17 24 38" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/7d77c471-e2bc-468a-8e82-46e1d0b90276">

It is also via this web client that you can see incoming messages during a recording session when MQTT Publishing is enabled.

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
- Sensor Logger only supports websockets. Typically websockets are on port 8000 (no TLS) or 8884 (TLS). TCP connections are not supported, which are typically on port 1883 (no TLS) or 8883 (TLS).

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

