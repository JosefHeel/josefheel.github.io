---
title: Experiments with Universal PMAC-lite
categories:
- CNC
excerpt: Experiments reusing the old control system from an industrial dispenser machine to repurpose it as a hobby CNC-machine.
feature_image: "../assets/cnc_banner.png"
---

Recently, a friend of mine acquired quite a massive industrial dispenser machine or something similar, I am not 100% sure what it even did exactly. This machine was given to him for free, or, for the expense of bringing to his workshop, so to say, which is not so negligible.

It is my friend's and my plan to convert this machine in a CNC-machine for light-duty machining (aluminum and such). However, we do not want to spend too much
money on the project, because the machine is quite old and also not the ideal CNC-machine in some ways. So it would be nice to be able to reuse the old control system of the machine. The heart is an ISA-Card specifically designed for this purpose, the so-called "Universal PMAC-lite".

Luckily, the documentation is still available. This card is able to do all sorts of complex motion operations such as jerk limitation, max-acceleration-limiting with look-ahead-feature, transformations between different coordinate systems, etc. etc. on 8 axis synchronously. So is quite a beast and certainly overkill for what we would like to do it.

Luckily, when making a test connection via the RS232-Port, the card proved to still be working just fine! Unfortunately, however, when trying to read configuration registers, it became clear that the PMAC currently does not hold any configuration data (parameters of servos used, accelerations, pulses per revolution etc.). With about a thousand configuration parameters, re-calibrating everything seems just about impossible. So the only chance is to recover the original machine settings from the old control-PC, which does unfortunately not boot.

![Test setup for RS232 interface to universal PMAC-lite]({{site.url}}assets/pic/pmac.jpg)

My friend, however, managed to pull a complete image of the old harddrive, and, to our great relive, it did contain the full PMAC configuration! The file is sort of human-readable, but very long (approx 8.5k lines) and basically not commented. But remember, the only thing of interest was the machine configuration: axis setup, accelerations, PID-settings and such. And so the simplest thing do do was to remove all the motion control programs and just "shoot" the remaining file containing all I-Register settings to the PMAC via a terminal. And it worked, immediately!

We only encountered one slight catch: Because the original control PC was removed (it is damaged in some way), the encoders of the servos were not powered. But it was only a matter of placing a jumper on the back panel - and it worked like a charm. So now, the main question is - how to continue?

There are two main possibilities in my opintion:

The first possibility is to run gcode straight on the PMAC, which it can do if configured correctly. However, for setting up a job, usually more than just loading the gcode is necessary. Setting up speeds and feeds is one thing, but it would also be really nice to get some visual feedback from the machine to check if everything is correct. A GUI, so to say. One Idea would be to use available GUIs like the Universal Gcode Sender for the grbl Arduino-based motion controller and write a "glue-layer" that accepts the commands from the GUI and translates these grbl commands to PMAC commands and back. Another option would be to roll our own GUI and implement some basic features. This way, however, could require quite some work.

The second possibility is based, another approach which I found in a forum post, looks more appealing: Configuring some GPIOs of the PMAC to interface with a typical step/direction CNC-controller. This way, we should be able to keep most of the wiring of the old machine, by having the comfort of a modern CNC controller user interface. This is what I would like to try out when I am at my friends place next.



<!-- more -->
