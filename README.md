# Awesome Sensor Logger
This repository contains a collection of tools, resources and sample code to use alongside the Sensor Logger app. Please submit a PR if you have scripts or links that you think may be useful for other users.

## The Sensor Logger App
Sensor Logger is a free, easy to use, cross-platform data logger that logs readings from common motion-related sensors on smartphones. Once completed, recordings can be exported as a zipped CSV file, JSON or be viewed within the app via interactive plots. The iOS version comes with a free companion watch app that allows you to log heart rate & wrist motion, and control recording sessions remotely from your wrist. Supported sensors and measurements include:

- Device Acceleration (Accelerometer; Raw & Calibrated)
- Gravity Vector (Accelerometer)
- Device Rotation Rate (Gyroscope; Raw & Calibrated)
- Device Orientation (Gyroscope)
- Magnetic Heading (Magnetometer; Raw & Calibrated)
- Barometric Altitude (Barometer)
- GPS Coordinate, Altitude, Speed & Heading
- Proximity Sensor (Android Only)
- Audio Recording (Microphone)
- Ambient Sound Level (Microphone)
- Heart Rate (via Companion Watch App)
- Wrist Motion (via Companion Watch App)
- Weather (via internet)
- Annotations (Timestamp and optional accompanying text comment)

Learn more at www.tszheichoi.com/sensorlogger. 

## Getting Started with Data Analysis
Measurements made using the Sensor Logger can be exported in either `.csv` or `.json` formats. For the purpose of data analysis, the former is recommended. See www.tszheichoi.com/sensorloggerhelp for more about how the exporting works.

### Recommended Tools
Python is recommended for analysing the outputs from Sensor Logger. For interactive data exploration and visualisation, do use Jupyter Notebooks, which you can run for free easily with tools like Google Colab or Deep Notes. Your typical data science Python packages apply:

- Pandas
- Numpy
- SciPy

### Understanding Timestamps
All exported data have synchrnoised time stamps, meaning they can be cross-referenced. However, they do not necessarily align due to varied sampling rates. 
- The `time` column is the UNIX epoch timestamp of the measurement as reported by the sensors in nanoseconds. You can use tools like https://www.epochconverter.com/ to readable timestamps. 
- tbc

### Accessing Recording Metadata
The `metadata.csv` file contains the following information
- version: The schema version of the exported data. This is different to the version of the app. When this version increments, it means you may have to update your data analysis script as things such as the column names, file names or data structure may have changed. 
- device name: The name of the device used for recording.
- recording time: The start time of the recording in UTC.
- platform: Either iOS or Android.

### Diagnosing Sampling Rates
tbc

### Plotting Data
tbc

### Mapping GPS Tracks
tbc

### 3D Trajectory Visualisation
tbc

### Basic Audio Analysis
tbc

### Aligning & Interpolating Measurements Across Sensors
tbc

### Cross Correlation & Dynamic Time Warping 
tbc

### Converting to GPX
Michael Haberler has helpfully put together a few command line tools to take the JSON exported from Sensor Logger and convert it to GPX formats: https://github.com/mhaberler/sensorlogger-util

### Track Simplification
You can use algorithms like Douglas-Peucker to simplify recorded GPS tracks to save storage space for long recordings. A Sensor Logger specific implementaion can be found here: https://github.com/mhaberler/sensorlogger-util/blob/master/simplify.py

## Use Case Specific Resources
Sensor Logger is being use for a lot of applications. Here are a few to get you started. Let me know if you want your's to be featured here.
- Hotair balloon tracking
- Flight data logging
- Roller coaster tracking
- Sports research
- Figure skating analysis
- Video stabilisation
- Inertial navigation
- Sensor fusion / Kalman filtering
