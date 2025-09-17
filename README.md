# Awesome Sensor Logger
This repository contains a collection of tools, resources and sample code to use alongside the Sensor Logger app.

- [The Sensor Logger App](#the-sensor-logger-app)
- [Getting Started with Data Analysis](#getting-started-with-data-analysis)
  * [Recommended Tools](#recommended-tools)
  * [Understanding Timestamps](#understanding-timestamps)
  * [Understanding Units](#understanding-units)
  * [File Handling](#file-handling)
    + [Zip and CSV](#zip-and-csv)
    + [JSON](#json)
    + [SQLite](#sqlite)
  * [Accessing Recording Metadata](#accessing-recording-metadata)
  * [When to Use Uncalibrated Data](#when-to-use-uncalibrated-data)
  * [Plotting Data](#plotting-data)
  * [Diagnosing Sampling Rates](#diagnosing-sampling-rates)
  * [Mapping GPS Tracks](#mapping-gps-tracks)
  * [Aligning and Interpolating Measurements Across Sensors](#aligning-and-interpolating-measurements-across-sensors)
  * [Smoothing and Denoising](#smoothing-and-denoising)
  * [Fourier Transforms](#fourier-transforms)
  * [Track Simplification](#track-simplification)
  * [Peak Detection](#peak-detection)
  * [Activity Detection and Semantic Segmentation](#activity-detection-and-semantic-segmentation)
  * [Time Series Classification](#time-series-classification)
  * [Removing Duplicated Entries](#removing-duplicated-entries)
  * [Audio Analysis](#audio-analysis)
  * [Converting to GPX or InfluxDB](#converting-to-gpx-or-influxdb)
- [Recording Bluetooth LE sensors](#recording-bluetooth-le-sensors)
  * [Postprocessing Bluetooth LE sensor recordings](#postprocessing-bluetooth-le-sensor-recordings)
    + [Example Logging a Ruuvi Tag with Sensor Logger](#example-logging-a-ruuvi-tag-with-sensor-logger)
    + [Example After Post-processing Ruuvi Tag Reported Values](#example-after-post-processing-ruuvi-tag-reported-values)
- [Live Data Streaming](#live-data-streaming)
  + [Setting Up Server](#setting-up-server)
  	+ [RequestBin](#requestbin)
  	+ [Timeplus](#timeplus)
  	+ [Javascript Webserver](#javascript-webserver)
  	+ [Python Webserver](#python-webserver)
- [Further Use Cases and Applications](#further-use-cases-and-applications)
- [Contribute](#contribute)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

<img width="970" alt="hero" src="https://user-images.githubusercontent.com/30114997/173469460-f20062ab-7b47-47bf-9f93-a266fa457ae9.png">

## The Sensor Logger App
Sensor Logger is a free, easy-to-use, cross-platform data logger that logs readings from common motion-related sensors on smartphones. Once completed, recordings can be exported as a zipped CSV file, JSON, SQLite, KML or be viewed within the app via interactive plots. There is also a free companion watch app (WatchOS and WearOS) that allows you to log heart rate & wrist motion, and control recording sessions remotely from your wrist. Supported sensors and measurements include:

- Device Acceleration (Accelerometer; Raw & Calibrated), G-Force
- Gravity Vector (Accelerometer)
- Device Rotation Rate (Gyroscope)
- Device Orientation (Gyroscope; Raw & Calibrated)
- Magnetic Field (Magnetometer; Raw & Calibrated)
- Compass
- Barometric Altitude (Barometer), Atmospheric Pressure
- GPS: Altitude, Speed, Heading, Latitude, Longitude
- Audio (Microphone)
- Loudness (Microphone), Sound Meter
- Camera Images (Front & Back, Foreground)
- Camera Depth (Front & Back, Foreground, iOS Only)
- Camera Video (Front & Back, Foreground)
- Pedometer
- Heart Rate (Apple Watch or Android WearOS)
- Wrist Motion (Apple Watch or Android WearOS)
- Watch Location (Apple Watch or Android WearOS)
- Watch Barometer (Apple Watch or Android WearOS)
- Light Sensor (Android Only)
- Annotations (Timestamp and Text)
- Device Battery Level and State
- Device Screen Brightness Level
- Nearby Bluetooth Beacons (All Advertised Data)
- Nearby WiFi Networks (Android Only)
- Battery Temperature (Android Only)
- Headphone Motion (Requires AirPods)
- Network

Learn more and download Sensor Logger at www.tszheichoi.com/sensorlogger. 

| Android | iOS |
|:-:|:-:|
| [<img src="https://play.google.com/intl/en_us/badges/static/images/badges/en_badge_web_generic.png" height="50">](https://play.google.com/store/apps/details?id=com.kelvin.sensorapp&pcampaignid=pcampaignidMKT-Other-global-all-co-prtnr-py-PartBadge-Mar2515-1) | [<img src="https://developer.apple.com/app-store/marketing/guidelines/images/badge-example-preferred_2x.png" height="50">](https://apps.apple.com/app/id1531582925) |

## Performing Cross-Platform Analysis?
If you are performing cross-platform analysis using Sensor Logger, please beware of some minor unit differences and some important coordinate system differences between iOS and Android. Depending on your analysis, you may have to multiply values by a negative sign. See the [Units Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md) and the [Coordinates Reference](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md). 

> 💡: **New in Version 1.29**: Toggling **Standardise Units & Frames** under _Settings > Sensor Configuration_ will eliminate a lot of convention differences between iOS and Android. See [this](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/CROSSPLATFORM.md) for more information. 

## Getting Started with Data Analysis
Measurements made using the Sensor Logger can be exported in `.zip`, `.csv`, `.json`, `.kml` or `.sqlite` formats. For data analysis, the zip export is recommended as it is free and contains all the raw data. See www.tszheichoi.com/sensorloggerhelp for more about how exporting works.

### Recommended Tools
Python is recommended for analysing the outputs from Sensor Logger. For interactive data exploration and visualisation, use Jupyter Notebooks, which you can run for free easily with tools like Google Colab or Deep Notes. Your typical data science Python packages apply:

- Pandas for CSV parsing and manipulation
- Numpy for data analysis
- SciPy for time series analysis
- Folium / Leaflet.js for geospatial visualisation
- Dash / Flask for data streaming

### Understanding Timestamps
All exported data have synchronised time stamps, meaning they can be cross-referenced. However, they **do not necessarily align** due to varied sampling rates. This is by design, so you can have the most precise timing for each sensor. If you require cross-sensor resampling, see the "Aligning and Interpolating Measurements Across Sensors" section below. 

- The `time` column is the UNIX epoch timestamp of the measurement as reported by the sensors in nanoseconds. By definition, these are UTC times -- whereas the filenames are in local times.
  - You can use tools like https://www.epochconverter.com/ to convert them to readable timestamps.
  - If you use Python, some libraries may expect miliseconds instead of nanoseconds. Divide by 1000000 accoridngly.
  - If you use Excel, you may want to convert it to fraction of day so that Excel can recognise it properly as datetime. To do so, divide by 1,000,000,000 * 60 * 60 * 24, and then format the column or cell as time.
- The `seconds_elapsed` column is the number of seconds since you tapped the Start Recording button. Note that some entries could be negative, meaning the measurements were made *before* the start of the recording, but are reported by your phone *after* the tap due to buffering or caching.
- Optionally, you can enable human readable timestamps to be logged alongside all your data. To toggle this, go to settings by tapping on the gear icon on the Logger Screen. Then navigate to Recording & Workflow and scroll to the bottom. 

Please note that the accuracy of timestamps relies on accurate system timestamps. Please make sure your phone’s time is accurate to ensure physically correct timestamps. If your phone changes time zone mid-recording, it may also lead to unpredictable behaviour. 

### Understanding Units
See [https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/UNITS.md) for the full documentation of units.

> :warning: **If you are analysing uncalibrated acceleration data across platforms**, there are important differences in unit definitions that you should be aware of.
> 
### Understanding Coordinate Systems

See [https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md](https://github.com/tszheichoi/awesome-sensor-logger/blob/main/COORDINATES.md) for the full documentation of coordinate systems.

> :warning: **If you are analysing acceleration & orientation values across platforms**, there are important differences in the reference frame definitions that you should be aware of.

### File Handling

#### Zip and CSV
- Normally, just use https://docs.python.org/3/library/zipfile.html, but for batch unzipping in Python, read https://superfastpython.com/multithreaded-unzip-files/
- Reading `.csv`: Use `pandas`, see below.
- Reading audio file: Depends on whether you have compression enabled in the Sensor Logger's settings. 
    - Do read https://hackernoon.com/audio-handling-basics-how-to-process-audio-files-using-python-cli-jo283u3y
    - Use https://librosa.org/doc/latest/index.html

#### JSON
The JSON export format is a single file, where the contents are an array of objects. Each object represents a single record (row).
All records for a given sensor are grouped together and are then sorted by time.
```
[
  {
    "sensor": "Accelerometer",
    "time": "1698501144401773000",
    "seconds_elapsed": "0.21677294921875",
    "z": "-0.10382747650146484",
    "y": "-0.0009566396474838257",
    "x": "0.06110857427120209"
  },
  {
    "sensor": "Accelerometer",
    "time": "1698501144411773000",
    "seconds_elapsed": "0.22677294921875",
    "z": "-0.10387134552001953",
    "y": "-0.002205267548561096",
    "x": "0.06393256038427353"
  },
  {
    "sensor": "Location",
    "time": "1698501145514000000",
    "seconds_elapsed": "1.328999755859375",
    "bearingAccuracy": "0",
    "speedAccuracy": "0",
    "verticalAccuracy": "1.773818016052246",
    "horizontalAccuracy": "15.102999687194824",
    "speed": "0",
    "bearing": "0",
    "altitude": "214.1999969482422",
    "longitude": "0.0",
    "latitude": "0.0"
  }
]
```

#### SQLite
For reading data exported using the SQLite option in Python, you may try:
```
import sqlite3

database_file = 'your_database_file.sqlite'

try:
    connection = sqlite3.connect(database_file)
    cursor = connection.cursor()

    sql_query = "SELECT * FROM Accelerometer"

    cursor.execute(sql_query)
    results = cursor.fetchall()

    for row in results:
        print(row)

except sqlite3.Error as e:
    print(f"SQLite error: {e}")

finally:
    cursor.close()
    connection.close()
```

### Accessing Recording Metadata
The `metadata.csv` file contains information about the device that performed the logging.
- version: The schema version of the exported data. This is different to the version of the app. When this version increments, you may have to update your data analysis script as things such as the column names, file names, or data structure may have changed. 
- device name: The name of the device used for recording.
- recording time: The start time of the recording in UTC.
- platform: Either iOS or Android.

### When to Use Uncalibrated Data
Sensor Logger gives you the option to log raw, uncalibrated data from the accelerometer, gyroscope and magnetometer. Calibrated data is always logged. The raw stream is useful for performing lower-level post-processing or custom sensor fusion. If in doubt, *always* use the calibrated version unless you have a good reason not to. 

### Plotting Data
Use `pandas` to import `.csv` and convert timestamps. Use Plotly to visualise data interactively. Here, we show the acceleration experienced by a user during a roller coaster ride. 
```
import pandas as pd
import plotly.graph_objects as go

df = pd.read_csv('Accelerometer.csv')
df.index = pd.to_datetime(df['time'], unit = 'ns')

fig = go.Figure()

for axis in ['x', 'y', 'z']:
    fig.add_trace(go.Scatter(x = df.index, y = df[axis], name = axis))

fig.show()
```
<img width="937" alt="simple_accel" src="https://user-images.githubusercontent.com/30114997/173203712-3079afc2-a210-482a-9073-e4b2e31281b8.png">

Some sensors may also report uncertainties, which is important for analysis and multi-sensor fusion. For example, the speed from GPS has associated errors. 

```
import pandas as pd
import plotly.graph_objects as go

df = pd.read_csv('Location.csv')
df.index = pd.to_datetime(df['time'], unit='ns')

fig = go.Figure()

fig.add_trace(go.Scatter(x=df.index, y=df['speed'], mode='markers',
              error_y={'type': 'data', 'array': df['speedAccuracy']}))

fig.show()
```
<img width="879" alt="error_gps" src="https://user-images.githubusercontent.com/30114997/173204026-a55c2f9e-1f52-44d5-ba4e-6f3a69eeee72.png">

### Diagnosing Sampling Rates
Real-world measurements are never evenly sampled. It is important to double-check before any analysis. For example, this particular GPS location data recorded on an iPhone has `avg_sampling_rate` of 0.93Hz, but the measurement gap ranges between 0.99 to 12 seconds.
```
import pandas as pd
import numpy as np

df = pd.read_csv('Location.csv')
consecutive_deltas = df['seconds_elapsed'].diff()
avg_sampling_rate = 1 / np.mean(consecutive_deltas)
shortest_gap = np.min(consecutive_deltas)
maximum_gap = np.max(consecutive_deltas)
total_num_of_samples = len(df.index)
```
To resample your data, for example, to minute periods:
```
import pandas as pd

df = pd.read_csv('Location.csv')
df.index = pd.to_datetime(df['time'], unit = 'ns')
df.resample('1T').median()
```
Also read https://www.earthdatascience.org/courses/use-data-open-source-python/use-time-series-data-in-python/date-time-types-in-pandas-python/resample-time-series-data-pandas-python/

To understand the implications and robustness of resampling and dealing with missing data in motion-related time series, consult the following:

- https://towardsdatascience.com/preprocessing-iot-data-linear-resampling-dde750910531
- Impact of Reduced Sampling Rate on Accelerometer-based Physical Activity Monitoring and Machine Learning Activity Classification: https://www.medrxiv.org/content/10.1101/2020.10.22.20217927v1.full
- Sensor Data Augmentation by Resampling for Contrastive Learning for Human Activity Recognition: https://arxiv.org/pdf/2109.02054.pdf

### Mapping GPS Tracks
Use tools like Folium, which is built on top of leaflet.js to overlap GPS tracks on a map
- https://towardsdatascience.com/build-interactive-gps-activity-maps-from-gpx-files-using-folium-cf9eebba1fe7
- https://towardsdatascience.com/simple-gps-data-visualization-using-python-and-open-street-maps-50f992e9b676

```
import folium
import pandas as pd

df = pd.read_csv("Location.csv")
coords = [(row.latitude, row.longitude) for _, row in df.iterrows()]

my_map = folium.Map(location=[df.latitude.mean(), df.longitude.mean()], zoom_start=16)
folium.PolyLine(coords, color="blue", weight=5.0).add_to(my_map)
```

<img width="972" alt="thorpe_park_track" src="https://user-images.githubusercontent.com/30114997/173207512-cffd38f0-400f-44ef-b3b3-2e7963a51a88.png">

Alternatively, convert your exported data to GPS using https://github.com/mhaberler/sensorlogger-util, and then upload to Google Maps for visualisation, following, for example, https://www.alphr.com/gpx-google-maps/. 

### Aligning and Interpolating Measurements Across Sensors
Often, one has to align measurements across sensors -- for instance, gyroscope and accelerometer so that you can apply rotation matrixes to the acceleration vectors. 

- Option 0: Use Sensor Logger's built-in "Combined CSV" export option. Note that this feature requires one of the paid subscription tiers. You can easily configure how you want to resample, upsample and downsample your measurements. The output of this is a single `.csv` file, saving you the hassle of dealing with alignment issues. If you prefer doing it yourself, see options 1 and 2 below.

<img width="659" alt="Screenshot 2023-10-25 at 15 07 19" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/f31366ae-ba81-4ff5-9984-156f8ccf5732">

- Option 1: Perform an outer join and then interpolate missing values for both sensors. By default, `pandas` interpolates linearly, but see the documentation for more advanced options.
```
import pandas as pd
import numpy as np

df_gyro = pd.read_csv('Gyroscope.csv')
df_acce = pd.read_csv('Accelerometer.csv')

for df in [df_gyro, df_acce]:
    df.index = pd.to_datetime(df['time'], unit = 'ns')

df = df_gyro.join(df_acce, lsuffix = '_gyro', rsuffix = '_acce', how = 'outer').interpolate()
```
- Option 2: Interpolate one sensor onto the timestamps of another -- probably better if the two sensors have wildly different sampling rates. For example: 
```
np.interp(df_acce.index, df_gyro.index, df_gyro['x'])
```
Using option 1 above, the altitude readings from both the GPS and barometer are resampled and aligned. As you can see, the GPS is not great at characterising rapid altitude changes, and exhibits biases during transient periods.

<img width="929" alt="resampled_altitudes" src="https://user-images.githubusercontent.com/30114997/173237727-d48fa023-4d47-48db-91b0-48e15fb060e1.png">

For more complex alignment needs -- such as aligning with measurements from sources other than Sensor Logger, you may need techniques such as cross-correlation or dynamic time warping:
- https://towardsdatascience.com/dynamic-time-warping-3933f25fcdd
- https://dtaidistance.readthedocs.io/en/latest/usage/dtw.html
- https://dynamictimewarping.github.io/

### Smoothing and Denoising
Different applications require different smoothing and denoising strategies. This scipy cookbook has some handy code you can borrow:
- https://scipy-cookbook.readthedocs.io/items/SignalSmooth.html
- https://scipy-cookbook.readthedocs.io/items/SavitzkyGolay.html
- Also try `scipy.ndimage.median_filter`

Referencing the previous section on interpolation, performing downsampling with a suitable aggregator (e.g. median) or interpolation with suitable spline or polynomial functions may also achieve smoothing. You can also apply a rolling median (or rolling mean) technique with ease using pandas, which can also achieve smoothing and anomaly removal:

```
import pandas as pd

df_gyro = pd.read_csv('Gyroscope.csv')
window_size = 200
smoothed_gyro = df_gyro['x'].rolling(window=window_size, min_periods=1).mean()
print(smoothed_gyro)
```

### Fourier Transforms
Use Fourier transforms to understand any periodicity in your logged values. For example, you can detect walking by simply thresholding the gravity vector measurements in frequency space. Here is a simple example of Fourier transforming the gravity measurements taken on [Zodiac, a spinning ride at Thorpe Park](https://en.wikipedia.org/wiki/Zodiac_(ride)). As you can see, there is a peak around 0.25 Hz (i.e. the ride goes around one revolution every 4 seconds). 

```
import pandas as pd
import numpy as np

df = pd.read_csv('Gravity.csv')
ts = pd.to_datetime(df['time'], unit = 'ns')
period = np.nanmedian(ts.diff().dt.total_seconds())

sp = np.fft.fft(df['x'])
freq = np.fft.fftfreq(len(df.index), period)

mask = (freq >= 0) &(freq < 1)

fig = go.Figure()
fig.add_trace(go.Scatter(x = freq[mask], y = [np.linalg.norm(s) for s in sp[mask]]))
fig.show()
```

<img width="935" alt="zodiac" src="https://user-images.githubusercontent.com/30114997/173238828-438cf3db-e767-4dd3-a0af-7295393aae4e.png">

### Track Simplification
You can use algorithms like Douglas-Peucker to simplify recorded GPS tracks to save storage space for long recordings. A Sensor Logger specific implementation can be found here: https://github.com/mhaberler/sensorlogger-util/blob/master/simplify.py

### Peak Detection
Scipy's `find_peaks` is the easiest place to get started. For example:

```
import pandas as pd
import numpy as np
from scipy.signal import find_peaks
import plotly.graph_objects as go

df_accel = pd.read_csv('Accelerometer.csv')
signal = df_accel['x']
min_distance = 25
peaks, _ = find_peaks(signal, distance=min_distance)

fig = go.Figure()
fig.add_trace(go.Scatter(x=peaks, y=signal[peaks], mode='markers', marker=dict(color='red', size=10)))
fig.add_trace(go.Scatter(x=range(len(signal)), y=signal, mode='lines'))
fig.show()

print("Indices of peaks:", peaks)
```

<img width="1065" alt="Screenshot 2023-10-25 at 15 17 17" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/2b1d3dd0-2a3a-433c-823d-e284fd0d3074">


Also see:
- https://docs.scipy.org/doc/scipy/reference/generated/scipy.signal.find_peaks.html
- https://en.wikipedia.org/wiki/Topographic_prominence
- https://stackoverflow.com/questions/1713335/peak-finding-algorithm-for-python-scipy

### Activity Detection and Semantic Segmentation
- A Comprehensive Study of Activity Recognition Using Accelerometers: https://www.researchgate.net/publication/325470495_A_Comprehensive_Study_of_Activity_Recognition_Using_Accelerometers
- Useful tool for time series data mining tasks: https://stumpy.readthedocs.io/en/latest/
- Kang et al. 2017 A Novel Walking Detection and Step Counting Algorithm Using Unconstrained Smartphones

<img width="1069" alt="Screenshot 2023-10-25 at 15 18 06" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/bc373657-e407-4051-b276-7900f4ce763f">

### Time Series Classification
- https://towardsdatascience.com/a-brief-introduction-to-time-series-classification-algorithms-7b4284d31b97

### Removing Duplicated Entries
Sometimes, erroneous sensors may report the same value twice with identical timestamps, likely due to caching. Try something like this to remove them:
```
def remove_duplicated_rows(df: pd.DataFrame):
    _df = df[
        ~(df["timeStamp"].diff() < 0)
    ]  # be careful that diff() gives nan for first row
    if len(_df.index) != len(df.index):
        print(
            f"duplicated rows detected in the input file ({len(df.index) - len(_df.index)}"
        )
    return _df
``` 
### Audio Analysis
`ffmpeg-python` (https://github.com/kkroening/ffmpeg-python) has some valuable examples of interesting audio analysis:
- Splitting silence: https://github.com/kkroening/ffmpeg-python/blob/master/examples/split_silence.py
- Audio transcription with Google Cloud: https://github.com/kkroening/ffmpeg-python/blob/master/examples/transcribe.py

`pyAudioAnalysis` is also worth checking out for audio feature extraction, classification and segmentation: https://github.com/tyiannak/pyAudioAnalysis

### Converting to GPX or InfluxDB
Michael Haberler has helpfully put together a command-line tool `sensorlogger-utils` to take the JSON exported from Sensor Logger and convert it to GPX or InfluxDB formats: https://github.com/mhaberler/sensorlogger-util

```
python sensorlogger -g <json file>
```
```
python sensorlogger.py -2 [--bucket sensorlogger] --token xxx  --org yyyy --url http://host:8086 2022-06-14_03-15-05.json
```

## Recording Bluetooth LE sensors
Version 1.17 adds the capability to record values reported from a wide range of Bluetooth LE sensors which report values via periodic advertisements.

Sensor Logger lets you scan for, and choose to record such BLE sensors, and will record their advertisements in the log. Sensor Logger supports this method of reporting values, but is unaware of how any particular sensor encodes its values. Therefore, Sensor Logger records the advertisement (and in particular the manufacturer data field) and leaves the interpretation of these records to a later postprocessing step.

This means that any - existing or yet-to-be-designed - BLE sensor using this reporting method is _supported_ by Sensorlogger - because it implements just the recording, but not the sensor-specific interpretation step.

A list of sensors that should work out of the box with Sensorlogger can be found here: https://decoder.theengs.io/devices/devices.html - however, any device using this method can be recorded.

Also, custom-built sensors can be recorded - an example project which has been verified to work with Sensor Logger can be found here: https://github.com/mhaberler/flowsensor

### Postprocessing Bluetooth LE sensor recordings
To interpret BLE sensor recordings, the exported log must be post-processed. An experimental service has been put together here: https://sensorlogger.mah.priv.at/sensorlogger - the source code can be found [here](https://github.com/mhaberler/sensorlogger-utils). Feel free to fork and roll your own.

#### Example Logging a Ruuvi Tag with Sensor Logger
This is how Sensorlogger records a [Ruuvi Tag](https://ruuvi.com/):
```
{
    "sensor": "bluetooth-DB08D33338EF",
    "time": "1690316310897000000",
    "seconds_elapsed": "0.906",
    "rssi": "-79",
    "id": "DB:08:D3:33:38:EF",
    "txPowerLevel": "",
    "manufacturerData": "99040512735828ffff0070fc18012890962ec379db08d33338ef"
}
```
The values are contained in the `manufacturerData` field, but make no sense as they stand. A quick and dirty way of parsing this is with an online decoder. For example, use https://parser.theengs.io/. Select TPMS and copy and replace the entire manufacturerData. Then click decode. If this is from a recognised sensor, such as this Ruuvi Tag example, then you will see the decoded information. 

<img width="1379" alt="parser" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/9aae62e8-1e6a-4a85-b140-b238b21f4002">

#### Example After Post-processing Ruuvi Tag Reported Values
Decoding with https://sensorlogger.mah.priv.at/sensorlogger expands this into the values which actually make sense:

```
{
    "sensor": "bluetooth-DB08D33338EF",
    "time": 1690316310896.9998,
    "seconds_elapsed": 0.906,
    "rssi": -79,
    "id": "DB:08:D3:33:38:EF",
    "txPowerLevel": "",
    "values": {
      "name": "Ruuvi 38EF",
      "rssi": -79,
      "brand": "Ruuvi",
      "model": "RuuviTag",
      "model_id": "RuuviTag_RAWv2",
      "type": "ACEL",
      "track": true,
      "tempc": 23.615,
      "tempf": 74.507,
      "hum": 56.42,
      "pres": 1155.35,
      "accx": 0.10983448,
      "accy": -0.980665,
      "accz": 0.29027684,
      "volt": 2.756,
      "tx": 4,
      "mov": 46,
      "seq": 50041,
      "mac": "DB:08:D3:33:38:EF"
    }
  }
```
## Live Data Streaming
> 💡: **New in Version 1.30**: Sensor Logger now supports pushing live data via MQTT. See https://github.com/tszheichoi/awesome-sensor-logger/blob/main/PUSHING.md for more. 

Sensor Logger supports pushing live data via HTTP. This can be enabled by tapping the gear icon on the Logger page. All enabled sensors during a recording will be streamed every 200ms to the specified URL. To display the streamed data, you will need to set up a webserver on another computer. 

<img width="667" alt="Screenshot 2023-10-25 at 15 09 43" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/19e800bb-3efd-40ae-b25b-22c92da1e071">

HTTP Push sends a POST request to the supplied URL with content-type "application/json". The request body is of the following format:
```
{
    messageId: 0,
    sessionId: "identifier",
    deviceId: "identifier",
    payload: [
        {
            "name": "accelerometer",
            "time": 1698501144401773000,
            <other fields depending on sensor>
        },
        {
            "name": "location",
            "time": 1698501145514000000,
            <other fields depending on sensor>
        },
    ],
}
```
The `messageId` is incremented for each message sent. The `messageId` is useful because the messages can be received out-of-order, which may need to be handled depending on your use case. The `sessionId` is the same for all messages in a single recording, and the `deviceId` is the same for all messages from a single device. The time is in UTC epoch nanoseconds.

Note: due to legacy reasons, on Android only, some sensors report accuracy alongside `name` and `time`. This is left in-place for backwards compatibility. Interpreting this field:
- 0 means unreliable
- 1 means low accuracy
- 2 means medium accuracy
- 3 means maximum accuracy

### Setting Up Server
There are many ways to setup a server that can accept messages pushed from Sensor Logger -- from off-the-shelf solutions to running the server yourself. Here are some pointers to get you started. It is recommended (but not required) for servers to respond with HTTP code 200. If the server responds with HTTP code 499 and the body contains text, then this message will be shown to the user (once per recording).

#### RequestBin
To simply consume and explore the data, you may want to use something like https://requestbin.com/. To plot the data in real-time, you may need something more custom. See https://github.com/mhaberler/sensorlogger-telegraf for a solution using telegraf. 

#### Timeplus
Also checkout Timeplus, a real-time streaming analytics platform: https://www.youtube.com/watch?v=iWA8FHjyatE. They also offer a dockerised solution. See https://github.com/timeplus-io/proton/tree/develop/examples/awesome-sensor-logger

![image](https://user-images.githubusercontent.com/30114997/224557365-dfe593f5-e84f-4fcf-9900-9bcfd31c5e44.png)

#### Javascript Webserver
Thanks to [Harshad Joshi](github.com/user/hj91), you can find a javascript implementation using nodejs for a webserver that is designed for Sensor Logger: https://github.com/hj91/json-server

#### Python Webserver
If you prefer sticking with Python, here is an implementation using Plotly Dash to get you started. Dash is powered by Flask under the hood, and provides an easy way to set up a web server for real-time, interactive data visualisation. This code listens on the `/data` endpoint, filters only the values from the accelerometer and plots it. The `update_graph()` callback is triggered every `UPDATE_FREQ_MS`, and updates the plot with any accumulated measurements so far. You will have to customise this script yourself if you want to plot measurements from other sensors. 

```
import dash
from dash.dependencies import Output, Input
from dash import dcc, html, dcc
from datetime import datetime
import json
import plotly.graph_objs as go
from collections import deque
from flask import Flask, request

server = Flask(__name__)
app = dash.Dash(__name__, server=server)

MAX_DATA_POINTS = 1000
UPDATE_FREQ_MS = 100

time = deque(maxlen=MAX_DATA_POINTS)
accel_x = deque(maxlen=MAX_DATA_POINTS)
accel_y = deque(maxlen=MAX_DATA_POINTS)
accel_z = deque(maxlen=MAX_DATA_POINTS)

app.layout = html.Div(
	[
		dcc.Markdown(
			children="""
			# Live Sensor Readings
			Streamed from Sensor Logger: tszheichoi.com/sensorlogger
		"""
		),
		dcc.Graph(id="live_graph"),
		dcc.Interval(id="counter", interval=UPDATE_FREQ_MS),
	]
)


@app.callback(Output("live_graph", "figure"), Input("counter", "n_intervals"))
def update_graph(_counter):
	data = [
		go.Scatter(x=list(time), y=list(d), name=name)
		for d, name in zip([accel_x, accel_y, accel_z], ["X", "Y", "Z"])
	]

	graph = {
		"data": data,
		"layout": go.Layout(
			{
				"xaxis": {"type": "date"},
				"yaxis": {"title": "Acceleration ms<sup>-2</sup>"},
			}
		),
	}
	if (
		len(time) > 0
	):  #  cannot adjust plot ranges until there is at least one data point
		graph["layout"]["xaxis"]["range"] = [min(time), max(time)]
		graph["layout"]["yaxis"]["range"] = [
			min(accel_x + accel_y + accel_z),
			max(accel_x + accel_y + accel_z),
		]

	return graph


@server.route("/data", methods=["POST"])
def data():  # listens to the data streamed from the sensor logger
	if str(request.method) == "POST":
		print(f'received data: {request.data}')
		data = json.loads(request.data)
		for d in data['payload']:
			if (
				d.get("name", None) == "accelerometer"
			):  #  modify to access different sensors
				ts = datetime.fromtimestamp(d["time"] / 1000000000)
				if len(time) == 0 or ts > time[-1]:
					time.append(ts)
					# modify the following based on which sensor is accessed, log the raw json for guidance
					accel_x.append(d["values"]["x"])
					accel_y.append(d["values"]["y"])
					accel_z.append(d["values"]["z"])
	return "success"


if __name__ == "__main__":
	app.run_server(port=8000, host="0.0.0.0")
```

Run this Python script and visit `http://localhost:8000/` on your computer. Then you have to enter the correct Push URL in Sensor Logger on your phone under the settings page. To find out the localhost of the device you are running the websever on, you can, for example, do something like this in Python. 

```
import socket
hostname = socket.gethostname()
print(socket.gethostbyname(hostname))
```

For example, if it returns `192.168.1.168`, then you want to enter `http://192.168.1.168:8000/data` in Sensor Logger. Use the "Tap to Test Pushing" button to test whether Sensor Logger can properly reach the endpoint. If you get a 200 response, then you are good to go! Start a recording as usual, and you should begin to see data being streamed in:

<img width="1440" alt="Screenshot 2022-07-10 at 10 23 03" src="https://user-images.githubusercontent.com/30114997/178138947-8522be59-4c0b-4966-84ad-49416fda5fc0.png">

#### Simple Streaming Demo (MQTT)
A simple web based demo app is available at https://github.com/tszheichoi/sensor-logger-streaming-demo-app. It connects to an MQTT broker, consumes streaming data, and visualizes it in an interactive plot. The demo also illustrates how to handle data from multiple devices simultaneously.

## Further Use Cases and Applications
Based on [user-submitted feedback](https://www.tszheichoi.com/sensor-logger-feedback), Sensor Logger is being use for a lot of applications -- for researchers and hobbyists alike. Here are a few to get you started. Let me know, and I will feature your use case here as well!

### Published Research
Some recently published papers citing / using Sensor Logger:

- Bingnan Duan, Yinhuan Dong, Ilari Vallivaara and Tughrul Arslan, "Anchored by Sound: Indoor Trajectory Mapping with Activity-Driven Audio Anchors", 2025 15th International Conference on Indoor Positioning and Indoor Navigation (IPIN), Tampere Finland
- Y. Dong, K. Kwan and T. Arslan, "Enhanced Pedestrian Trajectory Reconstruction Using Bidirectional Extended Kalman Filter and Automatic Refinement," 2024 14th International Conference on Indoor Positioning and Indoor Navigation (IPIN), Kowloon, Hong Kong, 2024, pp. 1-6, doi: 10.1109/IPIN62893.2024.10786127.
- I. Vallivaara, Y. Dong and T. Arslan, "Saying goodbyes to rotating your phone: Magnetometer calibration during SLAM," 2024 14th International Conference on Indoor Positioning and Indoor Navigation (IPIN), Kowloon, Hong Kong, 2024, pp. 1-7, doi: 10.1109/IPIN62893.2024.10786161.
- Rodi Laanen, Maedeh Nasri, Richard van Dĳk, Mitra Baratchi, Alexander Koutamanis, & Carolien Rieffe. (2023). Automated classification of pre-defined movement patterns: A comparison between GNSS and UWB technology.
- Shin, J. I. and Kim, J. O.: Possibility of Crowdsourcing-based Method for Surveying the Flatness of Pedestrian Spaces, Int. Arch. Photogramm. Remote Sens. Spatial Inf. Sci., XLVIII-4/W10-2024, 163–168, https://doi.org/10.5194/isprs-archives-XLVIII-4-W10-2024-163-2024, 2024.
- N. Loecher, S. King, J. Cabo, T. Neal and K. Kosyluk, "Assessing the Efficacy of a Self-Stigma Reduction Mental Health Program with Mobile Biometrics: Work-in-Progress," 2023 IEEE 17th International Conference on Automatic Face and Gesture Recognition (FG), Waikoloa Beach, HI, USA, 2023, pp. 1-6, doi: 10.1109/FG57933.2023.10042655.
- Etienne, A. J., Field, W. E., Ehlers, S. G., Tormoehlen, R., & Haslett, N. J. (2024). Testing the feasibility of selected, commercially available wearable devices in detecting agricultural-related incidents. Journal of Agricultural Safety and Health, 30(4), 181–204. https://doi.org/10.13031/jash.15985 
- Degambur, L.-N. (2024). Replay attack prevention in decentralised contact tracing: A blockchain-based approach. OALib, 11(02), 1–17. https://doi.org/10.4236/oalib.1111179
- Xiping Sun, Jing Chen, Cong Wu, Kun He, Haozhe Xu, Yebo Feng, Ruiying Du, & Xianhao Chen. (2024). MagLive: Near-Field Magnetic Sensing-Based Voice Liveness Detection on Smartphones.
- Gadelho, J., & Guedes Soares, C. (2024). Experimental Motion Measurements of a Floating Dual Chamber OWC Using the Smartphone Sensors as a Low Budget Solution. In Innovations in Renewable Energies Offshore Proceedings of the 6th International Conference on Renewable Energies Offshore.
- Zhang, J., Lau, M. C., & Zhu, Z. (2024). Hybrid CNN-GRU model for exercise classification using IMU Time-series data. Journal of Machine Intelligence and Data Science, 5. https://doi.org/10.11159/jmids.2024.007
- Zhang, J., Lau, M. C., & Zhu, Z. (2024). Advanced Exercise Classification with a hybrid CNN-GRU model: Utilising IMU data from cell phones. International Conference of Control, Dynamic Systems, and Robotics. https://doi.org/10.11159/cdsr24.115 
- Lee, M. J., Lin, J., & Hsu, L. T. (2024). Exploring the Feasibility of Automated Data Standardization using Large Language Models for Seamless Positioning. arXiv preprint arXiv:2408.12080.
- Vallivaara, I., Dong, Y., & Arslan, T. (2024). Saying goodbyes to rotating your phone: Magnetometer calibration during SLAM. arXiv preprint arXiv:2409.01242.
- Ray, L. S. S., Geißler, D., Liu, M., Zhou, B., Suh, S., & Lukowicz, P. (2024). ALS-HAR: Harnessing Wearable Ambient Light Sensors to Enhance IMU-based HAR. arXiv preprint arXiv:2408.09527.
- Yonetani, R., Baba, J., & Furukawa, Y. (2024, October). RetailOpt: Opt-In, Easy-to-Deploy Trajectory Estimation from Smartphone Motion Data and Retail Facility Information. In Proceedings of the 2024 ACM International Symposium on Wearable Computers (pp. 125-132).

If you have published work using Sensor Logger, feel free to reach out or make a pull request.

### Software Directory
- https://software.umich.edu/titles/sensor-logger-app

### Other Uses
- Hot air balloon tracking
- Flight data logging
- Wearable technology research
- Pedestrian dead reckoning
    - https://github.com/IdoMatan/PDR
- Roller coaster tracking
    - https://www.tszheichoi.com/coaster
- Sports research
    - https://www.tandfonline.com/doi/abs/10.1080/02640414.2021.1993640?journalCode=rjsp20
- Vehicle tracking
    - https://www.ndss-symposium.org/wp-content/uploads/vehiclesec2024-52-paper.pdf
- Figure skating analysis
- Whale watching
- Video stabilisation
    - https://docs.gyroflow.xyz/
- Inertial navigation
- Sensor fusion / Kalman filtering / Data assimilation
    - https://scipy-cookbook.readthedocs.io/items/KalmanFiltering.html
    - https://www.youtube.com/watch?v=TmBEryh2OXY
- GPS data logging for photo / video geolocation.
- Analyzing acceleration and vibration from personal transportation
    - https://github.com/zmsubin/accelerometers_pub

## Contribute
Please submit a PR if you have scripts or links that may be useful for other users. I will also feature any project that uses Sensor Logger, integrated as part of a larger workflow. 
