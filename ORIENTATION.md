# Orientation
On Android, the system provides up to three different orientation estimates. 

The default **Orientation** sensor on Sensor Logger utilizes the accelerometer, magnetometer, and gyroscope. The gyroscope is the primary orientation input, with compensation from the accelerometer and magnetometer. See [Unit Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md) for more details.

Additionally, you can enable the following in Settings > Sensor Configuration > Additional Orientation Data. You will, in addition to the default orientation measurements get:

- **Game Orientation**, which relies on the accelerometer and gyroscope (without a magnetometer). It reports continuously and lacks heading accuracy information. The Y-axis doesn't point north, allowing for drift similar to the gyroscope around the Z-axis. It aims to return the same vector for the same real-world orientation and is based solely on gyroscope data.
- **Geomagnetic Orientation** uses the accelerometer and magnetometer, omitting the gyroscope. Operating in a low-power mode, it reports continuously and provides heading accuracy information. 
