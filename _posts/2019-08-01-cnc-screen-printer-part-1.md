---
title: CNC from Screenprinter - Part 1
categories:
- CNC
excerpt: Beginning of a big project converting an industrial screen prining machine into a hobby CNC-machine.
feature_text: |
  ##  <font color='white'> Homemade CNC router ventures </font>
feature_image: /assets/pic/cnc/cnc_banner.png
aside: true
---

#### How it all started
CNC machines have always fascinated me, from as early on as I knew they existed. I've [build one](/cnc/projects/2013/10/20/first-cnc/) from wood and drawer slides some time ago, but it that was more or less just an experiment and not of much practical use. Professional components,  such as proper linear rails, ballscrews, servo motors and so on are, however, a bit expensive for the hobbyist. So for quite a few years now I've been waiting for the ideal opportunity to get my hands on some old used equipment that could be repurposed.

And now, it just so happened that at my good friend's company, they would throw out what was an old industrial screen printing machine for conductive paint or something similar. My friend sent me a couple of pictures, and we concluded that this was a decent base for a hobby CNC-project. So one nice day, we were allowed to haul the machine away alongside with a few other goodies including extra linear rails, the original electric cabinet and some old power supplies that were not needed there anymore. Huge thanks to the very generous boss of this company, I must say!

![Machine and other pieces we got basically for free](/assets/pic/cnc/screen_printing_machine.jpg)

It might not be obvious from the above picture, but this haul contains almost anything needed for a light-duty hobby CNC-machine:
- Proper linear rails (only 16mm wide ones, but hey)
- three stepper motors with encoders that could be configured as closed-loop
- enclosed industrial-quality linear axis (belt-based, though, more about that later)
- Enough 12mm aluminium plate material to cut parts for Z-axis output
- Machine base, already in a gantry-style
- all sorts of accessories like electric components, limit switches...
- cable chains, mounting brackets etc. etc.
- The original stepper drivers (DAC1005 from LPKF motion, more about those later)

What is still missing:
- A spindle motor with collets
- the Z-axis (there was no need for precise Z-movement on the screen printer)
- the control electronics and PC

So now that the machine has successfully been transferred to my small basement workshop, a huge amount of questions arises. How to reuse the available parts most efficiently and still have a acceptable machine? How to do the z-Axis? What to use as a spindle motor?

The following blog posts in this [series](/cnc/2019/10/01/cnc-screen-printer-part-2/) will document some of the steps in this project, problems that were encountered and experiences which were made. Enjoy!


{% include button.html text="Drop me an Email" link="mailto:website.jheel@gmail.com" %}

<!-- more -->
