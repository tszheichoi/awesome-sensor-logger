# Video Quality, FPS & Alignment Reference

This documents settings and behaviours that are relevant when using the Camera sensor in Sensor Logger in Video mode.

| Setting       | Options                                                                   |
| ------------- | ------------------------------------------------------------------------ |
| Camera Mode   | Images, Snapshot, Video                                                  |
| Image Quality | Lowest 640x480, Low 1280x720, Medium 1920x1080, High = largest available |
| Max Video FPS | 15, 30, 60 (Video mode only)                                             |
| Capture Depth | Image, Image + Depth (iOS & Images mode only)                            |

## How Sensor Logger Picks Cameras

On iOS and Android, these settings are not independent knobs. Sensor Logger needs to pick the most suitable format based on the settings you choose, depending on the available hardware cameras / virtual cameras that the operating system exposes. 

The selection strategy follows this order:

1. **Camera.** Front or back, then Capture Depth, then Lens Preference. This picks the
   physical camera, and the camera decides which formats exist at all. Depth off prefers
   the camera with the most lenses, depth on prefers the fewest.
2. **FPS**, Video only. Formats that can hit the rate you asked for win. If none can, the
   rate is ignored entirely, see edge cases.
3. **Quality.** Of what is left, the format closest to your Image Quality, which can land
   above or below it. High means largest available.

As such, raising the rate can lower the resolution, and changing lens can change both. For **Images** and **Snapshot**, there is no FPS concept. See "Sampling
Frequencies" settings.

## Example

These were measured on an iPhone 17 Pro, with the back camera and depth off.

| Image Quality | 15 fps    | 30 fps    | 60 fps        |
| ------------- | --------- | --------- | ------------- |
| Lowest        | 640x480   | 640x480   | 640x480       |
| Low           | 1280x720  | 1280x720  | 1280x720      |
| Medium        | 1920x1080 | 1920x1080 | 1920x1080     |
| High          | 4032x3024 | 4032x3024 | **3840x2160** |

## Edge Cases

**The FPS setting is a ceiling, not a guarantee.** Dim light can drop the real rate far below it. From one example recording, measured in low light conditions indoors at night, setting High at 60 FPS gave 17 to 24 fps. Make sure you respect the variable frame rate when interpreting timing from the video, especially when you align with other sensors.

**An unreachable FPS is ignored, not approximated.** If no format can hit it, the rate stops counting entirely and you get whatever that Image Quality would have picked on its own, with no warning. The front camera at 60 returns 1920x1440 capped at 30. This is why 120 was removed: at High it returned 4032x3024 at 22 fps, and at Lowest it returned plain 640x480.

**High can change the aspect ratio with the frame rate.** 4:3 at 15 and 30, 16:9 at 60. Avoid High if you need consistent geometry.

**High is not always 4K**. For example, on some iPhones it could be the 4:3 full sensor frame, 4032x3024, depending on your FPS settings.

## Aligning Video With Sensor Data

Each video is saved as `<epoch_ms>.mp4`, and that filename is the epoch time of the **first frame**.

From experimentation, the filename matches the first embedded timestamp to within 0.9 ms every time. For most purposes the filename plus the frame presentation timestamps is enough for data alignment:

```
epoch_ms(frame) = filename_ms + (pts_time - first_pts) * 1000
```

```bash
ffprobe -v error -select_streams v:0 -show_entries frame=pts_time -of default=noprint_wrappers=1:nokey=1 file.mp4
```

- Subtract the first PTS, because it is not always zero.
- Use the real PTS, never the frame index divided by the FPS setting, because the rate varies.

This lands within about a millisecond on a clean recording, but drifts up to 18 ms when frames are being dropped in low light, since PTS is an encoder timeline rather than capture time.

For exact per frame timing, Sensor Logger embeds a timed metadata track holding a nanosecond epoch timestamp for every camera buffer, captured on the same clock as the sensor CSVs. This stays glued to the correct buffer under variable frame rate.

```bash
exiftool -q -q -ee3 -n -p '$SampleTime, $Mdtasensor_loggerEpoch_timestamp' file.mp4
```

```text
0, 1789343352703032064
0.01666575, 1789343352719697664
0.033331291, 1789343352736363264
```

Match these to frames by nearest SampleTime. Make sure you do not join by rounding both to a fixed number of decimals. The track carries a few more samples than the video has frames, at the end.
