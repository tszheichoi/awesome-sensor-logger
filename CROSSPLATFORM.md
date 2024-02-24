# Cross-Platform Differences
Sensor Logger is a cross-platform app available on both iOS and Android. Whilst the user experience of the application is largely the same, some units and reference frame definitions are different. 

> 💡: **New in Version 1.29**: Toggle "Standardise Units & Frames" in Sensor Configuration under Settings will mostly eliminate the differences listed below. This is _turned off_ by default to maintain backwards compatibility. But if you are building a new analysis pipeline off Sensor Logger, it is suggested that you toggle this on, especially if you are using the Studies feature with participants across platforms.  

## Coordinate Differences
### Acceleration
iOS and Android differ by a negative sign in all three `x`, `y` and `z` axes. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md#differences-between-ios-and-android) for a diagram. 

If "Standardise Units & Frames" is toggled on, Sensor Logger will conform to the Android definition as it is a right-handed-coordinate system. 

### Gravity
iOS and Android differ by a negative sign. When you place your phone flat on a table, the gravity vector points in `-z` on iOS and `+z` on Android.

If "Standardise Units & Frames" is toggled on, Sensor Logger will conform to the Android definition.


### Orientation
On iOS, `yaw` is zero when the `x` points to true north, whereas on Android, it is the magnetic north. Understand the [differences between the two](https://www.rmg.co.uk/stories/topics/true-north-magnetic-north-whats-difference), and consider whether this matters to your analysis.
On iOS, `yaw` increases when you turn counterclockwise around the `z` axis. On Android, `yaw` increases when you turn clockwise around the `z` axis. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md#differences-between-ios-and-android-1) for a diagram.
On iOS, pitch decreases as you rotate around the `x` axis clockwise. On Android, pitch decreases as you rotate around the `x` axis counterclockwise. 

If "Standardise Units & Frames" is toggled on, Sensor Logger will conform to the Android definition. However, the difference between true and magnetic north remains unaccounted for. 

## Unit Differences
Only for _uncalibrated_ acceleration:
- On iOS, this is in standard gravity (g).
- On Android, this is in meters per second squared (ms-2)

Note that the calibrated version (default) of acceleration is unaffected, and is (ms-2) on both platforms. Please also reference the comprehensive [Units Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md). 

If "Standardise Units & Frames" is toggled on, Sensor Logger will conform to the Android definition of ms-2. 

## Other Differences
There are other considerations between iOS and Android, depending on your application and analysis:
- Sampling frequency;
- Sensor accuracy and precision;
- Platform-level data processing and fusion pipelines for calibrated or derived values, such as orientation.

Toggling "Standardise Units & Frames" will not account for any of these potential differences. 

## Notice Anything Else?
If you notice any other differences between operating systems when using Sensor Logger, please reach out or raise an issue in this repository. 
