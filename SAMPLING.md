# Sampling Reference

Sampling frequency and consistency of sensors vary from device to device, and from platform to platform. Even identical devices may log at variable rates, influenced by factors such as the device’s condition, running apps, and specific settings like low power mode. This reference is based on  sampling frequencies as reported by real Sensor Logger across a diverse user base to offer a better understanding of sampling rates for common phone models in real-world conditions.

This information is especially useful for research groups or organizations looking to purchase devices for running Sensor Logger. With data on how different models perform in actual use, you can make more informed purchasing decisions to ensure you choose devices with the best sensor performance for your specific needs.

# Definitions

## Zero-Gap Sensors

In Sensor Logger, Zero-Gap Sensors are those which Sensor Logger can and will try to sample as frequently as possible, **without any gap between successive requests**. This means the **sampling rate will be up against the hardware and operating system limitations**. 

- `Median Achievable Sampling` is the median sampling frequency, in Hz, across the relevant Sensor Logger recording sessions.
- `Median Minimum Sampling` is the median of minimum sampling frequency, in Hz, across the relevant Sensor Logger recording sessions.
- `Median Maximum Sampling` is the median of maximum sampling frequency, in Hz, across the relevant Sensor Logger recording sessions.
- `Sampling Gap Variability` the standard deviation of sampling gap *within* a recording session, aggregated across all relevant Sensor Logger recording sessions. This is in seconds.

Zero-Gap Sensors include: *location, barometer, accelerometer, gravity, gyroscope, magnetometer, orientation and light*. 

While a higher sampling rate and lower variability are generally considered better, it’s important to remember that a high sampling rate doesn't always equate to more accurate data. In some cases, it can introduce more noise. Additionally, some devices might report at a lower effective sampling rate due to built-in signal processing from the operating system, which can actually improve accuracy. Therefore, it’s crucial to consider both the sampling rate and the quality of the signal processing when evaluating devices.

## Other Sensors

For other sensors, Sensor Logger has built in delays between successive requests. These sensors are excluded. 

# Results

To lookup iPhone model names, you may use https://reincubate.com/lookup/. For Android, you may consider using [https://www.gsmarena.com/](https://www.gsmarena.com/). 

_Last Updated in January 2025._

### Location

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 0.48982 | 0.11111 | 6.21244 | 2.22693 |
| iPhone13,4                   | 0.84175 | 0.09799 | 156.91418 | 1.33552 |
| iPhone14,5                   | 0.92886 | 0.12688 | 2.45734 | 0.91648 |
| Pixel 7                      | 1.00669 | 0.26572 | 4.03962 | 0.47317 |
| iPhone13,2                   | 0.95272 | 0.14381 | 3.55505 | 0.82259 |
| iPhone16,2                   | 0.72552 | 0.11637 | 4.01673 | 1.96738 |
| iPhone9,3                    | 0.80576 | 0.05837 | 3.33919 | 1.79299 |
| iPhone14,6                   | 0.63021 | 0.09360 | 2.93455 | 2.13139 |
| Pixel 7a                     | 1.00199 | 0.33631 | 1.78543 | 0.26739 |
| iPhone14,7                   | 0.74749 | 0.10000 | 27.96985 | 1.62084 |
| iPhone12,8                   | 0.67405 | 0.11111 | 2.29527 | 1.72501 |
| iPhone12,1                   | 0.78446 | 0.08433 | 29.94190 | 1.92056 |
| iPhone14,3                   | 0.65451 | 0.11111 | 3.05253 | 2.20215 |
| iPhone13,1                   | 0.43478 | 0.07244 | 10.24206 | 2.70092 |
| iPhone13,3                   | 0.62337 | 0.07482 | 2.35710 | 2.45642 |
| iPhone17,2                   | 0.69024 | 0.15594 | 215.17209 | 2.01109 |
| SM-S928B                     | 0.97923 | 0.34439 | 1.00099 | 0.27207 |
| SM-S911B                     | 1.01428 | 0.47034 | 6.77880 | 0.35288 |
| iPhone12,3                   | 0.97681 | 0.13774 | 2.26182 | 0.43737 |
| iPhone10,6                   | 0.55680 | 0.08019 | 2.33312 | 2.12088 |
| iPhone15,3                   | 0.46853 | 0.09759 | 2.72426 | 2.41357 |
| iPhone14,8                   | 0.83609 | 0.13972 | 39.76758 | 1.53637 |
| iPhone11,8                   | 0.72531 | 0.07240 | 21.93199 | 2.16929 |
| iPhone14,2                   | 0.93234 | 0.11909 | 2.68688 | 0.85260 |
| iPhone16,1                   | 0.64832 | 0.10931 | 3.11740 | 2.15568 |
| Pixel 6a                     | 1.04637 | 0.19435 | 23.40946 | 0.39424 |
| Pixel 7 Pro                  | 0.84844 | 0.17428 | 5.79086 | 0.68772 |
| iPhone15,4                   | 0.71737 | 0.10500 | 3.07743 | 2.06554 |
| iPhone15,5                   | 0.89336 | 0.12500 | 27.69987 | 1.17979 |
| iPhone12,5                   | 0.77632 | 0.11107 | 2.32989 | 1.99155 |
| SM-A546E                     | 1.15747 | 0.34836 | 181.09321 | 0.46518 |
| iPhone14,4                   | 0.70590 | 0.08519 | 25.68060 | 2.24232 |
| Pixel 8                      | 1.03550 | 0.43376 | 13.54160 | 0.32302 |
| SM-S921B                     | 0.98868 | 0.27398 | 13.46590 | 0.56728 |
| SM-A546B                     | 1.06393 | 0.17996 | 165.39284 | 0.31420 |
| SM-A528B                     | 1.00232 | 0.60935 | 1.48780 | 0.20847 |
| iPhone11,2                   | 0.38915 | 0.04444 | 35.02609 | 4.12993 |
| SM-S918B                     | 1.01459 | 0.56418 | 1.22359 | 0.25528 |
| iPhone17,1                   | 0.31796 | 0.07008 | 65.22810 | 3.73621 |


### Barometer

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 0.97335 | 0.93526 | 2.87960 | 0.11740 |
| iPhone13,4                   | 1.01321 | 0.94068 | 2.81471 | 0.15413 |
| iPhone14,5                   | 0.95202 | 0.93656 | 2.85267 | 0.07570 |
| Pixel 7                      | 39.92091 | 39.79553 | 39.92121 | 0.00003 |
| iPhone13,2                   | 0.94138 | 0.93482 | 2.86237 | 0.04409 |
| iPhone16,2                   | 1.03111 | 0.94092 | 2.84297 | 0.17722 |
| iPhone9,3                    | 1.09626 | 0.98147 | 6.18292 | 0.12424 |
| iPhone14,6                   | 1.08945 | 0.97893 | 6.37625 | 0.12297 |
| Pixel 7a                     | 39.98313 | 39.86580 | 39.97862 | 0.00003 |
| iPhone14,7                   | 0.95414 | 0.93794 | 2.86608 | 0.10084 |
| iPhone12,8                   | 1.00017 | 0.99691 | 1.82090 | 0.01819 |
| iPhone12,1                   | 1.00361 | 0.99897 | 1.81504 | 0.03027 |
| iPhone14,3                   | 0.97244 | 0.93902 | 5.03754 | 0.11467 |
| iPhone13,1                   | 1.01782 | 0.93575 | 2.82958 | 0.15385 |
| iPhone13,3                   | 0.98079 | 0.93609 | 2.86464 | 0.12299 |
| iPhone17,2                   | 1.13922 | 0.94270 | 2.80717 | 0.19199 |
| SM-S928B                     | 25.02503 | 24.99072 | 25.00928 | 0.00005 |
| SM-S911B                     | 25.02503 | 24.93553 | 25.06014 | 0.00005 |
| iPhone12,3                   | 1.04272 | 0.99942 | 1.81504 | 0.07982 |
| iPhone10,6                   | 1.06701 | 0.97039 | 6.53257 | 0.06629 |
| iPhone15,3                   | 1.05805 | 0.94001 | 2.83093 | 0.19151 |
| iPhone14,8                   | 0.97633 | 0.93785 | 2.80492 | 0.09694 |
| iPhone11,8                   | 1.05335 | 0.97454 | 6.24921 | 0.03762 |
| iPhone14,2                   | 0.99126 | 0.93598 | 2.83539 | 0.13008 |
| iPhone16,1                   | 1.00696 | 0.93765 | 2.83668 | 0.14636 |
| Pixel 6a                     | 50.05056 | 49.01930 | 52.39772 | 0.00025 |
| Pixel 7 Pro                  | 39.92175 | 39.77365 | 39.90775 | 0.00004 |
| iPhone15,4                   | 0.99267 | 0.93895 | 3.93787 | 0.14041 |
| iPhone15,5                   | 0.99834 | 0.93623 | 2.81252 | 0.11595 |
| iPhone12,5                   | 1.01193 | 0.99942 | 1.81504 | 0.04219 |
| iPhone14,4                   | 0.95660 | 0.93150 | 2.86904 | 0.08850 |
| Pixel 8                      | 39.91876 | 39.78256 | 39.92121 | 0.00003 |
| SM-S921B                     | 12.58081 | 12.48674 | 12.51939 | 0.00029 |
| iPhone11,2                   | 1.07344 | 0.99362 | 1.83216 | 0.11044 |
| SM-S918B                     | 25.04980 | 24.91485 | 25.09057 | 0.00010 |
| iPhone17,1                   | 1.05112 | 0.94038 | 4.98187 | 0.20595 |


### Accelerometer

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 100.11593 | 99.98080 | 100.01408 | 0.00001 |
| iPhone13,4                   | 100.04407 | 99.88621 | 99.90665 | 0.00001 |
| iPhone14,5                   | 100.44015 | 100.10379 | 100.35067 | 0.00001 |
| Pixel 7                      | 77.45032 | 76.97120 | 77.63050 | 0.00003 |
| iPhone13,2                   | 99.82110 | 99.70010 | 99.72810 | 0.00001 |
| iPhone16,2                   | 100.41671 | 100.29913 | 100.32232 | 0.00001 |
| iPhone9,3                    | 100.27167 | 99.64716 | 100.21293 | 0.00003 |
| iPhone14,6                   | 100.11364 | 99.94901 | 100.44875 | 0.00002 |
| Pixel 7a                     | 59.79380 | 59.60601 | 59.85352 | 0.00002 |
| iPhone14,7                   | 100.27049 | 100.14742 | 100.18338 | 0.00001 |
| iPhone12,8                   | 99.90141 | 99.74975 | 99.80199 | 0.00001 |
| iPhone12,1                   | 99.95265 | 99.79944 | 99.88110 | 0.00001 |
| iPhone14,3                   | 100.18939 | 100.03039 | 100.05087 | 0.00001 |
| iPhone13,1                   | 100.57567 | 100.44614 | 100.47715 | 0.00001 |
| iPhone13,3                   | 100.64190 | 100.51334 | 100.54439 | 0.00001 |
| iPhone17,2                   | 99.84359 | 99.70774 | 99.72810 | 0.00001 |
| SM-S928B                     | 199.75031 | 61.53804 | 200.00256 | 0.00036 |
| SM-S911B                     | 208.89578 | 64.39104 | 209.16441 | 0.00034 |
| iPhone12,3                   | 100.61341 | 100.47228 | 100.55249 | 0.00001 |
| iPhone10,6                   | 99.32766 | 99.21643 | 99.24164 | 0.00001 |
| iPhone15,3                   | 100.19242 | 100.03713 | 100.07814 | 0.00001 |
| iPhone14,8                   | 100.50059 | 100.38032 | 100.39838 | 0.00001 |
| iPhone11,8                   | 99.77979 | 99.64415 | 99.72174 | 0.00001 |
| iPhone14,2                   | 100.03007 | 99.87855 | 99.91176 | 0.00001 |
| iPhone16,1                   | 100.09173 | 99.95010 | 100.01408 | 0.00001 |
| Pixel 6a                     | 72.41042 | 63.71821 | 72.43790 | 0.00002 |
| Pixel 7 Pro                  | 79.20964 | 59.41517 | 79.45508 | 0.00017 |
| iPhone15,4                   | 99.87033 | 99.72810 | 99.75102 | 0.00001 |
| iPhone15,5                   | 100.00147 | 99.88876 | 99.91048 | 0.00001 |
| iPhone12,5                   | 100.22337 | 100.07814 | 100.15769 | 0.00001 |
| SM-A546E                     | 124.06082 | 62.06773 | 478.88500 | 0.00057 |
| iPhone14,4                   | 100.23669 | 100.02945 | 100.06020 | 0.00001 |
| Pixel 8                      | 99.28057 | 66.15605 | 99.63144 | 0.00016 |
| SM-S921B                     | 125.04722 | 117.82384 | 125.18033 | 0.00002 |
| SM-A528B                     | 207.55524 | 15.56182 | 210.25082 | 0.00188 |
| iPhone11,2                   | 99.66097 | 99.52483 | 99.60604 | 0.00001 |
| SM-S918B                     | 209.36822 | 65.45544 | 209.30451 | 0.00033 |
| iPhone17,1                   | 100.59835 | 100.39709 | 100.41516 | 0.00002 |


### Gravity

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 100.11593 | 99.97824 | 100.02689 | 0.00001 |
| iPhone13,4                   | 100.67552 | 100.56510 | 100.59358 | 0.00001 |
| iPhone14,5                   | 100.45485 | 100.34035 | 100.38935 | 0.00001 |
| Pixel 7                      | 232.02893 | 173.20585 | 233.99132 | 0.00007 |
| iPhone13,2                   | 99.82110 | 99.70010 | 99.72810 | 0.00001 |
| iPhone16,2                   | 100.03632 | 99.92709 | 99.95010 | 0.00001 |
| iPhone14,6                   | 100.11364 | 99.94901 | 99.97456 | 0.00002 |
| Pixel 7a                     | 241.42578 | 79.46963 | 297.55104 | 0.00030 |
| iPhone14,7                   | 100.30281 | 100.15640 | 100.22579 | 0.00001 |
| iPhone12,8                   | 99.88820 | 99.76503 | 99.82240 | 0.00001 |
| iPhone12,1                   | 100.24836 | 100.09866 | 100.18338 | 0.00001 |
| iPhone14,3                   | 100.54015 | 100.33778 | 100.35582 | 0.00001 |
| iPhone13,1                   | 100.57587 | 100.45002 | 100.49136 | 0.00001 |
| iPhone13,3                   | 99.96230 | 99.84591 | 99.87144 | 0.00001 |
| iPhone17,2                   | 99.84359 | 99.70774 | 99.72810 | 0.00001 |
| SM-S928B                     | 199.75030 | 61.53804 | 200.00256 | 0.00036 |
| SM-S911B                     | 208.90454 | 64.38838 | 209.17001 | 0.00034 |
| iPhone12,3                   | 100.61341 | 100.47228 | 100.55249 | 0.00001 |
| iPhone10,6                   | 99.32766 | 99.21643 | 99.24164 | 0.00001 |
| iPhone15,3                   | 100.43044 | 100.08327 | 100.27339 | 0.00002 |
| iPhone14,8                   | 100.49643 | 100.37387 | 100.39193 | 0.00001 |
| iPhone11,8                   | 99.73460 | 99.57049 | 99.67975 | 0.00001 |
| iPhone14,2                   | 99.80547 | 99.63907 | 99.65940 | 0.00001 |
| iPhone16,1                   | 100.08529 | 99.94755 | 100.00128 | 0.00001 |
| Pixel 6a                     | 218.02766 | 216.02975 | 218.88659 | 0.00001 |
| Pixel 7 Pro                  | 237.14336 | 79.32366 | 243.77724 | 0.00028 |
| iPhone15,4                   | 100.12409 | 99.97313 | 99.99616 | 0.00001 |
| iPhone15,5                   | 99.67020 | 99.56034 | 99.58065 | 0.00001 |
| iPhone12,5                   | 100.22337 | 100.07814 | 100.15769 | 0.00001 |
| SM-A546E                     | 124.18506 | 61.79504 | 498.37331 | 0.00058 |
| iPhone14,4                   | 100.09596 | 99.97057 | 100.00640 | 0.00001 |
| Pixel 8                      | 198.46314 | 99.29972 | 200.18736 | 0.00016 |
| SM-A528B                     | 207.57614 | 15.63801 | 210.25648 | 0.00187 |
| iPhone11,2                   | 99.66097 | 99.52483 | 99.61366 | 0.00001 |
| SM-S918B                     | 209.36822 | 65.12913 | 209.30451 | 0.00034 |
| iPhone17,1                   | 100.59835 | 100.39709 | 100.41516 | 0.00002 |


### Gyroscope

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 100.10326 | 99.88621 | 100.02433 | 0.00001 |
| iPhone13,4                   | 100.04407 | 99.88621 | 99.90665 | 0.00001 |
| iPhone14,5                   | 100.45168 | 100.29656 | 100.36098 | 0.00001 |
| Pixel 7                      | 471.24958 | 336.11901 | 485.64408 | 0.00004 |
| iPhone13,2                   | 99.82225 | 99.70901 | 99.73447 | 0.00001 |
| iPhone16,2                   | 100.38403 | 100.27081 | 100.29398 | 0.00001 |
| iPhone9,3                    | 100.27167 | 99.64716 | 100.21293 | 0.00003 |
| iPhone14,6                   | 100.11364 | 99.94901 | 99.97456 | 0.00002 |
| Pixel 7a                     | 480.77546 | 235.47630 | 490.56862 | 0.00007 |
| iPhone14,7                   | 100.26607 | 100.13971 | 100.18081 | 0.00001 |
| iPhone12,8                   | 99.89865 | 99.74083 | 99.79179 | 0.00001 |
| iPhone12,1                   | 100.14188 | 100.00393 | 100.07313 | 0.00001 |
| iPhone14,3                   | 100.44878 | 100.33520 | 100.35582 | 0.00001 |
| iPhone13,1                   | 100.57606 | 100.45131 | 100.49266 | 0.00001 |
| iPhone13,3                   | 100.64313 | 100.53145 | 100.55474 | 0.00001 |
| iPhone17,2                   | 99.84359 | 99.70774 | 99.72810 | 0.00001 |
| SM-S928B                     | 471.44553 | 470.93472 | 471.02026 | 0.00000 |
| SM-S911B                     | 418.74920 | 418.27283 | 418.40724 | 0.00000 |
| iPhone12,3                   | 100.61341 | 100.47228 | 100.55249 | 0.00001 |
| iPhone10,6                   | 99.32766 | 99.21643 | 99.24164 | 0.00001 |
| iPhone15,3                   | 100.20568 | 100.05251 | 100.10122 | 0.00001 |
| iPhone14,8                   | 100.49643 | 100.37387 | 100.39193 | 0.00001 |
| iPhone11,8                   | 99.77342 | 99.63653 | 99.71028 | 0.00001 |
| iPhone14,2                   | 99.80547 | 99.63907 | 99.65940 | 0.00001 |
| iPhone16,1                   | 100.07139 | 99.94371 | 99.98720 | 0.00001 |
| Pixel 6a                     | 436.49270 | 390.66407 | 448.73636 | 0.00002 |
| Pixel 7 Pro                  | 476.49231 | 275.64848 | 583.10171 | 0.00005 |
| iPhone15,4                   | 99.96340 | 99.72810 | 99.75102 | 0.00001 |
| iPhone15,5                   | 100.00147 | 99.88876 | 99.91048 | 0.00001 |
| iPhone12,5                   | 100.22086 | 100.07686 | 100.14870 | 0.00001 |
| SM-A546E                     | 495.79232 | 307.07098 | 1202.29301 | 0.00057 |
| iPhone14,4                   | 100.18123 | 100.05771 | 100.09101 | 0.00001 |
| Pixel 8                      | 397.34829 | 390.82041 | 405.29674 | 0.00001 |
| SM-S921B                     | 499.45972 | 166.72002 | 500.86550 | 0.00013 |
| SM-A528B                     | 840.80090 | 824.27727 | 841.32027 | 0.00001 |
| iPhone11,2                   | 99.66097 | 99.52483 | 99.60604 | 0.00001 |
| SM-S918B                     | 420.98520 | 420.49071 | 420.62703 | 0.00000 |
| iPhone17,1                   | 100.59918 | 100.39709 | 100.41645 | 0.00002 |


### Magnetometer

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 100.45342 | 100.33778 | 100.36098 | 0.00001 |
| iPhone13,4                   | 99.42169 | 99.26187 | 99.28206 | 0.00001 |
| iPhone14,5                   | 100.03172 | 99.92198 | 100.35067 | 0.00001 |
| Pixel 7                      | 100.10012 | 99.58826 | 100.37129 | 0.00001 |
| iPhone13,2                   | 99.82099 | 99.70010 | 99.72301 | 0.00001 |
| iPhone16,2                   | 100.40914 | 100.29398 | 100.31716 | 0.00001 |
| iPhone14,6                   | 100.11364 | 99.94901 | 99.97456 | 0.00002 |
| Pixel 7a                     | 100.09988 | 99.52483 | 100.57286 | 0.00002 |
| iPhone14,7                   | 100.32144 | 99.63398 | 100.23222 | 0.00001 |
| iPhone12,8                   | 99.85097 | 99.58318 | 99.63398 | 0.00001 |
| iPhone12,1                   | 100.02719 | 99.84791 | 99.89387 | 0.00001 |
| iPhone14,3                   | 99.64027 | 99.52990 | 99.55019 | 0.00001 |
| iPhone13,1                   | 100.39519 | 100.00896 | 100.02176 | 0.00001 |
| iPhone13,3                   | 99.72261 | 99.60985 | 99.63526 | 0.00001 |
| iPhone17,2                   | 99.80505 | 99.65686 | 99.68356 | 0.00001 |
| SM-S928B                     | 100.10010 | 99.99872 | 100.00128 | 0.00001 |
| SM-S911B                     | 100.10010 | 99.99872 | 100.00128 | 0.00001 |
| iPhone15,3                   | 100.63681 | 100.52110 | 100.54439 | 0.00001 |
| iPhone14,8                   | 100.50577 | 100.39709 | 100.41516 | 0.00001 |
| iPhone14,2                   | 99.67683 | 99.56034 | 99.58572 | 0.00001 |
| iPhone16,1                   | 100.16521 | 100.05251 | 100.07430 | 0.00001 |
| Pixel 6a                     | 100.10009 | 99.80454 | 100.21165 | 0.00001 |
| Pixel 7 Pro                  | 100.10013 | 99.50201 | 100.48232 | 0.00001 |
| iPhone15,4                   | 100.30315 | 100.19108 | 100.21936 | 0.00001 |
| iPhone12,5                   | 100.21835 | 100.07814 | 100.15769 | 0.00001 |
| SM-A546E                     | 121.65953 | 110.06932 | 135.45965 | 0.00028 |
| iPhone14,4                   | 99.41506 | 99.30349 | 99.33001 | 0.00001 |
| Pixel 8                      | 100.09989 | 99.50201 | 100.56251 | 0.00002 |
| SM-S921B                     | 125.03487 | 62.51600 | 125.27661 | 0.00025 |
| SM-A528B                     | 100.10010 | 99.99872 | 100.00384 | 0.00001 |
| iPhone11,2                   | 100.58250 | 100.35840 | 100.47973 | 0.00002 |
| SM-S918B                     | 100.10010 | 99.99872 | 100.00128 | 0.00001 |
| iPhone17,1                   | 100.06617 | 94.09023 | 99.98592 | 0.00002 |


### Orientation

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| iPhone15,2                   | 100.27516 | 100.09096 | 100.35324 | 0.00001 |
| iPhone13,4                   | 99.74771 | 99.61314 | 99.63473 | 0.00001 |
| iPhone14,5                   | 100.12464 | 100.01664 | 100.31716 | 0.00001 |
| Pixel 7                      | 235.61654 | 229.94173 | 237.18451 | 0.00001 |
| iPhone13,2                   | 99.82099 | 99.70010 | 99.72301 | 0.00001 |
| iPhone16,2                   | 99.98899 | 99.67721 | 99.91431 | 0.00001 |
| iPhone14,6                   | 100.11364 | 99.94901 | 99.97456 | 0.00002 |
| Pixel 7a                     | 238.38256 | 67.45433 | 243.95905 | 0.00113 |
| iPhone14,7                   | 100.27278 | 100.15127 | 100.18595 | 0.00001 |
| iPhone12,8                   | 99.87224 | 99.75866 | 99.81219 | 0.00001 |
| iPhone12,1                   | 100.05819 | 99.85812 | 99.93221 | 0.00001 |
| iPhone14,3                   | 100.54015 | 100.43065 | 100.44614 | 0.00001 |
| iPhone13,1                   | 100.47426 | 100.36614 | 100.38419 | 0.00001 |
| iPhone13,3                   | 100.06762 | 99.87610 | 99.89654 | 0.00001 |
| iPhone17,2                   | 99.80505 | 99.65686 | 99.68356 | 0.00001 |
| SM-S928B                     | 200.20021 | 199.99232 | 200.00256 | 0.00000 |
| SM-S911B                     | 209.37474 | 209.15881 | 209.17001 | 0.00000 |
| iPhone10,6                   | 99.32766 | 99.21643 | 99.24164 | 0.00001 |
| iPhone15,3                   | 100.48559 | 100.26566 | 100.28497 | 0.00002 |
| iPhone14,8                   | 100.51120 | 100.39709 | 100.41516 | 0.00001 |
| iPhone11,8                   | 99.73460 | 99.57049 | 99.67975 | 0.00001 |
| iPhone14,2                   | 99.77263 | 99.57303 | 99.59334 | 0.00001 |
| iPhone16,1                   | 100.13051 | 99.99744 | 100.04483 | 0.00001 |
| Pixel 6a                     | 218.24933 | 216.50336 | 219.16325 | 0.00001 |
| Pixel 7 Pro                  | 237.57083 | 118.97329 | 240.07437 | 0.00013 |
| iPhone15,4                   | 99.86706 | 99.72810 | 99.75102 | 0.00001 |
| iPhone12,5                   | 100.22086 | 100.07686 | 100.14870 | 0.00001 |
| SM-A546E                     | 124.18506 | 61.79504 | 498.37331 | 0.00058 |
| iPhone14,4                   | 100.09596 | 99.97057 | 100.00640 | 0.00001 |
| Pixel 8                      | 198.46238 | 99.29972 | 200.18736 | 0.00016 |
| SM-S921B                     | 125.16014 | 111.15300 | 125.27661 | 0.00003 |
| SM-A528B                     | 210.13659 | 206.08019 | 210.25082 | 0.00002 |
| iPhone11,2                   | 100.06975 | 99.87324 | 99.99341 | 0.00001 |
| SM-S918B                     | 209.36822 | 209.01332 | 209.30451 | 0.00000 |
| iPhone17,1                   | 100.06617 | 84.65348 | 99.98592 | 0.00007 |


### Light

| Sensor Model                | Median Achievable Sampling | Median Minimum Sampling | Median Maximum Sampling | Sampling Gap Variability |
|-----------------------------|----------------------------|--------------------------|--------------------------|--------------------------|
| Pixel 7                      | 0.54304 | 0.01121 | 40.62754 | 8.56226 |
| Pixel 7a                     | 0.11954 | 0.01750 | 5.54537 | 18.42949 |
| SM-S928B                     | 2.57701 | 0.25000 | 6.25050 | 0.49011 |
| SM-S911B                     | 1.72331 | 0.23148 | 6.25082 | 0.94069 |
| Pixel 6a                     | 0.48509 | 0.09632 | 6.00367 | 2.69873 |
| Pixel 7 Pro                  | 0.47373 | 0.16975 | 3.38012 | 1.99695 |
| SM-A546E                     | 6.68102 | 0.09366 | 42.55545 | 0.42235 |
| Pixel 8                      | 0.28631 | 0.00559 | 27.26125 | 23.79286 |
| SM-S921B                     | 6.18961 | 0.49988 | 25.02194 | 0.25159 |
| SM-A546B                     | 14.49665 | 1.38653 | 38.91895 | 0.06322 |
| SM-A528B                     | 6.30572 | 6.24961 | 8.33388 | 0.00569 |
| SM-S918B                     | 2.74823 | 0.66288 | 6.25028 | 0.60444 |

# Note on Privacy

At Sensor Logger, user privacy is our top priority. No sensor data ever leaves the device—only high-level diagnostic metrics, such as sampling rates and sensor characteristics are occasionally reported. Personal or identifiable information is never collected. 

All data processing happens locally, with only anonymized, aggregated statistics sent to Sensor Logger servers. Specifically, only the mean, minimum, maximum, and standard deviation of sampling rates for enabled sensors are reported. This will happen in the background once or twice during the first few recordings you make. 

To further protect privacy, only widely used device models will report these metrics, preventing any link to individual users.

Users can opt out of contributing to this Sampling Reference at any time through the settings. Additionally, study investigators can disable data collection for all participants as part of the Study configuration.
