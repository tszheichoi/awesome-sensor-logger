# One-Page Coordinates Reference

This page is a comprehensive documentation of the coordinate systems used by Sensor Logger. Should you notice any error, please report by making an Issue or making a pull request directly. Additional information about sensors and measurements is available in-app by tapping the "eye" icon next to each sensor.

For information about units, refer to https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md

## Acceleration on Phones

Acceleration is reported in the following coordinate system, with `x` and `y` being the horizontal and vertical axes of the screen and `z` pointing into/out of the screen. These axes "stick" to the device, so they never change even when the phone rotates.

### Differences Between iOS and Android

This is what the coordinate frames look like by operating systems. 

<img width="966" alt="Screenshot 2024-02-24 at 00 57 04" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/ec93559b-5443-48a1-85e0-7c05fde6b723">

_IMPORTANT: These diagrams show the direction of the applied force. This is different to the diagrams on Apple's official documentation, which shows the inertial force (exact opposite). https://developer.apple.com/documentation/coremotion/cmheadphonemotionmanager._ 

While the directions of the axes are the same across platforms, **there is a negative sign difference for all three axes** between iOS and Android. For example, if you move your phone to the right, along the `x` axis, you will register positive values on Android, but negative values on iOS. This is simply a difference in definition -- likely because iOS' convention is in the context of _inertial force_, whereas Android's convention is in the context of _accelerating force_. 

Accordingly, the Gravity sensor is also different by a negative sign between iOS and Android. When you place your phone flat on a table, the gravity vector points in `-z` on iOS and `+z` on Android. 

> 💡: **New in Version 1.29**: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ will eliminate this difference by automatically converting values logged on iOS to the Android convention. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/CROSSPLATFORM.md) for more information. 

## Acceleration on Apple Watch & AirPods
Acceleration data from the Apple Watch follows the same convention as the iPhone. The acceleration values from the Headphone motion sensor follow the following convention. 

<img src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/bf2600df-d624-4cb3-acd2-44ef633628f5" width="200"/>

_Source: https://developer.apple.com/documentation/coremotion/cmheadphonemotionmanager_

This photo below roughly aligns the coordinates for all three Apple devices. The coordinate system across the three pictured devices is always the same and consistent. As such, it is safe to compare and perform data fusion amongst measurements from these devices. However, they collectively are inconsistent with Android's coordinate system, as noted in the previous section. Toggling "Standardise Units & Frames" under _Settings > Sensor Configuration_ will convert _all measurements from Apple Watch and AirPods_ to Android's convention. Also note that the [units](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md) of acceleration vary across iPhone, Apple Watch and AirPods if "Standardise Units & Frames" is not toggled on. 

<img width="977" alt="Screenshot 2024-03-07 at 00 39 40" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/ce79333d-75f5-4b83-a8fd-3c87c15222dd">

This plot compares the units and coordinate system of acceleration data from all three Apple devices with "Standardise Units & Frames" toggled on (Note: "Standardise Units & Frames" is off by default). 

<img width="1109" alt="Screenshot 2024-03-07 at 00 34 38" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/1cd383f6-4227-4fd8-8fcd-c54288476214">

## Gyroscope

The rotation rates and orientation are measured around the same axes as acceleration. When you read off the Gyroscope sensor in Sensor Logger, refer to the diagram below.

<img src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/ac11f346-2c49-40f1-a5e0-4c711ab978f3" width="200"/>

_Source: https://developer.apple.com/documentation/coremotion/getting_raw_gyroscope_events_

For the rotation rate readings from the Gyroscope sensor, iOS and Android have consistent definitions. 

## Orientation
The orientation is derived from the rotation rate and references the same axes. To be specific:
- `roll` refers to the rotation around `y`;
- `pitch` refers to the rotation around `x`;
- `yaw` refers to the rotation around `z`. Sometimes also called the `azimuth`.

Orientation is reported using a Tait‑Bryan Z‑X′‑Y″ (yaw → pitch → roll) intrinsic rotation sequence, meaning the device is first rotated around the z axis (yaw), then the rotated x axis (pitch), and finally the twice-rotated y axis (roll). 

Additionally, orientation has an arbitrary offset, as it is an integrated value from the rotation rate (i.e. an integration constant). For this, Sensor Logger uses the `x-north-z-vertical` reference frame, meaning the `yaw` value is 0 when the `x` axis is aligned with the north (i.e. the angle between the device's `y` axis and the north). 

### Differences Between iOS and Android
Due to legacy reasons and backwards compatibility reasons, there are some key differences in interpreting the yaw value:

1. On iOS, north means the _true north_, whereas on Android, it refers to the _magnetic north_. You may have to account for this difference if you are comparing absolute values measured across platforms, though factors such as the accuracy of the magnetometer may outweigh such differences. 
2. On iOS, `yaw` increases when you turn counterclockwise around the `z` axis (as pictured above, positive rotation around positive `z` following the right-handed system). On Android, `yaw` increases when you turn clockwise around the `z` axis (opposite to pictured above, negative rotation around positive `z` following the right-handed system; i.e. east is +π/2 and west is -π/2).
3. On iOS, `pitch` decreases as you rotate around the `x` axis clockwise (negative rotation around positive `x` following the right-handed system). On Android, `pitch` decreases as you rotate around the `x` axis counterclockwise (i.e. tiling the phone's top edge towards you and the phone's bottom edge away from you when you hold your phone normally, positive rotation around positive `x` following the right-handed system)

Further, on Android, there are additional Orientations you can log with various trade-offs. See https://github.com/tszheichoi/awesome-sensor-logger/blob/main/ORIENTATION.md. 

> 💡: **New in Version 1.29**: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ will eliminate 2 and 3 by automatically converting values logged on iOS to the Android convention. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/CROSSPLATFORM.md) for more information. 
