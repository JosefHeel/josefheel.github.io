---
title: Bachelor's thesis
categories:
- Electronics
- Projects
excerpt: My bachelor's thesis "Technologies for fill level determination" working with optical Time-of-Flight, radar and ultrasonic sensors.
feature_text: |
  ##  <font color='white'> experiments with sensors </font>
feature_image: /assets/pic/bac/banner.jpg
aside: true
---

#### Abstract
The potential of optical Time-of-Flight (ToF), radar and ultrasonic technology for fill level determination is discussed using the examples VL53L1X from ST, A111 from Acconeer and PGA460 from TI. This work is carried out in cooperation with SLOC GmbH, which specializes in the waste industry. A firmware implementation for the VL53L1X sensor based on the MAINT3 driver from ST is realized on an STM32 Cortex M4. To provide an easy-to-use solution for SLOC, a compact abstraction layer is written on top. With the ToF-sensor, tests including range, accuracy, opening angle, deadband behaviour, effects of pollution, reflectivity of materials, 3D-view, power consumption, metal detection and real-world use cases are carried out. Some tests are repeated with radar and/or ultrasonic sensor. From the gathered data, it can be concluded that the ToF-sensor delivers a stable performance in proximity < 1 m. For greater distances, however, it depends on many parameters such as ambient light and target texture if a measurement succeeds. Radar and ultrasonic are more comparable as they both have issues with very close objects, although radar can be focused with plastic lenses as opposed to ultrasonic.

#### A comment
This is my bachelor's thesis which I did in cooperation with the company [SLOC](https://www.sloc.one/) which I've been working for in the last two years. The main document is confidential to SLOC, but I'm allowed to give an overview here. The project was interesting in a way that that I had to get familiar with a large piece of software, the official driver for the VL53L1X with limited documentation as we were using the latest version of it.

There was also the need to acquire a large amount of measurement data points (over 10k in total, although a lot of it is just for completeness) to characterize the sensor's performance in a variety of different scenarios like lighting conditions, target materials and so on. The only practical way to achieve this was to write a little GUI (using python and wxWidgets) that would allow easy manipulation of the most important settings, read the values including status information and so on from the sensor and automatically dump them in a file.

Then, numpy and matplotlib were used to extract relevant information from the dataset an create nice illustrations. In the end, we were able to generate a lot of information on how the sensor would behave in some typical use-cases that SLOC specializes in.

#### Impressions

![Measurements at real wastebins out in the street](/assets/pic/bac/bins.jpg)
Making measurements at real wastebins out in the street.

![Opening angle measurements on optical breadboard](/assets/pic/bac/angle.jpg)
Determining the opening angle on an optical breadboard in the lab.

![Radar sensor with plastic lense](/assets/pic/bac/radar.jpg)
Radar sensor with plastic lens holder to focus the beam.

![Effects of tilted slopes](/assets/pic/bac/3dtof.jpg)
Effects of tilted slopes on the result of the ToF-sensor.

![Python program to help with data acquisition](/assets/pic/bac/tof_tester.png)
Python GUI that helped with  data acquisition.

{% include button.html text="Drop me an Email" link="mailto:website.jheel@gmail.com" %}

<!-- more -->
