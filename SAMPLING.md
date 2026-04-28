# Sampling Reference

Sampling frequency and consistency of sensors vary from device to device, and from platform to platform. Even identical devices may log at variable rates, influenced by factors such as the device's condition, running apps, and specific settings like low power mode. This reference is based on sampling frequencies as reported by real Sensor Logger users across a diverse user base to offer a better understanding of sampling rates for common phone models in real-world conditions.

This information is especially useful for research groups or organizations looking to purchase devices for running Sensor Logger. With data on how different models perform in actual use, you can make more informed purchasing decisions to ensure you choose devices with the best sensor performance for your specific needs.

# Definitions

## Zero-Gap Sensors

In Sensor Logger, Zero-Gap Sensors are those which Sensor Logger can and will try to sample as frequently as possible, **without any gap between successive requests**. This means the **sampling rate will be up against the hardware and operating system limitations**.

- `Median Achievable Sampling (Hz)` is the median sampling frequency, in Hz, across the relevant Sensor Logger recording sessions.
- `Sampling Gap Variability (s)` is the median of the standard deviation of sampling gaps _within_ a recording session, across all relevant Sensor Logger recording sessions. Lower values indicate more consistent timing between samples.

Zero-Gap Sensors include: _location, barometer, accelerometer, gravity, gyroscope, magnetometer, orientation and light_.

While a higher sampling rate and lower variability are generally considered better, it's important to remember that a high sampling rate doesn't always equate to more accurate data. In some cases, it can introduce more noise. Additionally, some devices might report at a lower effective sampling rate due to built-in signal processing from the operating system, which can actually improve accuracy. Therefore, it's crucial to consider both the sampling rate and the quality of the signal processing when evaluating devices.

## Other Sensors

For other sensors, Sensor Logger has built in delays between successive requests. These sensors are excluded.

# Results

To lookup iPhone model names, you may use https://reincubate.com/lookup/. For Android, you may consider using [https://www.gsmarena.com/](https://www.gsmarena.com/).

_Last Updated in April 2026._

### Location

| Device Model            | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| ----------------------- | ------------------------------- | ---------------------------- |
| iPhone14,5              | 0.99                            | 0.26961                      |
| iPhone13,2              | 0.97                            | 0.44593                      |
| iPhone15,4              | 0.97                            | 0.58127                      |
| iPhone14,7              | 0.97                            | 0.54311                      |
| iPhone16,1              | 0.95                            | 0.75412                      |
| iPhone12,1              | 0.96                            | 0.75730                      |
| iPhone14,2              | 0.99                            | 0.33685                      |
| iPhone14,6              | 0.98                            | 0.49003                      |
| iPhone16,2              | 0.97                            | 0.38318                      |
| iPhone15,2              | 0.95                            | 0.65537                      |
| iPhone17,1              | 0.96                            | 0.59775                      |
| iPhone13,3              | 0.95                            | 0.83131                      |
| SM-A136U                | 1.03                            | 0.32843                      |
| iPhone11,8              | 0.84                            | 1.65634                      |
| iPhone17,3              | 0.97                            | 0.58262                      |
| iPhone17,2              | 0.98                            | 0.37908                      |
| iPhone12,8              | 0.92                            | 0.90081                      |
| iPhone14,4              | 0.99                            | 0.30282                      |
| SM-A546B                | 1.07                            | 0.29559                      |
| iPhone14,3              | 0.98                            | 0.36127                      |
| iPhone13,1              | 0.98                            | 0.35647                      |
| iPhone15,3              | 0.98                            | 0.41496                      |
| SM-S911B                | 1.01                            | 0.33210                      |
| iPhone17,5              | 0.95                            | 1.14716                      |
| SM-A528B                | 1.00                            | 0.19249                      |
| iPhone14,8              | 0.96                            | 0.51969                      |
| SM-A315G                | 1.09                            | 0.24474                      |
| iPhone13,4              | 0.97                            | 0.64848                      |
| iPhone18,1              | 0.96                            | 0.52663                      |
| SM-A146U                | 1.16                            | 0.28270                      |
| iPhone11,2              | 0.91                            | 1.16087                      |
| Pixel 8                 | 1.11                            | 0.29369                      |
| Pixel 8 Pro             | 1.08                            | 0.25092                      |
| Pixel 7                 | 1.14                            | 0.29335                      |
| SM-G991B                | 0.90                            | 0.84462                      |
| iPhone12,3              | 0.99                            | 0.26159                      |
| SM-S918B                | 1.01                            | 0.24952                      |
| iPhone18,2              | 1.00                            | 0.18357                      |
| SM-A556E                | 1.10                            | 0.28636                      |
| SM-S928B                | 1.00                            | 0.26249                      |
| Pixel 6a                | 1.13                            | 0.32131                      |
| M2105K81C               | 1.00                            | 0.20584                      |
| SM-S921B                | 0.99                            | 0.55404                      |
| Pixel 5                 | 1.01                            | 0.20360                      |
| iPhone15,5              | 0.98                            | 0.35847                      |
| iPhone9,3               | 0.76                            | 1.88077                      |
| Pixel 9                 | 1.14                            | 0.29053                      |
| Pixel 7 Pro             | 1.03                            | 0.28398                      |
| iPhone12,5              | 0.95                            | 0.54853                      |
| SM-S901B                | 1.00                            | 0.30836                      |
| iPhone18,3              | 0.98                            | 0.38205                      |
| SM-S931B                | 1.04                            | 0.25004                      |
| Pixel 7a                | 1.00                            | 0.29286                      |
| SM-S928U1               | 1.01                            | 0.18086                      |
| Pixel 6                 | 1.16                            | 0.28496                      |
| SM-S901U                | 1.00                            | 0.08739                      |
| iPhone10,1              | 0.67                            | 2.49638                      |
| 2209116AG               | 1.00                            | 0.01952                      |
| Pixel 9 Pro             | 1.06                            | 0.28249                      |
| SM-A515F                | 1.00                            | 0.17760                      |
| SM-S928N                | 1.00                            | 0.09355                      |
| iPhone10,4              | 0.98                            | 0.44115                      |
| SM-G780G                | 1.06                            | 0.24089                      |
| motorola edge 50 neo    | 1.05                            | 0.30417                      |
| SM-S721B                | 1.02                            | 0.23758                      |
| SM-A556B                | 1.07                            | 0.31280                      |
| 2311DRN14I              | 1.01                            | 0.54994                      |
| SM-G998B                | 1.09                            | 0.75675                      |
| SM-A536B                | 1.02                            | 0.26277                      |
| SM-S926B                | 0.92                            | 0.61989                      |
| SM-S928W                | 1.02                            | 0.24403                      |
| Pixel 8a                | 1.08                            | 0.33364                      |
| moto g24                | 1.13                            | 0.44992                      |
| iPhone18,4              | 1.01                            | 0.28154                      |
| moto g53 5G             | 0.97                            | 0.34865                      |
| Pixel 6 Pro             | 1.07                            | 0.26988                      |
| Redmi Note 8 Pro        | 1.06                            | 0.23777                      |
| SM-S911U                | 1.01                            | 0.24496                      |
| SM-S908B                | 1.09                            | 0.31328                      |
| SM-S916B                | 1.01                            | 0.16926                      |
| T602DL                  | 1.00                            | 0.04705                      |
| XQ-CT72                 | 2.15                            | 0.28955                      |
| SM-A525F                | 1.01                            | 0.16357                      |
| SM-S711B                | 1.00                            | 0.42275                      |
| M2010J19CG              | 1.00                            | 0.22645                      |
| SM-A145R                | 1.00                            | 0.09629                      |
| Redmi Note 9 Pro        | 1.01                            | 0.08839                      |
| SM-A546E                | 1.06                            | 0.27779                      |
| Pixel 9 Pro XL          | 1.13                            | 0.31318                      |
| SM-S931N                | 1.00                            | 0.33291                      |
| 23124RA7EO              | 1.03                            | 0.14336                      |
| moto g stylus 5G - 2023 | 1.00                            | 0.07732                      |
| SM-M336B                | 13.36                           | 0.07490                      |
| SM-A156E                | 0.98                            | 0.66055                      |
| SM-G950F                | 1.17                            | 0.50984                      |
| 2109119DG               | 1.65                            | 0.25714                      |
| A063                    | 1.00                            | 0.08888                      |
| SM-G973F                | 1.09                            | 0.19761                      |
| SM-S938B                | 1.00                            | 0.31253                      |
| iPhone9,4               | 0.88                            | 1.17862                      |
| 2412DPC0AG              | 1.04                            | 0.17570                      |
| A142                    | 1.27                            | 0.33815                      |
| SM-A125F                | 0.18                            | 0.24615                      |
| 23078RKD5C              | 1.98                            | 0.33362                      |
| SM-S908N                | 2.82                            | 0.20202                      |
| 23108RN04Y              | 1.00                            | 0.06765                      |
| SC-51A                  | 0.20                            | 0.37928                      |
| SM-M625F                | 1.23                            | 0.57638                      |
| M2101K6G                | 1.02                            | 0.25137                      |
| 2312DRA50G              | 1.02                            | 0.07720                      |
| SM-G996B                | 1.02                            | 0.27859                      |
| SM-A236B                | 1.08                            | 0.28192                      |
| iPhone8,1               | 0.98                            | 0.29931                      |
| SM-A325F                | 0.73                            | 1.01312                      |
| iPad13,10               | 1.00                            | 0.13967                      |
| SM-S906U                | 1.03                            | 0.11814                      |
| SM-S9260                | 2.30                            | 0.25396                      |
| iPhone17,4              | 0.92                            | 1.31093                      |
| SM-A226B                | 1.15                            | 0.27876                      |
| SM-S921N                | 1.01                            | 0.20936                      |
| SM-F966Q                | 1.03                            | 0.10846                      |
| SM-S901E                | 1.05                            | 0.28694                      |
| SM-A526B                | 1.00                            | 0.03874                      |
| 23122PCD1G              | 1.00                            | 0.04844                      |
| iPhone10,3              | 0.81                            | 3.34468                      |
| SM-G990B2               | 0.98                            | 0.64470                      |
| SM-G781B                | 1.00                            | 0.26298                      |
| moto g 5G - 2024        | 1.02                            | 0.27643                      |
| iPhone10,6              | 0.90                            | 0.90726                      |
| DNY-NX9                 | 1.02                            | 0.12794                      |
| SM-A156U                | 1.03                            | 0.16567                      |
| Pixel 9a                | 1.01                            | 0.26900                      |
| Pixel 4a                | 0.99                            | 0.30089                      |
| V2338                   | 1.55                            | 0.19488                      |
| moto g54 5G             | 1.17                            | 0.29649                      |
| SM-A266M                | 1.02                            | 0.78877                      |
| SM-G998U                | 1.01                            | 0.00908                      |
| Infinix X6882           | 1.04                            | 0.17904                      |
| Infinix X6833B          | 1.04                            | 0.15994                      |
| iPad8,9                 | 0.08                            | 4.57457                      |
| Redmi Note 9S           | 1.00                            | 0.59868                      |
| FP3                     | 1.26                            | 0.67689                      |
| V2055A                  | 2.62                            | 0.24022                      |
| SM-A155F                | 0.99                            | 0.38717                      |
| SM-A356E                | 1.00                            | 0.81952                      |
| SM-G990B                | 1.10                            | 0.20104                      |
| SM-A536E                | 1.04                            | 0.18436                      |
| KB2005                  | 1.00                            | 0.06506                      |
| 2201117TY               | 1.01                            | 0.19762                      |
| RMX3231                 | 0.99                            | 0.49749                      |
| 2312DRAABC              | 0.91                            | 1.28070                      |
| SM-S908E                | 1.03                            | 0.14190                      |
| Infinix X6815B          | 0.64                            | 0.60727                      |
| 22041211AC              | 2.24                            | 0.27356                      |
| AC2003                  | 1.37                            | 0.34580                      |
| SM-F946B                | 1.02                            | 0.13485                      |
| moto g86 power 5G       | 1.01                            | 0.07716                      |
| moto g86 5G             | 1.00                            | 0.03031                      |
| 2201116PG               | 0.95                            | 0.75733                      |
| Infinix X6831           | 1.00                            | 0.37512                      |
| SM-S938U                | 1.02                            | 0.10062                      |
| SM-S926N                | 1.63                            | 0.30644                      |
| SM-A336B                | 1.18                            | 0.40219                      |
| 2311DRK48G              | 1.10                            | 0.25893                      |
| moto g84 5G             | 1.14                            | 0.34232                      |
| iPhone10,2              | 0.98                            | 0.57604                      |
| SM-A405FN               | 1.09                            | 0.21498                      |
| SM-S918N                | 1.01                            | 0.07212                      |
| SM-S916U                | 1.01                            | 0.27968                      |
| 2201116SG               | 1.02                            | 0.38030                      |
| SM-A346B                | 1.14                            | 0.44778                      |
| H1715V                  | 1.00                            | 0.09811                      |
| Infinix X6837           | 1.03                            | 0.13139                      |
| SM-S928U                | 1.01                            | 0.13589                      |
| Pixel 10 Pro            | 2.29                            | 0.26067                      |
| 24094RAD4G              | 1.08                            | 0.20196                      |
| SM-A266B                | 1.05                            | 0.32163                      |
| ASUS_AI2202             | 1.01                            | 0.16307                      |
| Pixel 2                 | 1.52                            | 0.83336                      |
| CPH2743                 | 1.00                            | 0.06777                      |
| Pixel 3                 | 1.01                            | 0.11837                      |
| RMX3710                 | 1.35                            | 0.34512                      |
| SM-S908U                | 1.05                            | 0.22048                      |
| SM-A235F                | 1.09                            | 0.28772                      |
| M2007J17I               | 0.98                            | 0.42083                      |
| SM-S911U1               | 1.00                            | 0.10333                      |
| SM-F946U1               | 0.60                            | 0.35261                      |
| BKL-L09                 | 0.94                            | 0.83118                      |
| 9137W                   | 1.00                            | 0.08941                      |
| RMX1821                 | 1.00                            | 0.25557                      |
| iPad16,2                | 0.96                            | 0.80734                      |
| SM-S921U                | 1.01                            | 0.15196                      |
| 25042PN24C              | 1.09                            | 0.28584                      |
| SM-X218U                | 1.01                            | 0.13278                      |
| SM-A5360                | 1.03                            | 0.40655                      |
| SM-S938U1               | 1.01                            | 0.07772                      |
| ELE-AL00                | 1.62                            | 0.27489                      |
| SM-G996U1               | 1.09                            | 0.29378                      |
| SM-G996U                | 1.00                            | 0.03642                      |
| SM-A155M                | 1.00                            | 0.16990                      |
| SM-A566E                | 0.42                            | 3.18380                      |
| moto g play - 2024      | 1.00                            | 0.05931                      |
| SM-A146P                | 0.56                            | 9.90665                      |
| 2107113SG               | 1.05                            | 0.16493                      |
| iPhone11,6              | 0.98                            | 0.55726                      |
| SM-G990E                | 1.17                            | 0.58794                      |
| SM-G991U1               | 1.20                            | 0.34181                      |
| iPad13,19               | 1.00                            | 0.01212                      |
| SM-A137F                | 0.11                            | 4.57848                      |
| SM-A505FN               | 0.21                            | 2.75468                      |
| moto g power 5G - 2023  | 1.15                            | 0.26133                      |
| SOG01                   | 1.00                            | 0.11913                      |
| moto g stylus 5G        | 1.01                            | 0.04349                      |
| CPH2059                 | 1.01                            | 0.05978                      |
| DN2101                  | 1.03                            | 0.13225                      |
| SM-N975F                | 1.05                            | 0.18931                      |
| SM-J510FN               | 1.00                            | 0.02303                      |
| CPH2707                 | 1.36                            | 0.34198                      |
| SM-S906E                | 0.17                            | 1.15775                      |
| moto g35 5G             | 0.99                            | 0.24265                      |
| SM-X826B                | 1.01                            | 0.31841                      |
| 21081111RG              | 1.50                            | 0.33155                      |
| Infinix X6853           | 1.07                            | 0.19917                      |
| I2214                   | 1.04                            | 0.19295                      |
| SM-G970F                | 1.03                            | 0.68770                      |
| SM-A146B                | 2.32                            | 0.22715                      |
| RMX3392                 | 1.03                            | 0.30657                      |
| 23049PCD8G              | 1.03                            | 0.12656                      |
| ASUS_I006D              | 2.19                            | 0.31478                      |
| SM-S938N                | 1.10                            | 0.22428                      |
| SM-S901U1               | 0.65                            | 1.63590                      |
| V2428                   | 1.01                            | 0.09474                      |
| moto g72                | 2.44                            | 0.31656                      |
| Mi 9 Lite               | 1.00                            | 0.18200                      |
| Armor Pad               | 1.00                            | 0.01555                      |
| moto g pure             | 0.97                            | 0.50619                      |
| M2101K7BNY              | 1.00                            | 0.14280                      |
| M2012K11AG              | 1.05                            | 0.17233                      |
| moto g42                | 1.01                            | 0.13691                      |
| SM-G965F                | 1.17                            | 0.27680                      |
| Nokia X20               | 1.01                            | 0.05142                      |
| SM-A3560                | 1.09                            | 0.27109                      |
| CPH2629                 | 0.19                            | 4.74966                      |
| 24090RA29G              | 1.05                            | 0.16974                      |
| iPad13,17               | 0.85                            | 1.73762                      |
| VOG-L29                 | 0.97                            | 0.37838                      |
| SM-S908U1               | 1.01                            | 0.08230                      |
| motorola edge 50 fusion | 2.13                            | 0.23512                      |
| SM-S936U                | 1.00                            | 0.31869                      |
| SM-M515F                | 1.01                            | 0.01168                      |
| 22101316I               | 1.17                            | 0.28981                      |
| V2324A                  | 2.19                            | 0.27127                      |
| CPH2493                 | 1.19                            | 0.80072                      |
| SM-A127F                | 1.00                            | 0.13546                      |
| SM-A035M                | 0.96                            | 0.49246                      |
| 21091116UG              | 0.53                            | 0.89981                      |
| SM-S918U                | 1.01                            | 0.09601                      |
| iPad11,1                | 0.09                            | 8.11642                      |
| SM-G781W                | 1.01                            | 0.06658                      |
| TECNO CK7n              | 1.02                            | 0.11289                      |
| FP4                     | 1.17                            | 0.23243                      |
| IN2023                  | 0.88                            | 0.79091                      |
| A015                    | 1.39                            | 0.35813                      |
| I2410                   | 2.31                            | 0.26925                      |
| SM-G975F                | 0.99                            | 0.89296                      |
| moto g play - 2023      | 1.02                            | 0.16309                      |
| XQ-BT52                 | 1.00                            | 0.04997                      |
| SM-M315F                | 1.06                            | 0.16211                      |
| KB2003                  | 1.00                            | 0.17572                      |
| iPhone9,1               | 0.62                            | 1.78922                      |
| SM-G991U                | 1.01                            | 0.34492                      |
| iPad16,4                | 0.99                            | 0.19902                      |
| CPH2729                 | 0.89                            | 0.72961                      |
| 22101316G               | 1.01                            | 0.56324                      |
| SM-S921W                | 1.00                            | 0.28067                      |
| SM-S916N                | 1.00                            | 0.32740                      |
| SM-G556B                | 1.01                            | 0.12565                      |
| moto g stylus 5G - 2024 | 1.00                            | 0.13665                      |
| SM-G973U1               | 1.17                            | 0.45262                      |
| SM-A205GN               | 1.02                            | 0.13602                      |
| Helium Pro              | 1.00                            | 0.60726                      |
| iPad14,10               | 0.07                            | 4.71694                      |
| CPH2491                 | 1.05                            | 0.17517                      |
| SM-G980F                | 1.05                            | 0.39314                      |
| motorola edge 40 neo    | 1.06                            | 0.20327                      |
| TC27                    | 1.86                            | 0.35134                      |
| A059                    | 1.01                            | 0.16557                      |
| SM-A245F                | 1.07                            | 0.22951                      |
| RMX3760                 | 1.01                            | 0.09106                      |
| SM-A166P                | 0.90                            | 1.21485                      |
| V2417                   | 1.06                            | 0.40020                      |
| Pixel 10 Pro XL         | 1.11                            | 0.32574                      |
| SM-M127F                | 0.99                            | 0.21176                      |
| moto g - 2025           | 1.09                            | 0.28573                      |
| CPH2653                 | 1.10                            | 0.20465                      |
| SM-S937B                | 0.99                            | 0.19570                      |
| SM-N960F                | 1.05                            | 0.21362                      |
| B160V                   | 1.02                            | 0.09644                      |
| SM-A217F                | 2.00                            | 0.30420                      |
| motorola edge 60 fusion | 1.01                            | 0.17891                      |
| V2284A                  | 1.62                            | 0.52131                      |
| INE-LX2                 | 1.00                            | 0.18216                      |
| SM-G770F                | 1.22                            | 0.31966                      |
| 24069PC21G              | 1.01                            | 0.14587                      |
| MIS-LX9                 | 0.98                            | 0.44662                      |
| SM-M146B                | 1.08                            | 0.21921                      |
| SM-S918U1               | 1.26                            | 0.41183                      |
| moto g34 5G             | 1.11                            | 0.34065                      |
| RMX3785                 | 1.82                            | 0.40801                      |
| 23090RA98G              | 1.22                            | 0.28884                      |
| SM-X210                 | 1.01                            | 0.01385                      |
| SM-A505W                | 0.84                            | 7.04446                      |
| 23030RAC7Y              | 1.34                            | 0.34782                      |
| SM-A366B                | 1.00                            | 0.09801                      |
| V2029                   | 1.00                            | 0.08551                      |
| iPad15,8                | 0.98                            | 0.51762                      |
| FP5                     | 3.88                            | 0.25675                      |
| XQ-ES54                 | 1.14                            | 0.40081                      |
| 2304FPN6DC              | 0.93                            | 0.62866                      |
| CPH2585                 | 1.70                            | 0.22409                      |
| M2101K9G                | 1.00                            | 0.07283                      |
| SM-A507FN               | 1.42                            | 0.40482                      |
| 220333QAG               | 1.00                            | 0.15807                      |
| 23129RN51X              | 1.00                            | 0.58594                      |
| 2312DRAABG              | 1.05                            | 0.19124                      |
| iPhone8,4               | 0.88                            | 1.36952                      |
| XQ-DC54                 | 0.99                            | 0.39949                      |
| SM-F731U                | 0.90                            | 0.71683                      |
| SM-A256B                | 1.41                            | 0.33385                      |
| moto g51 5G             | 1.03                            | 0.15923                      |
| RMX3997                 | 1.12                            | 0.32369                      |
| Pixel 5a                | 1.04                            | 0.88638                      |
| SM-N950F                | 0.20                            | 1.29003                      |
| SM-A356B                | 1.06                            | 0.24334                      |
| RMX3363                 | 1.01                            | 0.04149                      |
| SM-S936N                | 0.97                            | 0.46559                      |
| TMRV07P5G               | 1.00                            | 0.05022                      |
| 23021RAAEG              | 0.89                            | 0.74052                      |
| CPH2551                 | 1.00                            | 0.09460                      |
| SM-A546U                | 1.09                            | 0.17925                      |
| M2007J17G               | 2.27                            | 0.28349                      |
| H1702V                  | 1.00                            | 0.14717                      |
| SM-A107F                | 1.01                            | 0.16036                      |
| Nokia G22               | 0.83                            | 0.48170                      |
| SM-A736B                | 1.30                            | 0.29538                      |
| moto g(20)              | 0.93                            | 0.56242                      |
| SM-F936U                | 1.03                            | 0.10966                      |
| M2102J20SG              | 1.43                            | 0.27095                      |
| 21061119AL              | 1.00                            | 0.05245                      |
| Action-X3               | 1.00                            | 0.05561                      |
| SM-G988B                | 1.01                            | 0.19576                      |
| SM-S9110                | 1.00                            | 0.06939                      |
| SM-G930F                | 1.08                            | 0.30895                      |
| iPhone10,5              | 0.98                            | 0.34348                      |
| LGE-AN00                | 1.01                            | 0.05290                      |
| moto g41                | 1.17                            | 0.24008                      |
| SM-A546S                | 0.68                            | 0.35172                      |
| PTP-N49                 | 1.17                            | 0.26682                      |
| M2004J19C               | 1.00                            | 0.28653                      |
| RMX3092                 | 1.02                            | 0.06125                      |
| 24117RN76G              | 0.94                            | 1.30326                      |
| 25113PN0EI              | 1.01                            | 0.09791                      |
| 2406ERN9CI              | 1.04                            | 0.20996                      |
| SM-G960F                | 0.21                            | 0.59369                      |
| 25113PN0EC              | 1.81                            | 0.30887                      |
| SM-A715F                | 1.01                            | 0.59225                      |
| SM-A045F                | 0.21                            | 3.70548                      |
| CPH2613                 | 1.00                            | 0.04656                      |
| motorola edge 40 pro    | 1.06                            | 0.19402                      |
| M2103K19G               | 1.01                            | 0.13369                      |
| iPad15,7                | 0.19                            | 3.90835                      |
| RMX3312                 | 2.34                            | 0.46329                      |
| SM-M356B                | 1.02                            | 0.68116                      |
| SM-A165F                | 0.98                            | 0.29767                      |
| M2101K7BI               | 1.07                            | 0.28816                      |
| SM-A075F                | 0.93                            | 0.60660                      |
| Infinix X655C           | 0.92                            | 3.33921                      |
| BRP-NX3                 | 1.02                            | 0.11587                      |
| SM-F721N                | 0.30                            | 1.65482                      |
| CPH1931                 | 1.02                            | 0.29654                      |
| 22101316UG              | 1.02                            | 0.51791                      |
| moto g 5G plus          | 1.00                            | 0.03672                      |
| motorola edge 60 pro    | 1.00                            | 0.06371                      |
| motorola edge 2024      | 1.04                            | 0.16670                      |
| SM-A135F                | 1.00                            | 0.01999                      |
| PJX110                  | 0.67                            | 2.01898                      |
| 2201117SG               | 1.03                            | 0.13577                      |
| ELI-NX9                 | 1.01                            | 0.20608                      |
| 2306EPN60G              | 1.95                            | 0.19665                      |
| SM-S156V                | 1.18                            | 0.27545                      |
| CPH2487                 | 1.02                            | 0.10671                      |
| Redmi Note 7            | 1.02                            | 0.07180                      |
| I2219                   | 1.04                            | 0.32172                      |
| CPH2591                 | 1.23                            | 0.35125                      |
| 23128PC33I              | 0.77                            | 1.06639                      |
| V2312                   | 0.24                            | 3.98688                      |
| SM-S906B                | 0.97                            | 0.26001                      |
| iPad13,16               | 0.07                            | 17.97463                     |
| LLY-NX1                 | 1.01                            | 0.27864                      |
| SM-A225F                | 1.09                            | 0.23009                      |
| motorola edge 50        | 1.06                            | 0.17852                      |
| SM-S711U                | 1.02                            | 0.06991                      |
| 23053RN02Y              | 1.18                            | 0.67156                      |
| 25028RN03A              | 0.99                            | 0.85230                      |
| SM-S938Q                | 1.01                            | 0.31330                      |
| V2303                   | 0.38                            | 2.15286                      |
| 23116PN5BC              | 1.00                            | 0.02627                      |
| SM-N9750                | 2.31                            | 0.22647                      |
| SM-G781U                | 1.00                            | 0.06655                      |
| SM-A166U                | 1.05                            | 0.30881                      |
| 24031PN0DC              | 1.89                            | 0.37713                      |
| iPad14,2                | 0.80                            | 2.45430                      |
| SM-A057F                | 1.00                            | 0.15233                      |
| SM-A256E                | 2.25                            | 0.30058                      |
| SM-M346B                | 0.93                            | 1.08379                      |
| I2218                   | 1.00                            | 0.05320                      |
| SM-F956B                | 1.01                            | 0.08607                      |
| moto g stylus (2023)    | 1.17                            | 0.28349                      |
| 22071212AG              | 1.02                            | 0.07789                      |
| LYA-L29                 | 1.30                            | 0.58017                      |
| vivo 1802               | 0.15                            | 14.38543                     |
| 23106RN0DA              | 1.01                            | 0.09936                      |
| SM-G998N                | 1.07                            | 0.67378                      |
| Mi 9T Pro               | 1.02                            | 0.08502                      |
| 22101320G               | 1.02                            | 0.58017                      |
| Z2453                   | 0.53                            | 0.98068                      |
| SM-S711N                | 0.82                            | 0.97496                      |
| moto g04s               | 0.75                            | 1.90331                      |
| ONEPLUS A5010           | 1.02                            | 0.35617                      |
| SM-F936U1               | 1.00                            | 0.03287                      |
| ELE-L29                 | 1.03                            | 0.13953                      |
| SM-A065M                | 1.01                            | 0.05233                      |
| 901SO                   | 1.01                            | 0.02316                      |
| SM-M536B                | 0.36                            | 2.21484                      |
| CPH1803                 | 0.35                            | 3.49634                      |
| V2339A                  | 2.48                            | 0.20489                      |
| 2201123G                | 2.50                            | 0.28111                      |
| SM-X800                 | 1.00                            | 0.12963                      |
| SM-A047F                | 1.01                            | 0.18870                      |
| SM-G986B                | 1.03                            | 0.13144                      |
| SM-A037F                | 1.02                            | 0.19688                      |
| SM-S918W                | 1.00                            | 0.04423                      |
| LE2101                  | 2.41                            | 0.29000                      |
| SM-S906N                | 1.33                            | 0.46497                      |
| SM-F731U1               | 2.15                            | 0.60507                      |
| SM-G780F                | 1.00                            | 0.06580                      |
| M2007J20CG              | 1.01                            | 0.25496                      |
| MAR-LX3A                | 0.12                            | 13.78003                     |
| CPH2387                 | 1.08                            | 0.22207                      |
| POCOPHONE F1            | 1.00                            | 0.33434                      |
| SM-A325N                | 2.65                            | 0.23877                      |
| SM-G981U1               | 0.10                            | 77.30027                     |
| SM-A415F                | 1.27                            | 0.41562                      |
| RMX2170                 | 1.05                            | 0.17885                      |
| moto e                  | 1.01                            | 0.76745                      |
| SM-A145F                | 1.00                            | 0.13251                      |
| H8314                   | 1.22                            | 0.28679                      |
| SM-G965N                | 1.02                            | 0.11897                      |
| RMX3151                 | 1.02                            | 0.15150                      |
| M2003J15SC              | 1.02                            | 0.13066                      |
| moto g14                | 0.93                            | 0.65002                      |
| SM-G981B                | 1.20                            | 0.33433                      |
| SM-M526BR               | 0.98                            | 0.29936                      |
| SM-E546B                | 2.03                            | 0.31266                      |
| SM-G973C                | 1.11                            | 0.19738                      |
| SM-G986N                | 1.29                            | 1.11978                      |
| itel S665L              | 0.20                            | 0.25191                      |
| W55Y                    | 0.19                            | 1.64934                      |

### Barometer

| Device Model            | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| ----------------------- | ------------------------------- | ---------------------------- |
| iPhone14,5              | 0.94                            | 0.02772                      |
| iPhone13,2              | 0.94                            | 0.02777                      |
| iPhone12,1              | 1.00                            | 0.01731                      |
| iPhone14,6              | 1.06                            | 0.02568                      |
| iPhone16,1              | 0.94                            | 0.04934                      |
| iPhone17,1              | 0.94                            | 0.04442                      |
| iPhone15,4              | 0.94                            | 0.06002                      |
| iPhone14,7              | 0.94                            | 0.04125                      |
| iPhone16,2              | 0.94                            | 0.04334                      |
| iPhone14,2              | 0.94                            | 0.02949                      |
| iPhone15,2              | 0.94                            | 0.03367                      |
| SM-A136U                | 6.26                            | 0.00018                      |
| iPhone14,4              | 0.94                            | 0.03122                      |
| iPhone17,3              | 0.94                            | 0.03696                      |
| iPhone17,2              | 0.94                            | 0.04692                      |
| SM-A146U                | 10.01                           | 0.00046                      |
| iPhone13,1              | 0.94                            | 0.03392                      |
| iPhone13,3              | 0.94                            | 0.03245                      |
| iPhone12,8              | 1.00                            | 0.01445                      |
| SM-S928B                | 25.03                           | 0.00004                      |
| iPhone13,4              | 0.94                            | 0.02745                      |
| iPhone15,3              | 0.94                            | 0.04079                      |
| iPhone14,3              | 0.94                            | 0.03969                      |
| SM-S911B                | 25.03                           | 0.00004                      |
| Pixel 8                 | 39.85                           | 0.00003                      |
| Pixel 6a                | 50.05                           | 0.00027                      |
| iPhone11,8              | 1.05                            | 0.02695                      |
| Pixel 7                 | 39.89                           | 0.00003                      |
| SM-S938B                | 15.64                           | 0.00006                      |
| iPhone14,8              | 0.94                            | 0.05157                      |
| Pixel 8 Pro             | 39.83                           | 0.00003                      |
| iPhone10,1              | 1.06                            | 0.05286                      |
| Pixel 8a                | 39.88                           | 0.00003                      |
| SM-S921B                | 12.51                           | 0.00009                      |
| iPhone18,1              | 0.95                            | 0.03298                      |
| Pixel 5                 | 25.03                           | 0.00004                      |
| Pixel 9                 | 39.88                           | 0.00003                      |
| iPhone12,3              | 1.00                            | 0.02285                      |
| SM-G991B                | 10.01                           | 0.00014                      |
| SM-S918B                | 25.03                           | 0.00004                      |
| iPhone11,2              | 1.00                            | 0.02120                      |
| Pixel 4                 | 25.03                           | 0.00004                      |
| iPhone12,5              | 1.00                            | 0.02428                      |
| Pixel 7 Pro             | 39.87                           | 0.00003                      |
| iPhone18,2              | 0.95                            | 0.02728                      |
| Pixel 7a                | 39.96                           | 0.00003                      |
| SM-S931B                | 15.64                           | 0.00006                      |
| iPhone9,3               | 1.06                            | 0.02613                      |
| Pixel 6                 | 50.05                           | 0.00029                      |
| Pixel 4a                | 25.03                           | 0.00004                      |
| SM-S901B                | 10.01                           | 0.00012                      |
| iPhone18,3              | 0.94                            | 0.04558                      |
| SM-S926B                | 12.49                           | 0.00012                      |
| SM-S928N                | 25.03                           | 0.00004                      |
| SM-S908B                | 10.00                           | 0.00019                      |
| SM-S916B                | 25.03                           | 0.00004                      |
| SM-G998B                | 10.01                           | 0.00014                      |
| SM-G977U                | 25.03                           | 0.00004                      |
| SM-S911U                | 25.03                           | 0.00004                      |
| SM-S928W                | 25.03                           | 0.00004                      |
| iPhone15,5              | 0.94                            | 0.04658                      |
| Pixel 9 Pro             | 39.85                           | 0.00003                      |
| iPhone17,5              | 0.94                            | 0.04759                      |
| SM-S901U                | 25.03                           | 0.00010                      |
| XQ-CT72                 | 25.03                           | 0.00010                      |
| SM-S931N                | 15.64                           | 0.00006                      |
| SM-S721B                | 12.52                           | 0.00011                      |
| iPhone10,6              | 1.06                            | 0.04107                      |
| SM-S921W                | 25.03                           | 0.00004                      |
| SM-G991U1               | 25.03                           | 0.00004                      |
| iPhone18,4              | 0.95                            | 0.02729                      |
| SM-S928U1               | 25.03                           | 0.00004                      |
| SM-G996U1               | 25.03                           | 0.00004                      |
| moto g 5G - 2024        | 25.03                           | 0.00004                      |
| SM-S901E                | 25.03                           | 0.00010                      |
| SM-S908U                | 25.03                           | 0.00010                      |
| SM-S938U1               | 15.64                           | 0.00006                      |
| moto g play - 2024      | 25.03                           | 0.00004                      |
| SM-S918U                | 25.03                           | 0.00005                      |
| SC-51A                  | 25.03                           | 0.00012                      |
| iPhone9,4               | 1.06                            | 0.04360                      |
| SM-G990B                | 25.03                           | 0.00004                      |
| SM-A156U                | 6.26                            | 0.00021                      |
| SM-S906U                | 25.03                           | 0.00009                      |
| SM-G973F                | 10.01                           | 0.00016                      |
| moto g - 2025           | 10.02                           | 0.00016                      |
| SM-G975U1               | 25.03                           | 0.00004                      |
| iPad13,10               | 1.03                            | 0.02041                      |
| SM-G996B                | 10.01                           | 0.00016                      |
| iPad11,1                | 1.07                            | 0.04220                      |
| SM-S928U                | 25.03                           | 0.00004                      |
| SM-G996U                | 25.03                           | 0.00004                      |
| SM-S9160                | 25.03                           | 0.00006                      |
| SM-G960F                | 10.01                           | 0.00011                      |
| SM-S9260                | 25.03                           | 0.00004                      |
| SM-G990B2               | 25.03                           | 0.00004                      |
| Pixel 9 Pro XL          | 39.83                           | 0.00003                      |
| SM-S916U                | 25.03                           | 0.00004                      |
| iPad8,9                 | 1.06                            | 0.02571                      |
| 25042PN24C              | 100.10                          | 0.00001                      |
| Pixel 3                 | 25.03                           | 0.00005                      |
| iPhone8,1               | 0.97                            | 0.04637                      |
| SM-S711B                | 12.52                           | 0.00009                      |
| Pixel 6 Pro             | 50.05                           | 0.00026                      |
| SM-S9060                | 25.03                           | 0.00017                      |
| SM-S938U                | 15.64                           | 0.00006                      |
| Pixel 2                 | 26.03                           | 0.00040                      |
| SM-G981U1               | 25.03                           | 0.00005                      |
| Pixel 5a                | 25.03                           | 0.00004                      |
| SM-S938N                | 15.64                           | 0.00006                      |
| moto g stylus 5G - 2024 | 25.03                           | 0.00004                      |
| iPhone10,3              | 1.05                            | 0.02946                      |
| moto g power 5G - 2023  | 10.01                           | 0.00010                      |
| SM-G950F                | 10.00                           | 0.00017                      |
| iPad6,11                | 1.06                            | 0.06078                      |
| moto g stylus 5G        | 25.03                           | 0.00004                      |
| iPhone10,2              | 1.06                            | 0.04852                      |
| T803H                   | 10.01                           | 0.00015                      |
| moto g stylus 5G - 2023 | 25.03                           | 0.00005                      |
| 2210132C                | 25.03                           | 0.00017                      |
| 2210132G                | 25.03                           | 0.00015                      |
| iPhone10,4              | 1.06                            | 0.02645                      |
| SM-G980F                | 10.01                           | 0.00016                      |
| SM-S911N                | 25.03                           | 0.00004                      |
| SM-S921U                | 25.03                           | 0.00004                      |
| SM-S166V                | 6.22                            | 0.00054                      |
| SM-S916N                | 25.03                           | 0.00004                      |
| SM-N960F                | 10.01                           | 0.00011                      |
| B160V                   | 10.01                           | 0.00045                      |
| SM-G990E                | 10.01                           | 0.00016                      |
| M2102K1G                | 25.03                           | 0.00004                      |
| SM-S156V                | 6.26                            | 0.00038                      |
| SM-G950U                | 30.04                           | 0.00003                      |
| moto g play - 2023      | 10.01                           | 0.00057                      |
| 23116PN5BC              | 25.03                           | 0.00004                      |
| SM-N9750                | 25.03                           | 0.00004                      |
| SM-G973U1               | 25.03                           | 0.00004                      |
| SM-G991U                | 25.03                           | 0.00004                      |
| moto g pure             | 10.01                           | 0.00037                      |
| G8441                   | 30.04                           | 0.00003                      |
| M2012K11C               | 25.03                           | 0.00004                      |
| SM-G986N                | 25.03                           | 0.00038                      |
| SM-S901U1               | 25.03                           | 0.00009                      |
| C6                      | 32.03                           | 0.00006                      |
| Pixel 10 Pro XL         | 25.07                           | 0.00004                      |
| SM-S937B                | 15.64                           | 0.00006                      |
| Pixel 9a                | 25.20                           | 0.00004                      |
| SM-S936U                | 15.64                           | 0.00006                      |
| SM-G986B                | 10.01                           | 0.00017                      |
| SM-S911U1               | 25.03                           | 0.00005                      |
| SM-G975F                | 10.01                           | 0.00014                      |
| SM-G998U                | 25.03                           | 0.00004                      |
| iPhone9,1               | 1.07                            | 0.10515                      |
| 2107113SG               | 25.03                           | 0.00004                      |
| iPad13,19               | 1.05                            | 0.02652                      |
| moto g power 5G - 2024  | 10.02                           | 0.00054                      |
| SM-N950F                | 10.01                           | 0.00023                      |
| SM-F946U1               | 25.03                           | 0.00005                      |
| SM-F936B                | 25.03                           | 0.00004                      |
| iPad13,1                | 1.07                            | 0.04773                      |
| 2410DPN6CC              | 25.02                           | 0.00011                      |
| SM-S9110                | 25.03                           | 0.00004                      |
| 24129PN74C              | 25.03                           | 0.00010                      |
| SM-G970F                | 10.01                           | 0.00021                      |
| SM-A166U                | 6.20                            | 0.00034                      |
| iPad16,1                | 1.06                            | 0.03896                      |
| iPad13,17               | 1.08                            | 0.09156                      |
| SM-F721N                | 25.03                           | 0.00008                      |
| iPhone17,4              | 0.95                            | 0.06874                      |
| CPH2647                 | 25.03                           | 0.00005                      |
| SM-N976U                | 25.03                           | 0.00004                      |
| SM-S926N                | 12.51                           | 0.00009                      |
| SM-F946B                | 25.03                           | 0.00005                      |
| SM-G985F                | 10.01                           | 0.00063                      |
| CPH2551                 | 25.03                           | 0.00005                      |
| iPad15,8                | 1.06                            | 0.05784                      |
| SM-G986U                | 25.03                           | 0.00076                      |
| SM-S146VL               | 10.02                           | 0.00045                      |
| N156DL                  | 10.02                           | 0.00024                      |
| SM-N975F                | 10.01                           | 0.00014                      |
| Android                 | 12.52                           | 0.00015                      |
| SM-F958N                | 15.63                           | 0.00089                      |
| 25113PN0EI              | 25.03                           | 0.00004                      |
| 25113PN0EC              | 25.03                           | 0.00004                      |
| SM-G973N                | 10.01                           | 0.00016                      |
| CPH2653                 | 25.03                           | 0.00004                      |
| iPad7,4                 | 1.06                            | 0.02576                      |
| SM-G960U                | 25.03                           | 0.00004                      |
| BLA-L09                 | 12.51                           | 0.00008                      |
| 23127PN0CC              | 25.03                           | 0.00004                      |
| SM-F741B                | 15.64                           | 0.00006                      |
| SM-S908N                | 25.03                           | 0.00008                      |
| SM-S931U                | 15.64                           | 0.00008                      |
| SM-S918U1               | 25.03                           | 0.00005                      |
| 2304FPN6DC              | 25.03                           | 0.00004                      |
| iPhone8,2               | 0.96                            | 0.01780                      |
| TMAF025G                | 10.01                           | 0.00041                      |
| 2509FPN0BC              | 1.37                            | 8.59690                      |
| SM-F956B                | 15.64                           | 0.00006                      |
| moto g stylus (2023)    | 10.01                           | 0.00022                      |
| LYA-L29                 | 12.51                           | 0.00008                      |
| iPad13,16               | 1.06                            | 0.02617                      |
| SM-S711N                | 12.49                           | 0.00009                      |
| SM-S9280                | 25.03                           | 0.00004                      |
| 21081111RG              | 10.01                           | 0.00010                      |
| 25098PN5AC              | 25.02                           | 0.00009                      |
| SM-F936U1               | 25.03                           | 0.00004                      |
| 901SO                   | 25.03                           | 0.00004                      |
| SM-S711U                | 15.64                           | 0.00021                      |
| XQ-BC42                 | 25.03                           | 0.00004                      |
| SM-S906N                | 25.03                           | 0.00010                      |
| SM-F731U1               | 25.03                           | 0.00008                      |
| SM-A546U                | 6.08                            | 0.00090                      |
| TC78                    | 25.03                           | 0.00004                      |
| M2012K11I               | 25.03                           | 0.00004                      |
| SM-F926U                | 25.03                           | 0.00004                      |
| SM-G965N                | 10.01                           | 0.00010                      |
| SM-G930F                | 10.00                           | 0.00017                      |
| SM-G981B                | 10.01                           | 0.00014                      |

### Accelerometer

| Device Model          | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| --------------------- | ------------------------------- | ---------------------------- |
| iPhone16,1            | 100.09                          | 0.00001                      |
| iPhone13,2            | 99.86                           | 0.00001                      |
| iPhone15,2            | 100.29                          | 0.00001                      |
| iPhone14,5            | 100.01                          | 0.00001                      |
| iPhone14,7            | 99.98                           | 0.00001                      |
| iPhone17,1            | 100.04                          | 0.00001                      |
| iPhone15,4            | 99.92                           | 0.00001                      |
| 25028RN03A            | 99.90                           | 0.00032                      |
| iPhone12,1            | 100.05                          | 0.00001                      |
| iPhone14,2            | 99.93                           | 0.00001                      |
| iPhone16,2            | 99.99                           | 0.00001                      |
| Pixel 5               | 70.89                           | 0.00003                      |
| iPhone15,3            | 100.17                          | 0.00001                      |
| SM-G780G              | 207.46                          | 0.00000                      |
| Pixel 6a              | 72.75                           | 0.00002                      |
| iPhone14,6            | 99.56                           | 0.00001                      |
| SM-S926B              | 124.81                          | 0.00001                      |
| iPhone14,4            | 100.27                          | 0.00001                      |
| iPhone11,8            | 99.81                           | 0.00001                      |
| Pixel 4a              | 68.23                           | 0.00003                      |
| iPhone13,1            | 100.57                          | 0.00001                      |
| iPhone13,3            | 100.49                          | 0.00001                      |
| SM-S931B              | 199.75                          | 0.00036                      |
| Pixel 7 Pro           | 79.22                           | 0.00020                      |
| Pixel 9               | 66.89                           | 0.00109                      |
| iPhone17,2            | 100.11                          | 0.00001                      |
| SM-S901U              | 209.45                          | 0.00034                      |
| M2007J20CG            | 201.96                          | 0.00007                      |
| Pixel 8               | 91.90                           | 0.00053                      |
| SM-A346M              | 125.13                          | 0.00023                      |
| SM-F741N              | 188.59                          | 0.00002                      |
| Pixel 7a              | 79.28                           | 0.00002                      |
| SM-S928B              | 199.75                          | 0.00036                      |
| Pixel 7               | 78.82                           | 0.00002                      |
| SM-A145R              | 203.94                          | 0.00004                      |
| iPhone14,3            | 100.54                          | 0.00001                      |
| Pixel 6               | 73.29                           | 0.00002                      |
| iPhone17,3            | 100.10                          | 0.00006                      |
| SM-S911B              | 208.89                          | 0.00034                      |
| SM-G998B              | 100.07                          | 0.00009                      |
| iPhone12,8            | 100.06                          | 0.00001                      |
| SM-A528B              | 207.53                          | 0.00188                      |
| iPhone9,1             | 100.35                          | 0.00001                      |
| Pixel 9 Pro XL        | 66.15                           | 0.00040                      |
| XQ-BC42               | 209.79                          | 0.00017                      |
| SM-G991B              | 100.07                          | 0.00009                      |
| iPhone11,2            | 99.66                           | 0.00001                      |
| SM-G770F              | 212.46                          | 0.00001                      |
| VS988                 | 200.27                          | 0.00001                      |
| CPH2353               | 200.55                          | 0.00002                      |
| SM-S908B              | 99.19                           | 0.00005                      |
| SM-S918B              | 210.80                          | 0.00034                      |
| XQ-EC44               | 208.54                          | 0.00017                      |
| M2105K81C             | 203.97                          | 0.00001                      |
| SM-G781B              | 205.77                          | 0.00000                      |
| motorola edge 20 lite | 400.24                          | 0.00008                      |
| iPhone13,4            | 100.15                          | 0.00001                      |
| CPH2333               | 100.10                          | 0.00001                      |
| XQ-FE44               | 197.30                          | 0.00001                      |
| SM-A515F              | 126.62                          | 0.00052                      |
| SM-S921B              | 125.05                          | 0.00001                      |
| iPhone14,8            | 100.48                          | 0.00001                      |
| Pixel 9 Pro           | 49.76                           | 0.00003                      |
| M2007J17I             | 248.94                          | 0.00000                      |
| moto g stylus 5G      | 200.05                          | 0.00012                      |
| SM-A405FN             | 98.80                           | 0.00090                      |
| moto g 5G             | 199.95                          | 0.00001                      |
| SM-A720F              | 97.84                           | 0.00064                      |
| CPH2603               | 401.06                          | 0.00000                      |
| 23129RA5FL            | 199.91                          | 0.00012                      |
| SM-A566E              | 125.46                          | 0.00058                      |
| SM-S9280              | 199.75                          | 0.00036                      |
| iPhone17,5            | 100.04                          | 0.00003                      |
| moto g13              | 398.90                          | 0.00000                      |
| iPhone9,3             | 100.09                          | 0.00002                      |
| Redmi Note 9 Pro      | 208.32                          | 0.00034                      |
| iPhone15,5            | 99.88                           | 0.00001                      |
| iPad13,4              | 99.39                           | 0.00001                      |
| iPhone18,1            | 100.20                          | 0.00001                      |
| iPhone11,6            | 100.09                          | 0.00001                      |
| TC27                  | 212.72                          | 0.00000                      |
| SM-S938B              | 199.75                          | 0.00036                      |
| iPhone12,3            | 100.65                          | 0.00001                      |
| SM-S711B              | 128.18                          | 0.00091                      |
| iPhone9,4             | 100.25                          | 0.00002                      |
| SM-G991U1             | 207.73                          | 0.00034                      |
| 23078RKD5C            | 210.27                          | 0.00030                      |
| SM-A546E              | 124.03                          | 0.00064                      |
| SM-A536B              | 124.75                          | 0.00146                      |
| 2311DRK48G            | 206.78                          | 0.00008                      |
| SM-G973F              | 100.10                          | 0.00007                      |
| ASUS_I006D            | 200.09                          | 0.00009                      |
| SM-A346B              | 125.63                          | 0.00102                      |
| iPhone10,6            | 99.32                           | 0.00001                      |
| moto g(20)            | 97.52                           | 0.00032                      |
| SM-S918U              | 211.81                          | 0.00019                      |
| SM-S901E              | 208.79                          | 0.00034                      |
| SM-S911U              | 210.34                          | 0.00034                      |
| motorola edge 40 neo  | 404.07                          | 0.00000                      |
| CPH2647               | 199.46                          | 0.00013                      |
| SM-S931N              | 199.75                          | 0.00036                      |
| SM-S911U1             | 208.03                          | 0.00034                      |
| SM-S918N              | 211.53                          | 0.00000                      |
| 23116PN5BC            | 205.33                          | 0.00004                      |
| 23122PCD1G            | 211.40                          | 0.00000                      |
| SM-M346B              | 124.73                          | 0.00137                      |
| BV9900Pro             | 398.47                          | 0.00000                      |
| SM-N976U              | 204.16                          | 0.00035                      |
| FP5                   | 211.80                          | 0.00017                      |
| G8441                 | 203.83                          | 0.00001                      |
| iPhone10,3            | 100.58                          | 0.00001                      |
| Pixel 8a              | 76.10                           | 0.00208                      |
| BND-AL10              | 100.09                          | 0.00010                      |
| SM-G780F              | 76.57                           | 0.00464                      |
| SM-S928U              | 192.17                          | 0.00001                      |
| LE2123                | 199.95                          | 0.00020                      |
| moto g(8) plus        | 201.11                          | 0.00005                      |
| LGE-AN00              | 200.24                          | 0.00005                      |
| MAR-LX1A              | 100.84                          | 0.00001                      |
| Pixel 10 Pro          | 67.24                           | 0.00031                      |
| Redmi Note 8 Pro      | 397.61                          | 0.00015                      |
| Mi 10 Pro             | 211.76                          | 0.00000                      |
| SM-G781W              | 210.33                          | 0.00001                      |
| M2012K11AG            | 201.47                          | 0.00034                      |
| SM-A325F              | 98.09                           | 0.00199                      |
| 2312DRA50G            | 201.14                          | 0.00028                      |
| moto g 5G plus        | 204.20                          | 0.00050                      |
| SM-S166V              | 124.31                          | 0.00040                      |
| Pixel 9a              | 58.69                           | 0.00003                      |
| 22071212AG            | 209.52                          | 0.00000                      |
| SM-A217F              | 99.54                           | 0.00002                      |
| A142                  | 205.88                          | 0.00000                      |
| SM-G975F              | 100.07                          | 0.00012                      |
| M2101K9G              | 200.20                          | 0.00000                      |
| SM-A256E              | 124.12                          | 0.00029                      |
| 23049PCD8G            | 201.91                          | 0.00012                      |
| SM-S918U1             | 210.55                          | 0.00034                      |
| iPhone8,1             | 100.11                          | 0.00002                      |
| SM-F946B              | 199.75                          | 0.00036                      |
| CPH2387               | 368.76                          | 0.00347                      |
| YAL-L21               | 100.10                          | 0.00001                      |
| JKM-LX3               | 100.84                          | 0.00001                      |
| SM-S911W              | 210.83                          | 0.00034                      |
| M2012K11I             | 202.33                          | 0.00008                      |
| SM-S908N              | 211.38                          | 0.00034                      |
| Redmi Note 5 Pro      | 199.38                          | 0.00002                      |
| RMX3363               | 203.62                          | 0.00001                      |
| SM-S901U1             | 204.58                          | 0.00035                      |
| TEL-AN00              | 100.10                          | 0.00001                      |
| SM-N770F              | 100.08                          | 0.00008                      |
| iPhone10,4            | 99.71                           | 0.00001                      |
| 2109119DG             | 200.20                          | 0.00000                      |
| CPH2449               | 200.20                          | 0.00001                      |

### Gravity

| Device Model     | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| ---------------- | ------------------------------- | ---------------------------- |
| iPhone16,1       | 100.05                          | 0.00001                      |
| iPhone15,2       | 100.45                          | 0.00001                      |
| iPhone14,5       | 99.97                           | 0.00001                      |
| iPhone14,7       | 100.26                          | 0.00001                      |
| 25028RN03A       | 99.95                           | 0.00016                      |
| iPhone17,1       | 100.04                          | 0.00001                      |
| iPhone13,2       | 99.82                           | 0.00001                      |
| iPhone15,4       | 100.19                          | 0.00001                      |
| Pixel 5          | 212.65                          | 0.00002                      |
| iPhone16,2       | 100.04                          | 0.00001                      |
| iPhone14,2       | 99.93                           | 0.00001                      |
| SM-G780G         | 207.46                          | 0.00000                      |
| SM-S926B         | 124.81                          | 0.00001                      |
| iPhone15,3       | 100.27                          | 0.00001                      |
| Pixel 4a         | 204.62                          | 0.00002                      |
| iPhone11,8       | 99.81                           | 0.00001                      |
| iPhone12,1       | 100.14                          | 0.00001                      |
| Pixel 7 Pro      | 237.44                          | 0.00027                      |
| Pixel 9          | 198.28                          | 0.00072                      |
| SM-S931B         | 199.75                          | 0.00036                      |
| iPhone13,1       | 100.58                          | 0.00001                      |
| SM-S901U         | 209.44                          | 0.00034                      |
| SM-A145R         | 203.94                          | 0.00004                      |
| Pixel 6a         | 222.71                          | 0.00001                      |
| iPhone14,4       | 100.17                          | 0.00001                      |
| iPhone17,2       | 100.13                          | 0.00001                      |
| SM-S928B         | 199.75                          | 0.00036                      |
| Pixel 8          | 197.83                          | 0.00055                      |
| iPhone14,3       | 99.84                           | 0.00001                      |
| iPhone9,1        | 100.35                          | 0.00001                      |
| iPhone17,3       | 100.11                          | 0.00011                      |
| XQ-BC42          | 209.79                          | 0.00017                      |
| CPH2353          | 200.55                          | 0.00002                      |
| Pixel 7          | 236.62                          | 0.00027                      |
| XQ-EC44          | 208.54                          | 0.00017                      |
| M2105K81C        | 203.97                          | 0.00001                      |
| SM-G998B         | 100.07                          | 0.00009                      |
| iPhone18,1       | 99.82                           | 0.00001                      |
| SM-G781B         | 205.77                          | 0.00000                      |
| iPhone11,2       | 99.66                           | 0.00001                      |
| iPhone13,4       | 100.41                          | 0.00001                      |
| XQ-FE44          | 197.30                          | 0.00001                      |
| iPhone14,6       | 100.50                          | 0.00001                      |
| SM-A515F         | 126.62                          | 0.00052                      |
| iPhone13,3       | 100.20                          | 0.00001                      |
| SM-S911B         | 208.90                          | 0.00034                      |
| 23013PC75G       | 204.87                          | 0.00035                      |
| SM-A405FN        | 98.91                           | 0.00088                      |
| SM-A528B         | 207.56                          | 0.00188                      |
| CPH2603          | 401.06                          | 0.00000                      |
| moto g13         | 398.90                          | 0.00000                      |
| iPhone12,8       | 99.89                           | 0.00001                      |
| Pixel 6          | 223.69                          | 0.00001                      |
| SM-G991B         | 100.07                          | 0.00010                      |
| iPad13,4         | 99.39                           | 0.00001                      |
| SM-A720F         | 97.94                           | 0.00071                      |
| 23129RA5FL       | 199.97                          | 0.00012                      |
| TC27             | 212.72                          | 0.00000                      |
| SM-S9280         | 199.75                          | 0.00036                      |
| SM-S918B         | 211.13                          | 0.00034                      |
| Pixel 9 Pro XL   | 198.16                          | 0.00061                      |
| 23078RKD5C       | 210.38                          | 0.00017                      |
| SM-A536B         | 124.81                          | 0.00146                      |
| SM-G991U1        | 207.73                          | 0.00034                      |
| ASUS_I006D       | 200.09                          | 0.00009                      |
| iPhone14,8       | 100.48                          | 0.00001                      |
| SM-A346B         | 125.63                          | 0.00102                      |
| iPhone10,6       | 99.32                           | 0.00001                      |
| moto g(20)       | 97.57                           | 0.00016                      |
| SM-S911U         | 210.34                          | 0.00034                      |
| CPH2647          | 199.46                          | 0.00013                      |
| SM-S931N         | 199.75                          | 0.00036                      |
| SM-A546E         | 123.78                          | 0.00069                      |
| SM-S918N         | 211.53                          | 0.00000                      |
| iPhone12,3       | 100.65                          | 0.00001                      |
| G8441            | 203.83                          | 0.00001                      |
| iPhone9,3        | 100.18                          | 0.00002                      |
| Redmi Note 9 Pro | 208.32                          | 0.00001                      |
| 2311DRK48G       | 206.82                          | 0.00008                      |
| SM-G780F         | 76.57                           | 0.00464                      |
| SM-S928U         | 192.17                          | 0.00001                      |
| moto g stylus 5G | 200.13                          | 0.00008                      |
| moto g(8) plus   | 201.11                          | 0.00005                      |
| LGE-AN00         | 200.24                          | 0.00005                      |
| SM-G770F         | 212.46                          | 0.00001                      |
| Redmi Note 8 Pro | 397.61                          | 0.00015                      |
| SM-S918U         | 211.94                          | 0.00033                      |
| moto g 5G plus   | 204.20                          | 0.00050                      |
| SM-S166V         | 124.31                          | 0.00040                      |
| SM-A566E         | 124.53                          | 0.00056                      |
| SM-A217F         | 99.54                           | 0.00002                      |
| A142             | 205.88                          | 0.00000                      |
| M2101K9G         | 200.20                          | 0.00000                      |
| SM-S908B         | 99.19                           | 0.00005                      |
| Pixel 8a         | 234.20                          | 0.00046                      |
| Pixel 7a         | 233.58                          | 0.00020                      |
| BND-AL10         | 100.10                          | 0.00002                      |
| iPhone9,4        | 99.94                           | 0.00002                      |
| SM-S901E         | 208.74                          | 0.00034                      |
| SM-N770F         | 100.08                          | 0.00008                      |
| iPhone10,4       | 99.71                           | 0.00001                      |
| 2109119DG        | 200.20                          | 0.00000                      |

### Gyroscope

| Device Model          | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| --------------------- | ------------------------------- | ---------------------------- |
| iPhone16,1            | 100.05                          | 0.00001                      |
| iPhone13,2            | 99.86                           | 0.00001                      |
| iPhone15,2            | 100.41                          | 0.00001                      |
| iPhone14,5            | 100.03                          | 0.00001                      |
| iPhone14,7            | 99.99                           | 0.00001                      |
| RMX3710               | 210.08                          | 0.00001                      |
| iPhone17,1            | 100.04                          | 0.00001                      |
| iPhone16,2            | 99.96                           | 0.00001                      |
| iPhone15,4            | 99.88                           | 0.00001                      |
| iPhone12,1            | 100.14                          | 0.00001                      |
| iPhone14,2            | 99.92                           | 0.00001                      |
| Pixel 6a              | 443.09                          | 0.00001                      |
| Pixel 5               | 425.08                          | 0.00001                      |
| SM-G780G              | 414.94                          | 0.00000                      |
| SM-S926B              | 498.98                          | 0.00000                      |
| iPhone15,3            | 100.27                          | 0.00001                      |
| motorola edge 20 lite | 400.69                          | 0.00000                      |
| iPhone14,4            | 100.27                          | 0.00001                      |
| iPhone17,2            | 100.10                          | 0.00001                      |
| Pixel 4a              | 409.23                          | 0.00001                      |
| iPhone11,8            | 99.81                           | 0.00001                      |
| Pixel 7 Pro           | 476.16                          | 0.00003                      |
| iPhone13,1            | 100.58                          | 0.00001                      |
| SM-S931B              | 462.76                          | 0.00000                      |
| Pixel 9               | 401.73                          | 0.00002                      |
| Pixel 8               | 399.57                          | 0.00001                      |
| SM-S901U              | 419.84                          | 0.00000                      |
| SM-A346M              | 500.46                          | 0.00002                      |
| M2007J20CG            | 403.92                          | 0.00007                      |
| iPhone13,3            | 100.57                          | 0.00001                      |
| SM-F741N              | 471.48                          | 0.00001                      |
| Pixel 6               | 445.45                          | 0.00001                      |
| SM-S928B              | 469.95                          | 0.00000                      |
| moto g(20)            | 195.24                          | 0.00001                      |
| iPhone14,3            | 100.49                          | 0.00001                      |
| Pixel 7               | 474.39                          | 0.00003                      |
| SM-G770F              | 424.87                          | 0.00001                      |
| iPhone17,3            | 100.11                          | 0.00006                      |
| SM-S911B              | 418.72                          | 0.00000                      |
| iPhone12,8            | 100.23                          | 0.00001                      |
| SM-A528B              | 839.99                          | 0.00001                      |
| ELE-L29               | 500.50                          | 0.00001                      |
| iPhone9,1             | 100.35                          | 0.00001                      |
| Pixel 9 Pro XL        | 397.97                          | 0.00002                      |
| XQ-BC42               | 420.04                          | 0.00000                      |
| SM-G998B              | 499.81                          | 0.00009                      |
| XQ-BE72               | 425.07                          | 0.00000                      |
| CPH2353               | 401.10                          | 0.00002                      |
| iPhone18,1            | 99.89                           | 0.00001                      |
| XQ-EC44               | 417.50                          | 0.00000                      |
| M2105K81C             | 408.00                          | 0.00000                      |
| SM-G781B              | 411.54                          | 0.00000                      |
| iPhone11,2            | 99.66                           | 0.00001                      |
| SM-S908B              | 495.05                          | 0.00008                      |
| SM-S918B              | 422.88                          | 0.00000                      |
| CPH2333               | 100.10                          | 0.00001                      |
| iPhone13,4            | 100.21                          | 0.00001                      |
| XQ-FE44               | 394.62                          | 0.00001                      |
| iPhone14,6            | 100.50                          | 0.00001                      |
| SM-A515F              | 508.63                          | 0.00004                      |
| CPH2647               | 402.68                          | 0.00000                      |
| 23013PC75G            | 410.67                          | 0.00000                      |
| M2007J17I             | 497.91                          | 0.00000                      |
| 23122PCD1G            | 422.71                          | 0.00000                      |
| SM-G991B              | 499.80                          | 0.00009                      |
| SM-A405FN             | 99.90                           | 0.00036                      |
| moto g 5G             | 399.89                          | 0.00000                      |
| SM-A720F              | 196.93                          | 0.00028                      |
| CPH2603               | 401.06                          | 0.00000                      |
| SM-S921B              | 500.29                          | 0.00002                      |
| SM-A566E              | 500.54                          | 0.00000                      |
| SM-S9280              | 483.98                          | 0.00000                      |
| iPhone14,8            | 100.48                          | 0.00001                      |
| moto g13              | 398.90                          | 0.00000                      |
| SM-G991U1             | 416.37                          | 0.00000                      |
| 23078RKD5C            | 420.74                          | 0.00011                      |
| 2211133C              | 399.27                          | 0.00001                      |
| SM-A546E              | 495.04                          | 0.00055                      |
| Redmi Note 9 Pro      | 416.57                          | 0.00001                      |
| iPhone15,5            | 99.88                           | 0.00001                      |
| iPad13,4              | 99.39                           | 0.00001                      |
| 23129RA5FL            | 400.19                          | 0.00002                      |
| TC27                  | 425.44                          | 0.00000                      |
| iPhone12,3            | 100.65                          | 0.00001                      |
| iPhone9,4             | 100.25                          | 0.00002                      |
| SM-A536B              | 500.39                          | 0.00010                      |
| 2311DRK48G            | 413.57                          | 0.00000                      |
| iPhone10,3            | 100.58                          | 0.00001                      |
| SM-G973F              | 500.51                          | 0.00000                      |
| iPhone9,3             | 100.09                          | 0.00002                      |
| BND-AL10              | 200.20                          | 0.00001                      |
| ASUS_I006D            | 501.38                          | 0.00000                      |
| LE2123                | 502.97                          | 0.00000                      |
| SM-A346B              | 500.47                          | 0.00002                      |
| iPhone10,6            | 99.32                           | 0.00001                      |
| SM-S901E              | 418.49                          | 0.00001                      |
| motorola edge 40 neo  | 404.07                          | 0.00000                      |
| SM-S931N              | 461.71                          | 0.00000                      |
| SM-S918N              | 423.07                          | 0.00000                      |
| SM-N976U              | 409.15                          | 0.00000                      |
| G8441                 | 407.54                          | 0.00003                      |
| Pixel 8a              | 472.17                          | 0.00001                      |
| Pixel 7a              | 472.26                          | 0.00007                      |
| SM-G780F              | 499.87                          | 0.00009                      |
| SM-S928U              | 356.22                          | 0.00000                      |
| moto g stylus 5G      | 503.53                          | 0.00000                      |
| moto g(8) plus        | 402.74                          | 0.00004                      |
| LGE-AN00              | 800.56                          | 0.00001                      |
| Pixel 10 Pro          | 401.41                          | 0.00001                      |
| SM-S938B              | 462.61                          | 0.00039                      |
| Redmi Note 8 Pro      | 397.61                          | 0.00015                      |
| SM-G781W              | 420.42                          | 0.00000                      |
| 2312DRA50G            | 402.98                          | 0.00001                      |
| SM-S711B              | 499.03                          | 0.00000                      |
| SM-S918U              | 424.83                          | 0.00000                      |
| Pixel 9 Pro           | 398.10                          | 0.00002                      |
| moto g 5G plus        | 409.62                          | 0.00000                      |
| SM-S166V              | 497.07                          | 0.00006                      |
| iPhone18,2            | 100.16                          | 0.00001                      |
| 22071212AG            | 419.05                          | 0.00000                      |
| SM-S911U1             | 416.94                          | 0.00000                      |
| SM-A217F              | 199.05                          | 0.00002                      |
| A142                  | 411.76                          | 0.00000                      |
| M2101K9G              | 501.16                          | 0.00000                      |
| SM-A256E              | 496.65                          | 0.00001                      |
| 23049PCD8G            | 401.21                          | 0.00001                      |
| iPhone8,1             | 100.11                          | 0.00002                      |
| Infinix X6871         | 465.73                          | 0.00041                      |
| SM-S911U              | 421.61                          | 0.00000                      |
| SM-A5560              | 500.37                          | 0.00000                      |
| SM-F946B              | 478.05                          | 0.00001                      |
| M2101K9AG             | 501.90                          | 0.00000                      |
| CPH2387               | 406.77                          | 0.00000                      |
| JKM-LX3               | 252.11                          | 0.00001                      |
| SM-S911W              | 422.61                          | 0.00000                      |
| M2012K11I             | 404.65                          | 0.00000                      |
| SM-S908N              | 423.70                          | 0.00000                      |
| Redmi Note 5 Pro      | 398.76                          | 0.00001                      |
| SM-S901U1             | 410.07                          | 0.00000                      |
| TEL-AN00              | 250.25                          | 0.00000                      |
| SM-N770F              | 500.01                          | 0.00006                      |
| iPhone10,4            | 99.71                           | 0.00001                      |
| 2109119DG             | 499.92                          | 0.00000                      |

### Magnetometer

| Device Model     | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| ---------------- | ------------------------------- | ---------------------------- |
| iPhone16,1       | 99.79                           | 0.00001                      |
| 25028RN03A       | 99.90                           | 0.00032                      |
| iPhone13,2       | 99.82                           | 0.00001                      |
| iPhone17,1       | 100.04                          | 0.00001                      |
| Pixel 5          | 100.40                          | 0.00004                      |
| iPhone14,5       | 99.71                           | 0.00001                      |
| SM-G780G         | 100.10                          | 0.00001                      |
| iPhone14,7       | 99.97                           | 0.00001                      |
| SM-S926B         | 124.81                          | 0.00001                      |
| Pixel 9          | 100.03                          | 0.00002                      |
| Pixel 6a         | 100.10                          | 0.00001                      |
| Pixel 4a         | 99.80                           | 0.00001                      |
| SM-S901U         | 100.10                          | 0.00001                      |
| Pixel 7 Pro      | 100.10                          | 0.00001                      |
| SM-S931B         | 100.10                          | 0.00001                      |
| iPhone15,2       | 100.15                          | 0.00001                      |
| Pixel 8          | 100.10                          | 0.00002                      |
| Pixel 7a         | 100.10                          | 0.00001                      |
| SM-S928B         | 100.10                          | 0.00001                      |
| iPhone15,4       | 100.19                          | 0.00001                      |
| iPhone14,2       | 99.92                           | 0.00001                      |
| iPhone15,3       | 100.37                          | 0.00001                      |
| iPhone9,1        | 100.35                          | 0.00001                      |
| iPhone17,3       | 100.11                          | 0.00011                      |
| iPhone12,1       | 100.52                          | 0.00001                      |
| XQ-BC42          | 100.10                          | 0.00001                      |
| SM-G998B         | 100.07                          | 0.00009                      |
| CPH2353          | 100.10                          | 0.00001                      |
| XQ-EC44          | 100.10                          | 0.00001                      |
| Pixel 7          | 100.10                          | 0.00002                      |
| SM-G781B         | 100.10                          | 0.00001                      |
| iPhone17,2       | 100.13                          | 0.00001                      |
| SM-S908B         | 99.05                           | 0.00010                      |
| Pixel 6          | 100.10                          | 0.00001                      |
| iPhone11,8       | 99.97                           | 0.00001                      |
| XQ-FE44          | 100.10                          | 0.00001                      |
| SM-A145R         | 50.05                           | 0.00002                      |
| 23013PC75G       | 100.10                          | 0.00001                      |
| SM-A720F         | 98.04                           | 0.00051                      |
| LM-K920          | 100.09                          | 0.00004                      |
| CPH2603          | 50.05                           | 0.00002                      |
| SM-S918B         | 100.10                          | 0.00001                      |
| iPhone14,6       | 100.50                          | 0.00001                      |
| Pixel 8a         | 100.10                          | 0.00002                      |
| SM-G991B         | 100.07                          | 0.00009                      |
| iPad13,4         | 99.39                           | 0.00001                      |
| SM-A515F         | 127.12                          | 0.00016                      |
| TC27             | 100.10                          | 0.00001                      |
| 23078RKD5C       | 50.05                           | 0.00004                      |
| SM-A536B         | 124.73                          | 0.00010                      |
| SM-S721B         | 125.10                          | 0.00001                      |
| iPhone13,3       | 99.99                           | 0.00001                      |
| iPhone16,2       | 100.07                          | 0.00001                      |
| iPhone13,1       | 100.06                          | 0.00001                      |
| SM-G770F         | 100.10                          | 0.00005                      |
| ASUS_I006D       | 99.90                           | 0.00045                      |
| iPhone18,1       | 100.05                          | 0.00001                      |
| SM-S921B         | 125.10                          | 0.00001                      |
| CPH2647          | 100.10                          | 0.00001                      |
| SM-S931N         | 100.10                          | 0.00001                      |
| moto g13         | 50.05                           | 0.00002                      |
| SM-M346B         | 124.23                          | 0.00008                      |
| SM-N976U         | 100.25                          | 0.00026                      |
| G8441            | 101.43                          | 0.00002                      |
| BND-AL10         | 100.10                          | 0.00007                      |
| 2311DRK48G       | 50.05                           | 0.00139                      |
| SM-S928U         | 100.10                          | 0.00001                      |
| moto g stylus 5G | 100.10                          | 0.00001                      |
| LE2123           | 100.10                          | 0.00001                      |
| LGE-AN00         | 100.10                          | 0.00001                      |
| Redmi Note 8 Pro | 100.10                          | 0.00002                      |
| iPhone9,4        | 99.94                           | 0.00002                      |
| SM-A566E         | 125.14                          | 0.00001                      |
| Pixel 9 Pro XL   | 100.10                          | 0.00002                      |
| M2007J17I        | 100.10                          | 0.00001                      |
| SM-G996B         | 100.07                          | 0.00009                      |
| Pixel 8 Pro      | 100.10                          | 0.00002                      |
| SM-A165F         | 125.12                          | 0.00027                      |
| iPhone14,4       | 99.41                           | 0.00001                      |
| SM-G991U1        | 100.10                          | 0.00001                      |
| iPhone12,8       | 100.23                          | 0.00001                      |
| SM-S911B         | 100.10                          | 0.00001                      |

### Orientation

| Device Model     | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| ---------------- | ------------------------------- | ---------------------------- |
| iPhone16,1       | 99.94                           | 0.00001                      |
| iPhone13,2       | 99.82                           | 0.00001                      |
| 25028RN03A       | 99.95                           | 0.00016                      |
| iPhone17,1       | 100.04                          | 0.00001                      |
| iPhone14,5       | 99.71                           | 0.00001                      |
| iPhone14,7       | 100.26                          | 0.00001                      |
| Pixel 5          | 212.65                          | 0.00001                      |
| SM-G780G         | 207.47                          | 0.00000                      |
| SM-S926B         | 124.81                          | 0.00001                      |
| iPhone15,2       | 100.15                          | 0.00001                      |
| iPhone14,2       | 99.93                           | 0.00001                      |
| Pixel 4a         | 204.63                          | 0.00002                      |
| iPhone15,4       | 100.19                          | 0.00001                      |
| Pixel 9          | 197.78                          | 0.00072                      |
| Pixel 7 Pro      | 237.66                          | 0.00013                      |
| Pixel 6a         | 222.72                          | 0.00001                      |
| SM-S901U         | 209.90                          | 0.00000                      |
| SM-S931B         | 199.98                          | 0.00018                      |
| iPhone14,4       | 100.10                          | 0.00001                      |
| SM-A145R         | 203.94                          | 0.00004                      |
| SM-S928B         | 200.20                          | 0.00000                      |
| iPhone16,2       | 99.96                           | 0.00001                      |
| iPhone12,1       | 100.25                          | 0.00001                      |
| iPhone17,2       | 100.13                          | 0.00001                      |
| iPhone15,3       | 100.37                          | 0.00001                      |
| Pixel 8          | 197.83                          | 0.00055                      |
| iPhone11,8       | 99.80                           | 0.00001                      |
| iPhone9,1        | 100.35                          | 0.00001                      |
| iPhone17,3       | 100.11                          | 0.00011                      |
| SM-G998B         | 100.07                          | 0.00009                      |
| Pixel 7a         | 238.15                          | 0.00001                      |
| CPH2353          | 200.55                          | 0.00002                      |
| M2105K81C        | 204.00                          | 0.00000                      |
| SM-G781B         | 205.77                          | 0.00000                      |
| Pixel 7          | 236.90                          | 0.00013                      |
| iPhone14,3       | 100.54                          | 0.00001                      |
| SM-S908B         | 99.11                           | 0.00010                      |
| iPhone13,3       | 100.13                          | 0.00001                      |
| XQ-EC44          | 208.52                          | 0.00021                      |
| RMX3710          | 210.04                          | 0.00008                      |
| XQ-FE44          | 197.30                          | 0.00001                      |
| iPhone14,6       | 100.50                          | 0.00001                      |
| SM-A515F         | 126.62                          | 0.00052                      |
| CPH2647          | 201.34                          | 0.00001                      |
| SM-S911B         | 209.37                          | 0.00000                      |
| SM-G991B         | 100.07                          | 0.00009                      |
| SM-G991U1        | 208.17                          | 0.00000                      |
| M2007J17I        | 248.95                          | 0.00000                      |
| SM-A405FN        | 98.91                           | 0.00088                      |
| SM-G770F         | 212.47                          | 0.00000                      |
| CPH2603          | 401.06                          | 0.00000                      |
| SM-S9280         | 200.20                          | 0.00000                      |
| moto g13         | 398.90                          | 0.00000                      |
| iPhone12,8       | 99.89                           | 0.00001                      |
| Pixel 6          | 223.31                          | 0.00001                      |
| iPad13,4         | 99.39                           | 0.00001                      |
| SM-A720F         | 97.94                           | 0.00071                      |
| VS988            | 200.27                          | 0.00001                      |
| 23129RA5FL       | 200.11                          | 0.00004                      |
| TC27             | 212.72                          | 0.00000                      |
| SM-S918B         | 211.61                          | 0.00000                      |
| 23078RKD5C       | 210.62                          | 0.00008                      |
| SM-A536B         | 124.81                          | 0.00146                      |
| iPhone13,1       | 100.86                          | 0.00001                      |
| ASUS_I006D       | 200.20                          | 0.00000                      |
| SM-A346B         | 125.63                          | 0.00102                      |
| SM-A528B         | 210.33                          | 0.00002                      |
| iPhone10,6       | 99.32                           | 0.00001                      |
| iPhone18,1       | 100.05                          | 0.00001                      |
| SM-S901E         | 209.28                          | 0.00001                      |
| Pixel 9 Pro XL   | 197.89                          | 0.00040                      |
| SM-S931N         | 200.20                          | 0.00000                      |
| SM-S918N         | 211.53                          | 0.00000                      |
| 23116PN5BC       | 199.87                          | 0.00015                      |
| Pixel 8a         | 225.20                          | 0.00120                      |
| G8441            | 203.83                          | 0.00001                      |
| iPhone10,3       | 100.48                          | 0.00001                      |
| Redmi Note 9 Pro | 209.01                          | 0.00001                      |
| BND-AL10         | 100.10                          | 0.00002                      |
| 2311DRK48G       | 206.83                          | 0.00008                      |
| SM-G780F         | 76.57                           | 0.00464                      |
| SM-S928U         | 192.20                          | 0.00001                      |
| moto g stylus 5G | 200.20                          | 0.00000                      |
| moto g(8) plus   | 201.11                          | 0.00005                      |
| LGE-AN00         | 100.14                          | 0.00116                      |
| SM-S711B         | 123.78                          | 0.00091                      |
| SM-S918U         | 212.42                          | 0.00000                      |
| moto g 5G plus   | 204.81                          | 0.00000                      |
| SM-S166V         | 124.31                          | 0.00040                      |
| iPhone17,5       | 99.89                           | 0.00001                      |
| SM-A566E         | 124.53                          | 0.00056                      |
| A142             | 205.88                          | 0.00000                      |
| SM-G975F         | 100.07                          | 0.00012                      |
| M2101K9G         | 200.20                          | 0.00000                      |
| SM-A136U         | 125.12                          | 0.00003                      |
| 23049PCD8G       | 199.86                          | 0.00015                      |
| iPhone8,1        | 100.11                          | 0.00002                      |
| SM-F946B         | 200.20                          | 0.00000                      |
| SM-S901U1        | 206.73                          | 0.00000                      |
| SM-A546E         | 123.53                          | 0.00079                      |
| iPhone9,4        | 99.94                           | 0.00002                      |
| M2012K11I        | 202.33                          | 0.00008                      |
| SM-N770F         | 100.08                          | 0.00008                      |
| iPhone10,4       | 99.71                           | 0.00001                      |

### Light

| Device Model           | Median Achievable Sampling (Hz) | Sampling Gap Variability (s) |
| ---------------------- | ------------------------------- | ---------------------------- |
| SM-A146U               | 6.25                            | 0.00279                      |
| CPH2375                | 5.10                            | 0.00691                      |
| SM-S928B               | 2.05                            | 0.72945                      |
| SM-G991B               | 7.54                            | 0.02501                      |
| SM-S911B               | 1.05                            | 2.10842                      |
| Pixel 4                | 0.01                            | 763.65927                    |
| SM-G977U               | 0.94                            | 2.11056                      |
| XQ-CT72                | 13.15                           | 0.07322                      |
| SM-S931B               | 0.54                            | 1.93483                      |
| SM-S926B               | 2.88                            | 0.74723                      |
| SM-A546B               | 14.17                           | 0.06577                      |
| I2218                  | 6.26                            | 0.00016                      |
| SM-S938B               | 1.76                            | 1.39158                      |
| SM-A256E               | 5.28                            | 0.21881                      |
| Pixel 4a               | 0.48                            | 2.90036                      |
| SM-S901U               | 2.31                            | 0.70425                      |
| CPH2707                | 3.71                            | 0.04896                      |
| Pixel 5                | 0.36                            | 5.23967                      |
| moto g 5G - 2024       | 0.70                            | 3.96510                      |
| SC-51A                 | 3.40                            | 0.24357                      |
| RMX3360                | 4.77                            | 0.01954                      |
| SM-S918U               | 2.57                            | 0.73175                      |
| SM-S901E               | 5.51                            | 0.06509                      |
| moto g - 2025          | 5.02                            | 0.00190                      |
| Redmi Note 8 Pro       | 0.89                            | 2.46850                      |
| SM-A528B               | 6.26                            | 0.01894                      |
| 2312DRAABC             | 1.41                            | 1.18833                      |
| Pixel 8a               | 0.82                            | 2.26009                      |
| SM-A155F               | 2.39                            | 0.72062                      |
| SM-G990B               | 5.85                            | 0.04134                      |
| SM-S918B               | 1.22                            | 1.21978                      |
| SM-S938U1              | 1.38                            | 0.96914                      |
| SM-G996U1              | 2.36                            | 0.36704                      |
| SM-S146VL              | 6.25                            | 0.00331                      |
| moto e13               | 5.36                            | 0.09018                      |
| Infinix X6528          | 380.12                          | 0.00021                      |
| 9137W                  | 0.39                            | 69.11964                     |
| SM-G975U1              | 1.76                            | 0.84135                      |
| CPH2353                | 4.88                            | 0.00137                      |
| Pixel 7                | 0.70                            | 5.46987                      |
| SM-G960F               | 0.84                            | 4.54177                      |
| SM-G990B2              | 2.90                            | 0.51697                      |
| SM-S921B               | 4.48                            | 0.42361                      |
| XQ-EC44                | 1.03                            | 3.67909                      |
| SM-A155M               | 2.84                            | 0.73211                      |
| SM-A556B               | 6.87                            | 2.34178                      |
| 2209116AG              | 5.49                            | 0.26245                      |
| 23113RKC6C             | 0.47                            | 4.75145                      |
| SM-S9160               | 0.44                            | 7.52838                      |
| SM-S9060               | 0.72                            | 7.53942                      |
| Pixel 7 Pro            | 0.67                            | 12.67353                     |
| moto g35 5G            | 8.03                            | 0.24733                      |
| Pixel 9                | 0.11                            | 92.30455                     |
| SM-G781B               | 6.26                            | 0.00223                      |
| Pixel 8                | 0.31                            | 17.83420                     |
| XQ-BC42                | 8.60                            | 0.25214                      |
| SM-S928U1              | 1.29                            | 0.84935                      |
| 23108RN04Y             | 0.73                            | 24.64230                     |
| RMX3888                | 4.76                            | 0.00352                      |
| AC2003                 | 5.01                            | 0.00054                      |
| XQ-FE44                | 5.03                            | 0.00126                      |
| SM-A055F               | 5.01                            | 0.00533                      |
| SM-A546E               | 13.00                           | 0.09983                      |
| SM-A5360               | 0.33                            | 64.54095                     |
| SM-S931N               | 0.52                            | 3.91996                      |
| SM-A346B               | 4.88                            | 0.31226                      |
| M2006C3LG              | 3.02                            | 0.22667                      |
| SM-G950F               | 1.55                            | 0.83093                      |
| SM-S928U               | 2.23                            | 0.55136                      |
| moto g stylus 5G       | 0.26                            | 11.91615                     |
| HD1903                 | 4.51                            | 0.04222                      |
| Pixel 6                | 0.02                            | 202.64260                    |
| 2311DRN14I             | 0.72                            | 8.48191                      |
| I2220                  | 6.27                            | 0.00059                      |
| SM-G998U               | 2.69                            | 0.39164                      |
| I2214                  | 6.25                            | 0.00277                      |
| SM-S156V               | 1.63                            | 1.10944                      |
| SM-A336B               | 6.06                            | 2.88057                      |
| SM-A156B               | 2.83                            | 0.41423                      |
| CPH2591                | 5.01                            | 0.00520                      |
| SM-S921U1              | 1.01                            | 1.82884                      |
| 24122RKC7C             | 1.49                            | 2.45488                      |
| Pixel 8 Pro            | 0.24                            | 30.29632                     |
| motorola edge 50 neo   | 1.68                            | 1.73665                      |
| moto g power 5G - 2023 | 0.16                            | 23.85005                     |
| Pixel 6a               | 0.39                            | 10.50030                     |
| SM-G988B               | 12.63                           | 0.03508                      |
| SM-G991U1              | 0.82                            | 1.54090                      |
| SM-A515F               | 3.97                            | 0.49069                      |
| V2284A                 | 6.42                            | 0.01366                      |
| SM-G998B               | 8.66                            | 0.04203                      |
| moto g84 5G            | 1.21                            | 2.42033                      |
| PJX110                 | 3.87                            | 0.07117                      |
| SM-S908U               | 5.11                            | 0.10324                      |
| SM-A525F               | 6.08                            | 0.00641                      |
| SM-G991U               | 1.47                            | 1.86422                      |
| SM-A145R               | 5.01                            | 0.00050                      |
| SM-G973F               | 1.08                            | 0.75072                      |
| Pixel 9 Pro            | 0.36                            | 5.84277                      |
| SM-A032M               | 12.34                           | 0.00045                      |
| SM-N986N               | 5.44                            | 0.07132                      |
| 220333QNY              | 6.64                            | 0.04995                      |
| SM-A505FN              | 3.16                            | 2.22231                      |
| SM-A156U               | 2.83                            | 0.52705                      |
| CPH2059                | 19.14                           | 0.00007                      |
| SM-A037F               | 4.62                            | 0.00064                      |
| Redmi Note 9 Pro       | 7.95                            | 0.04975                      |
| M2012K11C              | 1.80                            | 1.43789                      |
| 2210132G               | 0.05                            | 127.02228                    |
| MAR-LX3A               | 2.88                            | 0.00372                      |
| PHB110                 | 4.90                            | 0.01384                      |
| SM-S908B               | 6.47                            | 0.05150                      |
| M2007J20CG             | 9.01                            | 0.00011                      |
| RMX3472                | 19.69                           | 0.00027                      |
| CPH2123                | 5.01                            | 0.00133                      |
| SM-A536E               | 16.66                           | 0.04211                      |
| CPH2477                | 5.03                            | 0.00118                      |
| SM-A536B               | 6.83                            | 0.30020                      |
| NE2213                 | 4.91                            | 0.00057                      |
| SM-X218U               | 16.14                           | 0.04696                      |
| 2409BRN2CY             | 3.27                            | 0.35079                      |
| RMX3834                | 199.89                          | 0.67439                      |
| Redmi Note 8           | 8.76                            | 0.04146                      |
| SM-S721B               | 1.62                            | 10.77495                     |
| SM-S911U               | 2.50                            | 0.59542                      |
| Infinix X6831          | 2.28                            | 0.50149                      |
| moto e20               | 1.42                            | 0.82926                      |
| SM-M366B               | 2.41                            | 3.63452                      |
| moto g play - 2024     | 0.05                            | 416.16491                    |
| HBN-LX9                | 2.86                            | 0.00080                      |
| 2312DRA50G             | 0.40                            | 3.56549                      |
| SM-S916B               | 2.99                            | 0.55154                      |
| IN2013                 | 5.01                            | 0.00072                      |
| SM-A405FN              | 9.41                            | 0.02082                      |
| 2310FPCA4G             | 2.69                            | 1.06712                      |
| SM-A032F               | 12.35                           | 0.00016                      |
| SM-A546U1              | 4.04                            | 1.43542                      |
| SM-A035M               | 6.19                            | 0.00023                      |
| B160V                  | 1.40                            | 19.03308                     |
| SM-A556E               | 5.70                            | 3.92271                      |
| SM-A226B               | 6.26                            | 0.00047                      |
| LLY-LX1                | 8.35                            | 0.00021                      |
| IN2023                 | 5.00                            | 0.01226                      |
| Infinix X6833B         | 5.02                            | 0.00909                      |
| SM-G556B               | 7.95                            | 0.14615                      |
| SM-S916U               | 2.43                            | 1.20557                      |
| 2210132C               | 0.14                            | 18.62047                     |
| PGEM10                 | 3.73                            | 1.84850                      |
| M2010J19CG             | 9.01                            | 0.00012                      |
| SM-F926U               | 1.45                            | 0.90306                      |
| 21061119AL             | 0.31                            | 125.93677                    |
| SC-02K                 | 3.40                            | 0.19184                      |
| 2201116SG              | 2.88                            | 0.45885                      |
| M2006C3LII             | 3.63                            | 0.36558                      |
| SM-G780G               | 22.42                           | 0.00551                      |
| SM-S936U               | 2.61                            | 0.37581                      |
| moto g54 5G            | 2.13                            | 0.79746                      |
| A063                   | 16.68                           | 0.00008                      |
| CPH2495                | 5.01                            | 0.00092                      |
| LYA-L29                | 1.14                            | 2.79409                      |
| SM-F946B               | 1.95                            | 3.05298                      |
| RMX2170                | 4.71                            | 0.04547                      |
| SM-G975F               | 1.19                            | 0.21552                      |
| 2107113SG              | 0.51                            | 9.20931                      |
| ZTE Blade A7 2020      | 5.11                            | 0.37088                      |
| TMAF025G               | 5.01                            | 0.00189                      |
| CPH2609                | 4.98                            | 0.01358                      |
| CPH2579                | 5.01                            | 0.00060                      |
| SM-S931U1              | 1.64                            | 0.57371                      |
| SM-S911U1              | 1.25                            | 1.69049                      |
| SM-G965U1              | 0.29                            | 89.84883                     |
| SM-G996B               | 9.36                            | 0.04235                      |
| RMX3997                | 5.01                            | 0.00068                      |
| CPH2387                | 5.05                            | 0.01196                      |
| SM-F936U1              | 5.97                            | 0.03076                      |
| SM-A065M               | 5.01                            | 0.00050                      |
| Pixel 6 Pro            | 0.53                            | 3.92475                      |
| SM-M536B               | 10.89                           | 0.15818                      |
| SM-S921N               | 9.05                            | 0.22625                      |
| RMX3363                | 4.77                            | 0.00258                      |
| SM-A145M               | 6.20                            | 0.20373                      |
| moto g42               | 0.16                            | 20.07641                     |
| SM-A055M               | 5.01                            | 0.00043                      |
| moto e40               | 5.83                            | 0.39447                      |
| CPH2653                | 3.68                            | 0.10737                      |
| SM-A057F               | 6.04                            | 0.00044                      |
| M2101K6G               | 0.67                            | 3.50053                      |
| PJE110                 | 5.00                            | 0.01008                      |
| SM-A042M               | 4.61                            | 0.00023                      |
| SM-F936B               | 1.60                            | 1.02670                      |
| 23117RK66C             | 1.45                            | 1.79038                      |
| SM-G780F               | 15.67                           | 0.03247                      |
| TC78                   | 2.21                            | 0.58330                      |
| SM-A356E               | 7.99                            | 0.26509                      |
| RMX2144                | 5.01                            | 0.00050                      |
| SNE-LX1                | 8.41                            | 0.00027                      |
| SM-A115M               | 7.45                            | 0.00017                      |
| RMX3392                | 5.01                            | 0.00108                      |

# Note on Privacy

At Sensor Logger, user privacy is our top priority. No sensor data ever leaves the device—only high-level diagnostic metrics, such as sampling rates and sensor characteristics are occasionally reported. Personal or identifiable information is never collected.

All data processing happens locally, with only anonymized, aggregated statistics sent to Sensor Logger servers. Specifically, only the mean, minimum, maximum, and standard deviation of sampling rates for enabled sensors are reported. This will happen in the background once or twice during the first few recordings you make.

To further protect privacy, only widely used device models will report these metrics, preventing any link to individual users.

Users can opt out of contributing to this Sampling Reference at any time through the settings. Additionally, study investigators can disable data collection for all participants as part of the Study configuration.
