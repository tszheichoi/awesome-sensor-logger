# One-Page Unit Reference

This page is a comprehensive documentation of the units of values reported in the Sensor Logger app. Much effort has been spent to ensure correctness and consistency across iOS and Android. Should you notice any error, please report by making an Issue or make a pull request directly. Additional information about sensors and measurements is available in-app by tapping the "eye" icon next to each sensor.

For full documentation, please visit [https://www.tszheichoi.com/sensorloggerhelp](https://www.tszheichoi.com/sensorloggerhelp)

## Time
- `time` is in nanoseconds since epoch. For more information about conversion, use tools like https://www.epochconverter.com/. 
- `seconds_elapsed` is in seconds since the start of the recording.

## Accelerometer
- `x`, `y` and `z` in meters per second squared (ms<sup>-2</sup>); Assumes `g` to be 9.80665ms<sup>-2</sup>.

See the [Coordinates Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md) for definitions of axes. 

## Accelerometer Uncalibrated
- `x`, `y` and `z`:
    - On iOS, this is in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g).
    - On Android, this is in meters per second squared (ms<sup>-2</sup>)

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

## Location
- `altitude`, in meters as a height above the WGS84 ellipsoid.
- `altitudeAboveMeanSeaLevel`, in meters above mean sea level (iOS Only). 
- `bearing`, in degrees from 0 to 360 relative to due north. Negative values indicate it is invalid. 
- `bearingAccuracy`, in degrees. Negative values indicate it is invalid. 
- `horizontalAcccuracy`, in meters as the radius of uncertainty. It is approximately the unit standard deviation around the `altitude`. Negative values indicate it is invalid.
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
- `pressure` is in mBar.

## Microphone
- `dBFS` is [decibels relative to full scale](https://en.wikipedia.org/wiki/DBFS) and is dimensionless.

## Network
- `type` can be one of none, unknown, cellular, wifi, Bluetooth, ethernet, wimax, vpn or other. 
- `isConnected` is a boolean or null.
- `isInternetReachable` is boolean or null.
- `isWifiEnabled` is boolean (Android only).
- `isConnectionExpensive` is boolean.
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
- `text` is the text string entred by the user. 

## Battery
- `batteryLevel` is between 0 and 1, representing the fractional charge level.
- `batteryState` is an enum that can be one of unplugged, charging or full.
- `lowerPowerMode` is a boolean.

## Headphone
- `pitch`, `roll` and `yaw`, in radians.
- `accelerationX`, `accelerationY` and `accelerationZ` in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g).
- `gravityX`, `gravityY` and `gravityZ`, in meters per second squared (ms<sup>-2</sup>); Assumes `g` to be 9.80665ms<sup>-2</sup>.
- `quaternionW`, `quaternionX`, `quaternionY` and `quaternionZ`, dimensionless. 
- `devicelocation` can be left or right.  

## Heartrate
- `bpm` in beats per minute.

## WristMotion
- `rotationX`, `rotationY` and `rotationZ`, in radians per second (rad/s).
- `gravityX`, `gravityY` and `gravityZ`, in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g).
- `accelerationX`, `accelerationY` and `accelerationZ` in [standard gravity](https://en.wikipedia.org/wiki/Standard_gravity) (g).
- `quaternionW`, `quaternionX`, `quaternionY` and `quaternionZ`, dimensionless. 

## Light
- `lux` is in lux.

## WiFi
- `ssid` is the name of the WiFI network.
- `bssid` is the MAC address.
- `frequency` is the network frequency.
- `level` is the signal strength in dBm.
 
