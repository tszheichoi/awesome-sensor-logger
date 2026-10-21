# Sandbox

Sandbox turns Sensor Logger into a live sensor source over WebRTC (PeerJS). Sandbox is intended to power lightweight, interactive visualisation. A Sandbox session creates no recording on the phone, so data the host doesn't keep is gone. For longer collection, consider using the app's streaming features, such as HTTP and MQTT, instead.

Sample ready-made mini games and experiments can be found at https://sensorlogger.app/sandbox. 

## Protocol

- **Available:** accelerometer, gyroscope, orientation, magnetometer and barometer at up to about 100 Hz; vibration; a name shown on the phone. Several phones can join one session.
- **Not currently available:** location, microphone, camera, other sensors.

### Connecting

1. The host creates a PeerJS peer on the **default PeerJS cloud server** and shows a QR code of `sensorlogger://sandbox/<peerId>`.
2. On the phone, go to About > Sandbox > Scan QR Code. Opening the link with the phone's camera app also works.
3. The phone connects to the host. Nothing streams until the host sends `start`.
4. Data flows while the Sandbox screen stays open. Leaving it or tapping Disconnect ends the session.

### Commands (Host to Phone)

| Message                                                   | Effect                                                                       |
| --------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `{"type":"start","sensors":["accelerometer",...]}`        | Streams these sensors, replacing the previous set. Unknown names are dropped |
| `{"type":"stop"}`                                         | Stops streaming. The connection stays open                                   |
| `{"type":"vibrate","strength":"small"\|"medium"\|"hard"}` | Haptic tap                                                                   |
| `{"type":"setName","playerName":"Alice"}`                 | Name shown on the phone                                                      |
| `{"type":"ping"}`                                         | Phone replies `{"type":"pong"}`                                              |

The phone silently ignores anything else, so confirm a command took effect from the data.

### Samples (Phone to Host)

`{"timestamp": 1792414496698, "sensor": "accelerometer", "values": {"x": 0.12, "y": -0.03, "z": 0.41}}`

`timestamp` is milliseconds since the Unix epoch on the phone's clock. iOS and Android send the same keys on the same standardised axes: https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md

| Sensor          | Fields                       | Units and notes                                                             |
| --------------- | ---------------------------- | --------------------------------------------------------------------------- |
| `accelerometer` | `x y z`                      | m/s², gravity removed (about 0 at rest)                                     |
| `gyroscope`     | `x y z`                      | rad/s                                                                       |
| `magnetometer`  | `x y z`                      | µT, calibrated                                                              |
| `orientation`   | `qw qx qy qz roll pitch yaw` | Quaternion; angles in radians                                               |
| `barometer`     | `pressure relativeAltitude`  | hPa; metres since the Sandbox screen opened. Updates far slower than 100 Hz |

### Good to Know

- The phone only connects through the public PeerJS cloud server (`0.peerjs.com`), so a custom PeerServer won't work.
- Samples can arrive out of order; sort by `timestamp`. Timestamps come from each phone's own clock.
- Sampling rates depend on the hardware.
- If the connection drops, the phone reconnects once. The reconnect arrives as a new connection with nothing streaming, so send `start` again.
- Restarting the host means a new peer ID, so every phone must scan again. To change sensors, send `start` instead.
- Assume the stream stops if the phone is backgrounded or locked, and the Sandbox screen doesn't prevent auto-lock.
- Whoever hosts the QR the user scans receives the data.

## Browser Example

For a page the user looks at, such as a game or a live plot. Opening it as a local file in Chrome works. Keep these two imports as they are: `qrcode` has no browser build, so it comes from jsDelivr's `+esm`, and the PeerJS script exposes `peerjs.Peer`.

```html
<canvas id="qr"></canvas>
<script src="https://cdn.jsdelivr.net/npm/peerjs@1.5.5/dist/peerjs.min.js"></script>
<script type="module">
  import QRCode from "https://cdn.jsdelivr.net/npm/qrcode@1.5.4/+esm";
  const peer = new peerjs.Peer();
  peer.on("open", (id) =>
    QRCode.toCanvas(
      document.getElementById("qr"),
      `sensorlogger://sandbox/${id}`,
    ),
  );
  peer.on("connection", (conn) => {
    conn.on("open", () =>
      conn.send({ type: "start", sensors: ["accelerometer", "orientation"] }),
    );
    conn.on("data", (msg) => {
      if (msg.sensor) console.log(msg);
    });
  });
</script>
```

## Node Example

If you are setting this up for, for example, an AI agent, this is a more suitable way to get started. Requires Node 22 or newer.

```bash
mkdir sandbox && cd sandbox && npm init -y && npm i peerjs@1.5.5 node-datachannel qrcode
# save sandbox-host.mjs (below), then:
node sandbox-host.mjs accelerometer,gyroscope > stream.jsonl 2> host.log &
until [ -s host.log ]; do sleep 1; done
open sandbox-qr.png   # show the QR to the user (xdg-open on Linux)
until [ -s stream.jsonl ]; do sleep 1; done   # first sample from a phone
tail -n 5 stream.jsonl
```

The host saves `sandbox-qr.png`, prints the link to stderr, names each phone `p1`, `p2`, ... (shown on the phone) and starts the sensors given on the command line as it connects. A reconnecting phone gets a new name. Every message from the phones, including `pong` replies, goes to stdout as a JSON line with a `phone` field added. `POST 127.0.0.1:8765/send[?phone=p1]` passes a command on and replies with the phones it sent it to. Bad JSON gets a 400.

```js
// node sandbox-host.mjs accelerometer,gyroscope > stream.jsonl 2> host.log
import http from "node:http";
import * as webrtc from "node-datachannel/polyfill";
import QRCode from "qrcode";

Object.assign(globalThis, webrtc);
// PeerJS checks for WebRTC on load, so import it after the polyfill
const { Peer } = (await import("peerjs")).default;
const ALLOWED = "accelerometer,gyroscope,orientation,magnetometer,barometer";
const SENSORS = process.argv[2].split(",");
if (!SENSORS.every((s) => ALLOWED.split(",").includes(s)))
  throw new Error(`sensors: ${ALLOWED}`);
const phones = {}; // "p1" -> connection
let count = 0;

const peer = new Peer();
peer.on("open", async (id) => {
  const link = `sensorlogger://sandbox/${id}`;
  await QRCode.toFile("sandbox-qr.png", link);
  console.error(link);
});
peer.on("error", console.error);
peer.on("connection", (conn) => {
  const phone = `p${++count}`;
  conn.on("open", () => {
    phones[phone] = conn;
    conn.send({ type: "setName", playerName: phone });
    conn.send({ type: "start", sensors: SENSORS });
  });
  conn.on("data", (msg) => console.log(JSON.stringify({ phone, ...msg })));
  conn.on("close", () => delete phones[phone]);
});

// POST /send[?phone=p1] with a command as the body
http
  .createServer(async (req, res) => {
    const url = new URL(req.url, "http://localhost");
    if (url.pathname !== "/send") return res.writeHead(404).end();
    try {
      let body = "";
      for await (const chunk of req) body += chunk;
      const msg = JSON.parse(body);
      const target = url.searchParams.get("phone");
      const sent = Object.keys(phones).filter((p) => !target || p === target);
      sent.forEach((p) => phones[p].send(msg));
      res.end(JSON.stringify({ sent }));
    } catch (e) {
      res.writeHead(400).end(e.message);
    }
  })
  .listen(8765, "127.0.0.1");
```

If you can't open an image, print a text QR and put it in a code block.

```bash
node -e 'require("qrcode").toString(process.argv[1], { type: "utf8" }).then(console.log)' "$(head -1 host.log)"
```

### Reading Data

Expect about 100 lines per second per sensor per phone. Don't read `stream.jsonl` whole.

| Need             | Use                                                                                                                                                                                            |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Latest samples   | `tail -n 50 stream.jsonl`. A phone that stopped leaves its last lines at the end, so compare `timestamp` with the current time                                                                 |
| Summaries        | Pipe `tail -n 1000 stream.jsonl` into a short script                                                                                                                                           |
| Events           | A filter on `tail -n 0 -f stream.jsonl` that prints only matches. Run it in the background and wait on its output. Make it print each line straight away (`grep --line-buffered`, `python -u`) |
| Offline analysis | Load `stream.jsonl` after the session                                                                                                                                                          |
| Commands         | `curl -s "localhost:8765/send?phone=p1" -d '{"type":"vibrate","strength":"hard"}'`. Omit `phone` to send to every phone. Send `start` the same way to change sensors                           |
