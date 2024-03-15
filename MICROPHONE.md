# Microphone

When the Microphone sensor is toggled, Sensor Logger writes two files:

- Audio file in various formats.
    - On by default, but can be turned off.
    - Can change between lossy and lossless.
- Loudness in dBFS in a CSV.
    - Always recorded and its sampling frequency cannot be changed.

## Audio Quality Configuration

You can adjust the audio quality level in Sensor Logger. In the latest version, the settings “Lossy”and “Lossless” carry the following configurations. 

|  | Lossy on iOS | Lossy on Android | Lossless on iOS | Lossless on Android |
| --- | --- | --- | --- | --- |
| Extension | .mp4 | .mp4 | .mp4 | .mp4 |
| Sample Rate | 16000 | 16000 | 44100 | 4100 |
| Channels | 1 | 1 | 2 | 2 |
| Bit Rate | 32000 | 32000 | 128000 | 12800 |

The above configurations are applicable from version 1.31 and onwards. Prior to version 1.31, the following applies. In particular, note that the lossless option made not difference on Android. 

|  | Lossy on iOS | Lossy on Android | Lossless on iOS | Lossless on Android |
| --- | --- | --- | --- | --- |
| Extension | .mp4 | .mp4 | .caf | .3gp |
| Sample Rate | 22050 | 8000 | 44100 | 8000 |
| Channels | 1 | 1 | 2 | 1 |
| Bit Rate | 32000 | 32000 | 128000 | 12800 |

## Rule Engine Interaction

### Loudness

The loudness file reacts and responds to the rule engine states as expected, just like any other sensors to write to CSV files.

### Audio File

Prior to version 1.31, the audio recording does not respect the rule engine. Since version 1.31, recording pauses and resumptions will apply to recordings. However, note that, once paused, the audio file timestamp is no longer aligned with the timestamps of other measurements. You should perform the necessary alignment yourself.
