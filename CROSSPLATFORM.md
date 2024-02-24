# Cross-Platform Differences
Sensor Logger is a cross-platform app available on both iOS and Android. Whilst the user experience of the application is largely the same, some units and reference frame definitions are different. 

- [Cross-Platform Differences](#cross-platform-differences)
  * [Coordinate Differences](#coordinate-differences)
    + [Acceleration](#acceleration)
    + [Gravity](#gravity)
    + [Orientation](#orientation)
    + [Rotation Rate](#rotation-rate)
  * [Unit Differences](#unit-differences)
  * [Other Differences](#other-differences)
  * [Notice Anything Else](#notice-anything-else)

> 💡: **New in Version 1.29**: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ will mostly eliminate the differences listed below. This is _turned off_ by default to maintain backwards compatibility. But if you are building a new analysis pipeline, it is suggested that you toggle this on, especially if you are using the Studies feature with participants across platforms. Toggling this setting makes iOS values conform to Android conventions. Adjusting this setting on Android has no effect. For the plots and demonstrations below, data was taken from the three pictured phones.

![IMG_0012](https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/4d590cdc-0167-4135-978d-a466afc9b30f)

## Coordinate Differences
### Acceleration
By default, iOS and Android differ by a negative sign in all three `x`, `y` and `z` axes. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md#differences-between-ios-and-android) for a diagram. The same applies to the uncalibrated acceleration. If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android definition, as it is a right-handed-coordinate system. 

<img width="1392" alt="acceleration" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/9bbfc15b-d91a-463d-aa27-5f3a94607029">

### Gravity
By default, iOS and Android differ by a negative sign. When you place your phone flat on a table, the gravity vector points in `-z` on iOS and `+z` on Android. If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android definition. Note that the test data was taken with the phone's screen face downwards to prevent accidental input, so gravity points in the opposite direction. Regardless, the key takeaway is the alignment in axes definitions across platforms once standardisation is turned on.

<img width="1388" alt="gravity" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/8b532a91-b79d-4d5a-80ad-9ea96b9204c9">

### Orientation
On iOS, `yaw` is zero when the `x` points to true north, whereas on Android, it is the magnetic north. Understand the [differences between the two](https://www.rmg.co.uk/stories/topics/true-north-magnetic-north-whats-difference), and consider whether this matters to your analysis.
On iOS, `yaw` increases when you turn counterclockwise around the `z` axis. On Android, `yaw` increases when you turn clockwise around the `z` axis. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md#differences-between-ios-and-android-1) for a diagram.
On iOS, pitch decreases as you rotate around the `x` axis clockwise. On Android, pitch decreases as you rotate around the `x` axis counterclockwise. 

If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android directions. However, the difference between true and magnetic north remains unaccounted for. You can observe this in the plot below, where the standardised iOS `yaw` and Android `yaw` are offset by an amount. 

<img width="1387" alt="orientation" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/d19898b4-7959-4746-8793-04ac610134a4">

### Rotation Rate
iOS and Android report with the same sign convention for the rotation rate from the Gyroscope sensor. Toggling **Standardise Units & Frames** has no effects here. 

<img width="1391" alt="rotation_rate" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/8987be74-a4db-4efc-a43b-f2f599d8a8bf">

## Unit Differences
Only for _uncalibrated_ acceleration:
- On iOS, this is in standard gravity (g).
- On Android, this is in meters per second squared (ms-2)

Note that the calibrated version (default) of acceleration is unaffected, and is (ms-2) on both platforms. Please also see the comprehensive [Units Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md). If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android definition of ms-2, in addition to applying the aforementioned sign convention change (See the Acceleration section). 

<img width="1385" alt="uncalibrated_acceleration" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/99988cd0-91aa-42d3-97f3-877e873a5777">

## Other Differences
There are other considerations between iOS and Android, depending on your application and analysis:
- Sampling frequency;
- Sensor accuracy and precision;
- Platform-level data processing and fusion pipelines for calibrated or derived values, such as orientation.

Toggling "Standardise Units & Frames" will not account for these potential differences. 

## Notice Anything Else
If you notice any other differences between operating systems when using Sensor Logger, please reach out or raise an issue in this repository. 
