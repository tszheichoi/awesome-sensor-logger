# Video-to-Sensor Synchronization

**Sensor Logger** embeds a high-precision **Timed Metadata** track directly into the MP4 video container. This track stores a nanosecond-resolution epoch timestamp for every camera buffer captured. This feature allows for synchronization between video frames and other Sensor Logger data (IMU, GPS, etc.) without manual offset calculation.

While video files are saved as `<timestamp>.mp4`, this timestamp reflects when the recording session started — before camera initialization and sensor setup. The video actually begins recording several hundred milliseconds later, so using the filename for alignment introduces a constant offset (e.g. ~695ms in testing on slow phones). The Timed Metadata Track avoids this by embedding per-frame epoch timestamps directly in the video, achieving high accuracy even under variable frame rates.

To extract this data, you will need two standard tools installed:

1. **ExifTool**: Used to read the embedded metadata track.
2. **FFmpeg (ffprobe)**: Used to read the video frame presentation timestamps.

## Step 1: Extract the Frame-to-Epoch Map

Run the following command to list every metadata sample with its relative video time and absolute epoch timestamp.

```bash
exiftool -q -q -ee3 -n -p '$SampleTime, $Mdtasensor_loggerEpoch_timestamp' file.mp4
```

**Example Output:**

```text
0, 1770510090666860288
0.033333875, 1770510090700194304
0.06666775, 1770510090733528064
0.100001583, 1770510090766861824
```

## Step 2: Extract Video Frame Timestamps

To find the exact time each video frame appears in the file, run:

```bash
ffprobe -v error -select_streams v:0 -show_entries frame=pts_time -of csv=p=0 file.mp4
```

**Example Output:**

```text
0.000000
0.033333
0.066667
```

## Step 3: Aligning the Data

The metadata track may contain extra samples due to encoder latency or dropped frames, especially towards the start or end of the video file. You should align the **PTS (Presentation Time Stamp)** from each frame against the PTS in the metadata track to find the epoch time.

_Note: Video encoders often round timestamps to fit a specific timescale, so a metadata PTS of `0.033333875` should be treated as a match for a video frame PTS of `0.033333`._

### Alignment Logic:

| Video PTS (`ffprobe`) | Metadata PTS (`exiftool`) | **Target Epoch (Nanoseconds)** |
| --------------------- | ------------------------- | ------------------------------ |
| **0.000000**          | 0                         | `1770510090666860288`          |
| **0.033333**          | 0.033333875               | `1770510090700194304`          |
| **0.066667**          | 0.06666775                | `1770510090733528064`          |

## Technical Notes

- **Precision:** The timestamps are captured using the same system clock as the sensor CSV files.
- **Variable Frame Rate (VFR):** Even if the video frame rate fluctuates (due to device heat or lighting changes), the metadata remains glued to the correct video buffer.

## Automated Alignment

For advanced users, this command performs the alignment and outputs a single CSV:

```bash
awk -F, 'NR==FNR {a[sprintf("%.2f",$1)]=$2; next} {t=sprintf("%.2f",$1); if(a[t]) print $1 "," a[t]}' <(exiftool -q -q -ee3 -n -p '$SampleTime, $Mdtasensor_loggerEpoch_timestamp' file.mp4) <(ffprobe -v error -select_streams v:0 -show_entries frame=pts_time -of csv=p=0 file.mp4)
```

## Experimental Verification

To verify alignment accuracy, we record a short session with the Camera (in video mode), Microphone, and Accelerometer sensors enabled. When video mode and the Microphone sensor are both on, the audio is embedded directly in the MP4 file. During the recording, a sharp clap is performed to produce a distinctive event visible in both the audio and accelerometer signals.

The accelerometer magnitude spike serves as ground truth, using the timestamps from its CSV file. The audio envelope extracted from the video is then aligned using two methods:

1. **Timed Metadata Track** — the per-frame epoch timestamps embedded in the MP4.
2. **Filename Timestamp** — the `<timestamp>.mp4` filename as the video start time.

To measure the offset for each method, we compute the cross-correlation between the audio envelope and the accelerometer magnitude, and find the lag that maximises alignment. This plot was generated from a recording on a very underpowered iPhone SE, which exacerbates the delay between the start of the recording session and the start of the video pipeline.

<img width="2400" height="2000" alt="sync_comparison" src="https://github.com/user-attachments/assets/71e326e6-2aad-494a-b875-193de45b5141" />

When using the filename timestamp, the clap appears to happen earlier in the video than in the accelerometer. This is because the filename is set at session start (time T), but the video only begins recording after setup completes (time T + delay). For example, an event at real time T + 2000ms is 1305ms into the video, but gets placed at T + 1305ms on the timeline — 695ms ahead of where the IMU sees it.
