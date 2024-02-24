# One-Page Coordinates Reference

This page is a comprehensive documentation of the coordinate systems used by Sensor Logger. Should you notice any error, please report by making an Issue or making a pull request directly. Additional information about sensors and measurements is available in-app by tapping the "eye" icon next to each sensor.

For information about units, refer to https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md

## Acceleration on Phones

Acceleration is reported in the following coordinate system, with `x` and `y` being the horizontal and vertical axes of the screen and `z` pointing into/out of the screen. These axes "stick" to the device, so they never change even when the phone rotates.

<img width="966" alt="Screenshot 2024-02-24 at 00 57 04" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/ec93559b-5443-48a1-85e0-7c05fde6b723">

_Adapted from https://developer.apple.com/documentation/coremotion/cmheadphonemotionmanager to reflect the sign convention differences between operating systems._ 

### Differences Between iOS and Android
While the directions of the axes are the same across platforms, **there is a negative sign difference for all three axes** between iOS and Android. For example, if you move your phone to the right, along the `x` axis, you will register positive acceleration on Android, but negative acceleration on iOS. This is simply a difference in definition -- likely because iOS' convention is in the context of _inertial force_, whereas Android's convention is in the context of _accelerating force_. 

Accordingly, the Gravity sensor is also different by a negative sign between iOS and Android. When you place your phone flat on a table, the gravity vector points in `-z` on iOS and `+z` on Android. 

## Acceleration on Apple Watch & AirPods
Acceleration data from the Apple Watch follows the same convention as the iPhone. Simply replace the screen of the phone with the screen of the phone in the diagram below. 
 
The acceleration values from the Headphone motion sensor follow the following convention. 

<img src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/bf2600df-d624-4cb3-acd2-44ef633628f5" width="200"/>

_Source: https://developer.apple.com/documentation/coremotion/cmheadphonemotionmanager_

Note: The Gravity sensor in Sensor Logger has the same coordinate system as the Accelerometer linear acceleration measurements. 

## Gyroscope & Orientation

The rotation rates and orientation are measured around the axes, as the acceleration. Again, following the right-hand convention. When you read off the Gyroscope sensor in Sensor Logger, refer to the diagram below.

<img src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/ac11f346-2c49-40f1-a5e0-4c711ab978f3" width="200"/>

_Source: https://developer.apple.com/documentation/coremotion/getting_raw_gyroscope_events_

The orientation is derived from the rotation rate and references the same axes, but are called:

- `roll` refers to the rotation around `y`;
- `pitch` refers to the rotation around `x`;
- `yaw` refers to the rotation around `z`. Sometimes also called the `azimuth`. 

Additionally, orientation has an arbitrary offset, as it is an integrated value from the rotation rate (i.e. an integration constant). For this, Sensor Logger uses the `x-north-z-vertical` reference frame, meaning the `yaw` value is 0 when the `x` axis is aligned with the north (i.e. the angle between the device's `y` axis and the north). 

### Differences Between iOS and Android
Due to legacy reasons and backwards compatibility reasons, there are some key differences in interpreting the yaw value:

- On iOS, north means the _true north_, whereas on Android, it refers to the _magnetic north_. You may have to account for this difference if you are comparing absolute values measured across platforms, though factors such as the accuracy of the magnetometer may outweigh such differences. 
- On iOS, `yaw` increases when you turn counter-clockwise around the `z` axis (as pictured above). On Android, `yaw` increases when you turn clockwise around the `z` axis (opposite to pictured above, i.e. east is +π/2 and west is -π/2).

Further, on Android, there are additional Orientations you can log with various trade-offs. See https://github.com/tszheichoi/awesome-sensor-logger/blob/main/ORIENTATION.md. 

