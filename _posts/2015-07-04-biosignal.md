---
title: Audiovisual muscle therapy device
categories:
- Electronics
- Projects
excerpt: |
  An assistant device for muscle training with acoustic feedback.
feature_text: |
  #  <font color='white'> Measuring electrical muscle signals  </font>
feature_image: /assets/pic/biosignal/banner.jpg
---

#### Introduction
The aim of this project was to design and manufacture a device that helps children to regain their muscle functionality after an injury. The project was carried out at the technical college (HTL) in cooperation with the NGO "Give children a chance", where one of our teachers is involved.

The basic principle of operation is such that the electrical muscle signal is measured using adhesive electrodes. This signal is then processed and displayed together with a reference waveform that the patient is supposed to match as good as possible. During this training, music is played using headphones. If the deviation from the reference waveform to the actual muscle contraction exceeds a threshold, the music is distorted. In this sense, additional acoustic feedback is given to the user creating a motivation to "keep the music going".

#### Hardware and signal processing
The whole setup consists of the electrode connections with integrated preamplifier, the main device, a USB-Stick containing music files and a small USB powerbank as energy source. It is important to use a battery-based supply and not connect it to a power socket because of safety reasons.
![Overall setup of therapy device](/assets/pic/biosignal/setup.jpg)

Two electrodes have to be glued directly above the muscle that should be trained, for example the biceps. A third one needs to be placed somewhere else on the body, providing "active ground", basically cancelling common mode noise. The weak signal is first amplified using an INA118 instrumentation amplifier. On a Cypress PSoC 5LP board, the signal is then amplified, digitized, rectified and filtered in software to produce a signal which is (very roughly) proportional to muscle tension. The designed PCB furthermore includes an audio amplifier and some passive filtering of the signal from the preamp.
![Connection electrodes on arm](/assets/pic/biosignal/Hand.jpg)

The sides of the device contain the connectors as well as the volume control for the headphone jack. Music files stored on an USB stick can be selected and played via the Raspberry Pi.
![Back of device with connectors](/assets/pic/biosignal/Connectors.png)
![Front of device with volume control](/assets/pic/biosignal/volume.png)

#### Raspberry Pi and software
The processed data is passed from the PSoC to the Raspberry Pi via a UART connection. The data rate is not very high as the filtered signal has quite low bandwidth. The software runs on the Raspberry Pi and allows easy interaction with the device via the touchscreen. It is work of my friend [Simon Kaufmann](https://www.simonkaufmann.org/).

![Main screen](/assets/pic/biosignal/software1.png)
![In operation](/assets/pic/biosignal/software2.png)

#### Result
We demonstrated this device at a "project fair" and also participated at the 2015 "jugend innovativ" design competition, where we were invited to the semi-finals in Dornbirn. Finally, the device was packed up and shipped to Uganda in the summer after the school year ended.

{% include button.html text="Drop me an Email" link="mailto:website.jheel@gmail.com" %}
