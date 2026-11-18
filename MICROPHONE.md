# Microphone

When the Microphone sensor is toggled, Sensor Logger writes up to two outputs depending on the **Microphone Quality** setting:

- Audio file (`.mp4`).
    - Recorded in **Lossy** (default) and **Lossless** modes.
    - Omitted when **Microphone Quality** is set to **Loudness** (loudness-only mode), which logs `Microphone.csv` without creating an `.mp4` file.
- Loudness in dBFS in `Microphone.csv`.
    - Always recorded when the Microphone sensor is enabled, and its sampling frequency cannot be changed.

## Audio Quality Configuration

You can adjust the audio quality level in Sensor Logger under _Settings > Sensor Configuration > Microphone Quality_ (**Lossy**, **Lossless**, or **Loudness**). In the latest version, the audio recording modes "Lossy" and "Lossless" carry the following configurations. 

|  | Lossy on iOS | Lossy on Android | Lossless on iOS | Lossless on Android |
| --- | --- | --- | --- | --- |
| Extension | .mp4 | .mp4 | .mp4 | .mp4 |
| Sample Rate | 16000 | 16000 | 48000 | 48000 |
| Channels | 1 | 1 | 2 | 2 |
| Bit Rate | 32000 | 32000 | N/A | 128000* |

_* Not actually lossless due to API limitations_

The above configurations are applicable from version 1.31 and onwards. Prior to version 1.31, the following applies. In particular, note that the lossless option made no difference on Android. 

|  | Lossy on iOS | Lossy on Android | Lossless on iOS | Lossless on Android |
| --- | --- | --- | --- | --- |
| Extension | .mp4 | .mp4 | .caf | .3gp |
| Sample Rate | 22050 | 8000 | 44100 | 8000 |
| Channels | 1 | 1 | 2 | 1 |
| Bit Rate | 32000 | 32000 | 128000 | 12800 |

## Rule Engine Interaction

### Loudness

The loudness file reacts and responds to the rule engine states as expected, just like any other sensors that write to CSV files.

### Audio File

Prior to version 1.31, the audio recording does not respect the rule engine. Since version 1.31, recording pauses and resumptions will apply to recordings. However, note that, once paused, the audio file timestamp is no longer aligned with the timestamps of other measurements. You should perform the necessary alignment yourself.

## Troubleshooting & Platform Limitations

### Constant `-160 dBFS` Readings or Missing Audio

- **`-160 dBFS` sentinel value**: A reading of `-160` dBFS represents the digital silence floor / null value when no audio signal reaches Sensor Logger. On Android, this typically occurs if another app holds exclusive microphone focus, the system-wide microphone privacy toggle is muted, or the recording was started while the app was in the background without foreground microphone eligibility.
- **Loudness recorded without `.mp4` audio**: Check _Settings > Sensor Configuration > Microphone Quality_ and confirm it is set to **Lossy** or **Lossless** rather than **Loudness** (which intentionally records `Microphone.csv` without audio). Also ensure no concurrent voice/call app preempted the audio session during recording.

### Simultaneous AirPods Motion (`Headphone`) and Audio on iOS

On iOS, enabling both the **Headphone** (AirPods motion) sensor and **Microphone** audio recording at the same time prevents `Headphone.csv` motion data from being recorded. This is an Apple iOS system limitation (`CMHeadphoneMotionManager` cannot stream motion samples while an active microphone audio recording session reconfigures the Bluetooth audio route). If you need AirPods motion data, disable the Microphone audio recording (or record audio on a separate device).
