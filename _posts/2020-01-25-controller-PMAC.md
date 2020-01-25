---
title: Experiments with Universal PMAC-lite
categories:
- CNC
feature_image: "https://picsum.photos/2560/600?image=872"
---

Recently, a friend of mine aquired quite a massive industrial dispenser machine (or something similar, I am not 100% sure what it even did exactly). This machine was given to him for free, or, for the expense of bringing to his workshop, so to say, which is not so negligible.

It is my friend's and my plan to convert this machine in a CNC-machine for light-duty machining (aluminum and such). However, we do not want to spend too much
money on the project, because it is quite old and also not the ideal CNC-machine in some ways. So it would be nice to be able to reuse the old control system of the machine. The heart is an ISA-Card specifically designed for this purpose, the so-called "Universal PMAC-lite".

Luckily, the documentation is still available. This card is able to do all sorts of complex motion operations such as jerk limitation, max-acceleration-limiting with look-ahead-feature, transformations between different coordinate systems, etc. etc. on 8 axis synchronously. So is quite a beast and certainly overkill for what we would like to do it.

Luckily, when making a test connection via the RS232-Port, the card proved to still be working just fine! Unfortunately, however, when trying to read configuration registers, it became clear that the PMAC currently does not hold any configuration data (parameters of servos used, accelerations, pulses per revolution etc.). With about a thousand configuration parameters, recalibrating everything seems just about impossible. So I really hope that we will be able to extract some of the configuration from the old industrial PC which originally controlled it all. 

![Test setup for RS232 interface to universal PMAC-lite]({{site.url}}assets/pic/pmac.jpg)

So now it is "just" a matter of finding out how to use the PMAC again. Theoretically, the PMAC can run straigt gcode if configured correctly. However, I am not sure if we can make use of that. At the moment, another approach which I found in a forum post, looks more appealing: Configuring some GPIOs of the PMAC to interface with a typical step/direction CNC-controller. This way, we should be able to keep most of the wiring of the old machine, by having the comfort of a modern CNC controller user interface. This is what I would like to try out when I am at my friends place next.



<!-- more -->
