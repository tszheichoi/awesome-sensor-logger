# Cross-Platform Differences & Standardisation
Sensor Logger is a cross-platform app available on both iOS (iPhone, Apple Watch & AirPods) and Android. Whilst the user experience of the application is largely the same, some units and reference frame definitions are different. 

- [Cross-Platform Differences](#cross-platform-differences)
  * [Coordinate Differences](#coordinate-differences)
    + [Acceleration](#acceleration)
    + [Gravity](#gravity)
    + [Orientation](#orientation)
    + [Rotation Rate](#rotation-rate)
  * [Unit Differences](#unit-differences)
  * [Other Differences](#other-differences)
  * [Notice Anything Else?](#notice-anything-else)

> 💡: **New in Version 1.63**: Standardisation is now applied properly and consistently for the Apple Watch and AirPods, covering both units and coordinate frame conventions, including recordings started from the watch itself. The watch inherits the standardisation state from the phone and displays it directly on the watch app.

> The watch tables below distinguish three recording modes. *Stream*: rows sent live to the phone during a phone-initiated recording, written by the phone. *Transfer*: files recorded on the watch during a phone-initiated recording and transferred afterwards. *Watch Only*: recordings started from the watch itself. For *Transfer* and *Watch Only*, "Standardisation On" means the phone's setting as last synced to the watch. A watch that has never connected since the setting was enabled keeps recording unstandardised values, matching pre-1.63 behaviour.

> 💡: **New in Version 1.55**: Introducing **Sensor Zoo**, which provides transparent, cross-platform sensor fusion algorithms: orientation filters (Complementary, Madgwick, Mahony, EKF), step counters, and a tilt-compensated compass. Every algorithm is fully inspectable, benchmarked against public datasets, and produces consistent results across iOS and Android. No proprietary APIs. No surprises. See https://github.com/tszheichoi/sensor-zoo. 

> 💡: **New in Version 1.29**: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ will mostly eliminate the differences listed below. This is _turned off_ by default to maintain backwards compatibility. But if you are building a new analysis pipeline, it is suggested that you toggle this on, especially if you are using the Studies feature with participants across platforms. Toggling this setting makes iOS (iPhone, Apple Watch & AirPods) values conform to Android conventions. Adjusting this setting on Android has no effect. For the plots and demonstrations below, data was taken from the three pictured phones.

![IMG_0012](https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/4d590cdc-0167-4135-978d-a466afc9b30f)

## Coordinate Differences
### Acceleration
By default, iOS (iPhone, Apple Watch & AirPods) and Android differ by a negative sign in all three `x`, `y` and `z` axes. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md#differences-between-ios-and-android) for a diagram. The same applies to the uncalibrated acceleration. If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android definition, as it is a right-handed-coordinate system. 

<img width="1392" alt="acceleration" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/9bbfc15b-d91a-463d-aa27-5f3a94607029">

### Gravity
By default, iOS (iPhone, Apple Watch & AirPods) and Android differ by a negative sign. When you place your phone flat on a table, the gravity vector points in `-z` on iOS and `+z` on Android. If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android definition. Note that the test data was taken with the phone's screen face downwards to prevent accidental input, so gravity points in the opposite direction. Regardless, the key takeaway is the alignment in axes definitions across platforms once standardisation is turned on.

<img width="1388" alt="gravity" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/8b532a91-b79d-4d5a-80ad-9ea96b9204c9">

### Orientation
On iOS, `yaw` is zero when the `x` points to true north, whereas on Android, it is the magnetic north. Understand the [differences between the two](https://www.rmg.co.uk/stories/topics/true-north-magnetic-north-whats-difference), and consider whether this matters to your analysis.
On iOS, `yaw` increases when you turn counterclockwise around the `z` axis. On Android, `yaw` increases when you turn clockwise around the `z` axis. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md#differences-between-ios-and-android-1) for a diagram.
On iOS, pitch decreases as you rotate around the `x` axis clockwise. On Android, pitch decreases as you rotate around the `x` axis counterclockwise. 

If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android directions. However, the difference between true and magnetic north remains unaccounted for. You can observe this in the plot below, where the standardised iOS `yaw` and Android `yaw` are offset by an amount. 

<img width="1387" alt="orientation" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/d19898b4-7959-4746-8793-04ac610134a4">

> 💡: **In Version 1.51**: Prior to this version, toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ only affected the euler angles. Since this version, the quaternions are also consistently flipped on iOS.

> 💡: **In Version 1.63**: Orientation standardisation now covers the Apple Watch and AirPods consistently. Euler angles are also now included when wrist motion is streamed to the phone, matching the other watch recording modes.

| With Standardisation On | Before 1.63 | After 1.63 |
| --- | --- | --- |
| Phone (Euler) | Standardised | Standardised |
| Phone (Quaternion) | Standardised | Standardised |
| Watch (Euler, Stream) | Column does not exist | Now exists and standardised |
| Watch (Quaternion, Stream) | Not standardised | Standardised |
| Watch (Euler, Transfer) | Not standardised | Standardised |
| Watch (Quaternion, Transfer) | Not standardised | Standardised |
| Watch (Euler, Watch Only) | Not standardised | Standardised |
| Watch (Quaternion, Watch Only) | Not standardised | Standardised |
| Headphone (Euler) | Standardised | Standardised |
| Headphone (Quaternion) | Not standardised | Standardised |

### Rotation Rate
iOS and Android report with the same sign convention for the rotation rate from the Gyroscope sensor. Toggling **Standardise Units & Frames** has no effect here. 

<img width="1391" alt="rotation_rate" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/8987be74-a4db-4efc-a43b-f2f599d8a8bf">

## Unit Differences
### For Phones
Only for _uncalibrated_ acceleration:
- On iOS, this is in standard gravity (g).
- On Android, this is in meters per second squared (ms-2)

Note that the calibrated version (default) of acceleration is unaffected, and is (ms-2) on both platforms. Please also see the comprehensive [Units Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md). If **Standardise Units & Frames** is toggled on, Sensor Logger will conform to the Android definition of ms-2, in addition to applying the aforementioned sign convention change (See the Acceleration section). 

<img width="1385" alt="uncalibrated_acceleration" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/99988cd0-91aa-42d3-97f3-877e873a5777">

### For Watches & Headphones
The unit for acceleration from the Apple Watch and AirPods is in standard gravity (g). And the gravity vector from the Apple Watch is in standard gravity (g). However, when **Standardise Units & Frames** is toggled on, all units will be consistent with the phone. Namely:
- Acceleration and gravity vector values from Apple Watch will be in meters per second squared (ms-2).
- Acceleration and gravity vector values from AirPods will be in meters per second squared (ms-2).
- Pressure values from the Apple Watch barometer will be in millibars (mbar), matching the phone.

It is strongly recommended that you toggle **Standardise Units & Frames** on -- by default, it is off for backwards compatibility reasons. 

> 💡: **In Version 1.63**: Unit standardisation now applies consistently across all watch recording modes.

Acceleration units, with **Standardise Units & Frames** on:

| With Standardisation On | Before 1.63 | After 1.63 |
| --- | --- | --- |
| Watch (Accelerometer, Stream) | ms-2 | ms-2 |
| Watch (Accelerometer, Transfer) | g | ms-2 |
| Watch (Accelerometer, Watch Only) | g | ms-2 |
| Watch (Uncalibrated Accelerometer, Stream) | Unavailable | Unavailable |
| Watch (Uncalibrated Accelerometer, Transfer) | g | ms-2 |
| Watch (Uncalibrated Accelerometer, Watch Only) | g | ms-2 |
| Headphone (Accelerometer) | ms-2 | ms-2 |
| Headphone (Uncalibrated Accelerometer) | Unavailable | Unavailable |

Gravity vector units, with **Standardise Units & Frames** on:

| With Standardisation On | Before 1.63 | After 1.63 |
| --- | --- | --- |
| Watch (Gravity, Stream) | ms-2 | ms-2 |
| Watch (Gravity, Transfer) | g | ms-2 |
| Watch (Gravity, Watch Only) | g | ms-2 |
| Headphone (Gravity) | ms-2 | ms-2 |

Pressure from the watch barometer is also affected. The phone reports pressure in millibars (mbar, equivalently hPa) on both iOS and Android, whereas the Apple Watch historically reported pressure in kilopascals (kPa) in all recording modes. Since Version 1.63, toggling **Standardise Units & Frames** on converts watch pressure to mbar to match the phone.

| With Standardisation On | Before 1.63 | After 1.63 |
| --- | --- | --- |
| Watch (Barometer, All Modes) | kPa | mbar / hPa |

Note that with standardisation *off*, watch barometer files remain in kPa even after 1.63, to avoid silently changing raw recordings. The watch's `Metadata.csv` records the `standardisation` flag, and it is reliable across all app versions: recordings from before 1.63 always carry `false` (and are indeed in kPa), so downstream tooling can use that flag alone to tell which unit a given `WatchBarometer.csv` is in.

## Other Differences
There are other considerations between iOS and Android, depending on your application and analysis:
- Sampling frequency;
- Sensor accuracy and precision;
- Platform-level data processing and fusion pipelines for calibrated or derived values, such as orientation. Note: As of 1.55, you can now enable Sensor Zoo to eliminate differences in algorithm pipeline by selecting one of the open source algorithms. See https://github.com/tszheichoi/sensor-zoo. 

Toggling **Standardise Units & Frames**  will not account for these potential differences. 

## Notice Anything Else?
If you notice any other differences between operating systems when using Sensor Logger, please reach out or raise an issue in this repository. 
