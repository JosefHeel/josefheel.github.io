---
title: Experiments with an Universal PMAC-lite motion controller
categories:
- CNC
excerpt: Experiments reusing the old control system from an industrial dispenser machine to re-purpose it for a hobby CNC-machine.
feature_text: |
  ##  <font color='white'> Homemade CNC router ventures </font>
feature_image: /assets/pic/cnc/cnc_banner.png
aside: true
---

Recently, a friend of mine acquired a massive industrial dispenser machine or something similar, I am not 100% sure what it even did exactly. This machine was given to him for free, or, for the expense of bringing to his workshop, so to say, which is not entirely negligible. The firmly built machine contains three proper AC-servos with encoders and drivers.

It is my friend's and my plan to convert this machine in a CNC-machine for light-duty machining (aluminum and such). However, we do not want to spend too much money on the project, because the machine is quite old and also not the ideal CNC-machine in some ways. So it would be nice to be able to reuse the old control system of the machine. The heart is an ISA-Card specifically designed for this purpose, the so-called "Universal PMAC-lite".

Luckily, the documentation is still available. This card is able to do all sorts of complex motion operations such as jerk limitation, max-acceleration-limiting with look-ahead-feature, transformations between different coordinate systems, etc. etc. on 8 axis synchronously. So is quite a beast and certainly overkill for what we would like to do with it.

When making a test connection via the RS232-Port, the card proved to still be working just fine! Unfortunately, however, when trying to read configuration registers, it became clear that the PMAC currently does not hold any configuration data (parameters of servos used, accelerations, pulses per revolution etc.). With about a thousand configuration parameters, re-calibrating everything seems just about impossible. So the only chance is to recover the original machine settings from the old control-PC, which does unfortunately not boot.

![Test setup for RS232 interface to universal PMAC-lite](/assets/pic/cnc/pmac.jpg)

My friend, however, managed to pull a complete image of the old harddrive, and, to our great relive, it did contain the full PMAC configuration! The file is sort of human-readable, but very long (approx 8.5k lines) and basically not commented. But remember, the only thing of interest was the machine configuration: axis setup, accelerations, PID-settings and such. And so the simplest thing to do was to remove all the motion control programs and just "shoot" the remaining file containing all setup registers to the PMAC via the terminal. And it worked, immediately!

We only encountered one slight catch: Because the original control PC was removed (it is damaged in some way), the encoders of the servos were not powered. But it was only a matter of placing a jumper on the back panel - and it worked like a charm. It always fascinates me how smooth and quiet a proper motion controller can move a machine. It is such a contrast to all the rattling noise that you get when the acceleration ramps and such are not perfect.

Unfortunately, this is where things got more tricky. Now, there is the question on how to interface interface to this card and send g-code to it.

The most promising way is to run g-code straight on the PMAC, which it can do if set up correctly. The last statement is the catch, however. The mechanism works as follows: The PMAC can be configured to interpret G-code commands as subprogram-calls. So for each command, it just calls a subprogram and passes you the rest of the arguments. G01 for example would call subprogram 1001, for G04, it would be 1004. In this program, it is your task to implement the desired behavior, which is a non-trivial task. There is a guide in the manual giving many suggestions, but still it seems like a lot of work.

Secondly, things are not really done if the PMAC executes G-code. As a the machine's operator, you really need some graphical user interface to see what is going on, set up working offsets and so on. And this GUI would need to talk to the PMAC. I think the most feasable solution here would be to use the free "G-code-sender" GUI for the arduino grbl project and write a glue layer program that allows to translate the grbl commands to PMAC commands. This is, however, also a lot of work.  

Another possibility which I found in a forum post, looks appealing: Configuring some GPIOs of the PMAC to interface with a typical step/direction CNC-controller. This way, it would be possible to keep most of the wiring of the old machine, by having the comfort of a modern CNC controller user interface. This approach, however, did not work at all. The PMAC could not really keep track of all the step pulses and would move very abruptly.

The third and probably best option would be to throw out the PMAC all together and replace it with a MESA-card/LinuxCNC combination. MESA offers extension cards like the 7i77, which allow it to interface to analog servo motors, as present in the old machine. This would cost some money, though.

So at the moment it is unclear on what to do in this situation. Maybe, if I find the time to look into the G-code implementation a bit more, it would be nice to give it a try, but if my friend wants to have a usable machine anytime soon in the future, the third option is probably the best. It is not so urgent, however, because there is a lot of work to on the mechanical side of things which is not dependent on having a control system working. Let's see what will happen to this project.

{% include button.html text="Drop me an Email" link="mailto:website.jheel@gmail.com" %}

<!-- more -->
