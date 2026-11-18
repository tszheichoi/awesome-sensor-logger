# Orientation
On Android, the system provides up to three different orientation estimates. 

The default **Orientation** sensor on Sensor Logger utilizes the accelerometer, magnetometer, and gyroscope. The gyroscope is the primary orientation input, with compensation from the accelerometer and magnetometer. See [Units Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md) and the [Coordinates Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md) for more details. 

Additionally, you can enable the following in Settings > Sensor Configuration > Additional Orientation Data. You will, in addition to the default orientation measurements get:

- **Game Orientation**, which relies on the accelerometer and gyroscope (without a magnetometer). It reports continuously and lacks heading accuracy information. Because it does not use the magnetometer, the yaw reference axis does not point north and instead starts from an arbitrary heading, allowing for slow yaw drift around the Z-axis while keeping pitch and roll referenced to gravity.
- **Geomagnetic Orientation** uses the accelerometer and magnetometer, omitting the gyroscope. Operating in a low-power mode, it reports continuously and provides heading accuracy information. 
