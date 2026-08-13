# One-Page Unit Reference

This page is a comprehensive documentation of the units of values reported in the Sensor Logger app. Much effort has been spent to ensure correctness and consistency across iOS and Android. Should you notice any error, please report by making an Issue or make a pull request directly. Additional information about sensors and measurements is available in-app by tapping the "eye" icon next to each sensor.

For full documentation, please visit [https://www.tszheichoi.com/sensorloggerhelp](https://www.tszheichoi.com/sensorloggerhelp)

## Time

- `time` is in nanoseconds since epoch. For more information about conversion, use tools like https://www.epochconverter.com/.
- `seconds_elapsed` is in seconds since the start of the recording.

## Accelerometer

- `x`, `y` and `z` in meters per second squared (ms<sup>-2</sup>); Assumes `g` to be 9.80665ms<sup>-2</sup>.

**Android Only**: On Android, due to varying device capabilities, there are two separate acceleration files:

- **Accelerometer.csv**: measures acceleration _without_ gravity (user-induced motion only). Note that some Android devices may not have the capability to isolate acceleration without gravity, and only TotalAcceleration is available.
- **TotalAcceleration.csv**: measures acceleration _with_ gravity included (raw accelerometer readings).

On iOS, only **Accelerometer.csv** is logged. You may create acceleration with gravity by combining the Accelerometer and Gravity sensor readings.

See the [Coordinates Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md) for definitions of axes.

## Accelerometer Uncalibrated

- `x`, `y` and `z`:
  - On iOS, this is in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g), when "Standardise Units & Frames" is off (default). The unit is ms<sup>-2</sup> when "Standardise Units & Frames" is on.
  - On Android, this is in meters per second squared (ms<sup>-2</sup>).

> 💡: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ removes all platform-dependent units and coordinate systems differences.

## Gravity

- `x`, `y` and `z`, in meters per second squared (ms<sup>-2</sup>); Assumes `g` to be 9.80665ms<sup>-2</sup>.

## Gyroscope

- `x`, `y` and `z`, in radians per second (rad/s).

## Gyroscope Uncalibrated

- `x`, `y` and `z`, in radians per second (rad/s).

## Orientation

- `pitch`, `roll` and `yaw`, in radians.
- `qx`, `qy`, `qz` and `qw`, dimensionless.

See the [Coordinates Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md) for definitions of axes. Note that the `yaw` definition is different between iOS and Android.

## Pedometer

- `steps` is an integer.

## Activity

- `activity` is a string, which can be one of walking, running, cycling, automotive, stationary, tilting or unknown.
- `confidence` is a string, which can be one of low, medium, high or unknown.

- Note that Android internally reports "on foot" and "walking", Sensor Logger maps these both to "walking".
- Note that the "tilting" activity is only reported on Android devices.

## Location

- `altitude`, in meters as a height above the WGS84 ellipsoid.
- `altitudeAboveMeanSeaLevel`, in meters above mean sea level (iOS Only).
- `bearing`, in degrees from 0 to 360 relative to due north. Negative values indicate it is invalid.
- `bearingAccuracy`, in degrees. Negative values indicate it is invalid.
- `horizontalAccuracy`, in meters as the radius of uncertainty. It is approximately the unit standard deviation around the reported position. Negative values indicate it is invalid.
- `verticalAccuracy`, in meters. It is approximately the unit standard deviation around the `altitude`. Negative values indicate it is invalid.
- `speed`, in meters per second. Negative values indicate it is invalid. Note this is derived from the location, so may be unreliable if the speed changes between location updates.
- `speedAccuracy`, in meters per second. Negative values indicate it is invalid.
- `latitude`, in degrees. Positive values are north of the equator (-90 to 90)
- `longitude`, in degrees. Positive values are east of the meridian line (-180 to 180).

## Magnetometer

- `x`, `y` and `z`, in micro teslas.

## Uncalibrated Magnetometer

- `x`, `y` and `z`, in micro teslas.

## Barometer

- `relativeAltitude` is in meters since the start of the recording.
- `pressure` is in millibars (mbar, equivalently hPa).

## Microphone

- `dBFS` is [decibels relative to full scale](https://en.wikipedia.org/wiki/DBFS) and is dimensionless.

For more information about the audio file, see https://github.com/tszheichoi/awesome-sensor-logger/blob/main/MICROPHONE.md

## Network

- `type` can be one of none, unknown, cellular, wifi, Bluetooth, ethernet, wimax, vpn or other.
- `isConnected` is a boolean or null.
- `isInternetReachable` is a boolean or null.
- `isWifiEnabled` is a boolean (Android only).
- `isConnectionExpensive` is a boolean.
- `ssid` is a string.
- `bssid` is a string.
- `strength` is a number between 0 and 100.
- `ipAddress` is the external IP address. Can be IPv4 or IPv6.
- `frequency` is the network frequency. For example, 2.4GHz will return 2457.
- `cellularGeneration` can be one of 2g, 3g, 4g, 5g or null.
- `carrier` is a string.

## Brightness

- `brightness` is between 0 and 1, representing the relative screen brightness.

## Annotation

- `millisecond_press_duration` is how long the pencil icon was tapped, in milliseconds.
- `text` is the text string entered by the user.

## Battery

- `batteryLevel` is between 0 and 1, representing the fractional charge level.
- `batteryState` is an enum that can be one of unknown, unplugged, charging or full.
- `lowPowerMode` is a boolean.
- `voltage` is the battery terminal voltage, in volts (V). (Android Only, _New in version 1.62_)
- `chargingCurrent` is the instantaneous battery current, in milliamps (mA). The sign is reported by the device and is manufacturer-dependent; on most devices a positive value means current flowing into the battery (charging) and a negative value means discharging. (Android Only, _New in version 1.62_)
- `health` is an enum that can be one of good, overheat, dead, over_voltage, unspecified_failure or cold. (Android Only, _New in version 1.62_)

## Battery Temp

- `temperature` is the battery temperature, in degrees celsius (°C). (Android Only)

## Headphone

- `pitch`, `roll` and `yaw`, in radians.
- `accelerationX`, `accelerationY` and `accelerationZ` in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g), when "Standardise Units & Frames" is off (default). The unit is ms<sup>-2</sup> when "Standardise Units & Frames" is on.
- `gravityX`, `gravityY` and `gravityZ`, in meters per second squared (ms<sup>-2</sup>); Assumes `g` to be 9.80665ms<sup>-2</sup>, regardless of whether "Standardise Units & Frames" is turned on or not.
- `quaternionW`, `quaternionX`, `quaternionY` and `quaternionZ`, dimensionless.
- `devicelocation` can be left or right.
- `rotationRateX`, `rotationRateY` and `rotationRateZ`, in radians per second (rad/s). (_Note: New in version 1.30_)

> 💡: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ removes all platform-dependent units and coordinate systems differences.

## Heartrate

- `bpm` in beats per minute.

## WristMotion

- `rotationRateX`, `rotationRateY` and `rotationRateZ`, in radians per second (rad/s).
- `gravityX`, `gravityY` and `gravityZ`, in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g), when "Standardise Units & Frames" is off (default). The unit is ms<sup>-2</sup> when "Standardise Units & Frames" is on.
- `accelerationX`, `accelerationY` and `accelerationZ` in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g), when "Standardise Units & Frames" is off (default). The unit is ms<sup>-2</sup> when "Standardise Units & Frames" is on.
- `quaternionW`, `quaternionX`, `quaternionY` and `quaternionZ`, dimensionless.
- `pitch`, `roll` and `yaw`, in radians. (New since version 1.44)

> 💡: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ removes all platform-dependent units and coordinate systems differences.

## WatchBarometer

- `relativeAltitude` is in meters since the start of the recording, the same as the phone.
- `pressure` is in kilopascals (kPa) when "Standardise Units & Frames" is off (default), unlike the phone which uses mbar. The unit is mbar when "Standardise Units & Frames" is on.

## WatchLocation

The same measurements as the phone's [Location](#location) sensor, in the same units, but three of the fields are named differently:

| On the watch | On the phone |
| --- | --- |
| `ellipsoidalAltitude` | `altitude` |
| `altitude` | `altitudeAboveMeanSeaLevel` |
| `course` and `courseAccuracy` | `bearing` and `bearingAccuracy` |

Note in particular that `altitude` is the height above mean sea level on the watch, but the height above the WGS84 ellipsoid on the phone. The two differ by the geoid separation, so do not combine them on that column name alone.

`latitude`, `longitude`, `speed`, `speedAccuracy`, `horizontalAccuracy` and `verticalAccuracy` are named and defined the same as on the phone.

## WatchMagnetometer

- `x`, `y` and `z`, in micro teslas — the same units as the phone's Magnetometer.

## WatchCompass

- `magneticBearing` is in degrees, the same as the phone's Compass.

## WatchMicrophone

- `dBFS` is [decibels relative to full scale](https://en.wikipedia.org/wiki/DBFS) and is dimensionless, the same as the phone's Microphone.

## Light

- `lux` is in lux.

## WiFi

- `ssid` is the name of the WiFi network.
- `bssid` is the MAC address.
- `frequency` is the network frequency.
- `level` is the signal strength in dBm.
- `capabilities` is a string listing the advertised capabilities of the network (e.g. supported authentication and encryption schemes).

## Compass

- `magneticBearing` is in degrees.

## Bluetooth

Each row is one received advertisement. Sensor Logger records advertisements raw, and may additionally interpret them where an existing decoder is available -- see the [sensor-ble](https://github.com/tszheichoi/sensor-ble) library for the supported devices. For decoding raw payloads yourself, see the [Recording Bluetooth LE sensors](https://github.com/tszheichoi/awesome-sensor-logger#recording-bluetooth-le-sensors) section of the README for worked examples.

- `id` is the device identifier (a MAC address on Android, a system-assigned UUID on iOS).
- `rssi` is the Received Signal Strength Indicator, in dBm. A larger negative value means a weaker signal. Can be null.
- `txPowerLevel` is the advertised transmit power, in dBm, where the device reports one.
- `manufacturerData` is the raw manufacturer data field, hex encoded.

If you record all nearby devices, the sensor is named `bluetooth`. If you select individual devices, each gets its own file named `bluetooth-<id>`.

## BluetoothMetadata

Written once per discovered device, alongside the advertisements above.

- `id` is the device identifier, matching the `id` in the Bluetooth records.
- `name` is the device name.
- `localName` is the local name from the advertisement, where present.
- `isConnectable` indicates whether the device accepts connections.
- `serviceUUIDs` is the list of advertised service UUIDs.
- `manufacturer` and `model` are the manufacturer and model strings, where the device reports them.

## Camera

The camera is the one sensor whose recorded form and streamed form differ, so treat them separately.

**In a recording**, the camera does not write a CSV. Frames are written into a `Camera/` directory inside the recording, and the filename carries the timestamp:

- In Images and Snapshot modes, one `<timestamp>.jpg` per frame.
- In Video mode, a single `<timestamp>.mp4` per recording segment.

Note that these filename timestamps are UNIX epoch **milliseconds**, not the nanoseconds used by the `time` column elsewhere. They are NTP-corrected if NTP synchronisation is enabled.

**When streaming** over HTTP Push or MQTT, there is no filesystem to write to, so each frame is sent inline as a reading named `camera`, with:

- `image`, the frame itself, base64 encoded.
- `imageFormat`, the encoding of that frame, `jpg`.

On iOS, depth maps are embedded within the captured images rather than stored separately. See https://github.com/tszheichoi/awesome-sensor-logger/blob/main/DEPTH.md for how to extract them.
