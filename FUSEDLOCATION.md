# Fused, GPS & Network Location

Your phone employs several methods to measure and report your location. The primary methods are:

- GPS, which depends on signals from a constellation of orbiting satellites to provide precise latitude and longitude coordinates.
- Utilizing information from nearby cellular network towers, which is less accurate than GPS but functional in areas with limited GPS signal or indoors.
- Other data sources such as WiFi.

By default, Sensor Logger reports fused location, a combination of GPS, cellular network-based data and other sources. It's important to note that this fusion is managed by the operating system, not Sensor Logger itself. While this fusion algorithm generally produces accurate results, there may be instances where it doesn't make the correct decision or where you prefer to analyze location data from one specific source.

In the Android version of Sensor Logger, you have the option to enable additional location data before fusion alongside the fused location. To do this, simply tap the settings icon located next to the "Start Recording" button and navigate to "Recording & Workflow." From there, you can toggle on "Additional Location Data." Enabling this option results in the creation of two additional CSV files, one for GPS-only location and another for network-only location.

To illustrate the distinction between fused, network-only, and GPS-only location data, consider the sample data collected using Sensor Logger on a roller coaster at Dreamland Margate:

<img width="673" alt="Screenshot 2023-11-06 at 22 23 10" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/b7bf86d3-0df5-45a7-b6d2-9bb92444339f">

Examining the satellite coaster track, you can observe how the fusion product combines both GPS and network data. However, since the network-based location is of lower quality, it introduces a slight bias to the fused location. In situations like this, it may be more prudent to rely solely on the GPS location.

Conversely, in another plot of the same data, you'll notice that the network-based location is more consistently available, particularly at the beginning of the recording. This is especially noticeable in the covered, semi-indoor loading station of the roller coaster, where the GPS signal was weak. Depending on whether you prioritize availability or accuracy for your specific use case, Sensor Logger offers the flexibility to choose between one or the other.

<img width="1071" alt="network_vs_gps_availability" src="https://github.com/tszheichoi/awesome-sensor-logger/assets/30114997/611f810a-3474-4af6-b1b2-994285edf617">

