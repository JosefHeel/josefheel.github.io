---
title: Repairing an ILIFE Model V7s Plus robotic vacuum cleaner (2-beep error)
categories:
- Electronics
- Repairs
excerpt: Repairing an ILIFE Model V7s Plus robotic vacuum cleaner that gives a two-beep error after turning it on (cliff sensor or bumper error). 
feature_text: |
  ##  <font color='white'> Except this one thing, its perfectly fine ... </font>
feature_image: /assets/pic/drillstand/ds_banner.jpg
aside: true
---

#### Introduction
This small repair project on a rainy sunday afternoon is about a ILIFE Model V7s Plus vacuum cleaning robot that a friend gave to me. Upon turning it on, it drives back and forth for a few seconds. Then it stops, the status LED turns red and it emits two short beeps repeatingly. The manual relates this error code to "error NO. 2", where "Cliff sensor or bumper failure" is listed as a cause, with the proposed solution "Check cliff sensor and check bumper sensor".
![ILIVE Model V7s Plus vacuum cleaning robot](/assets/pic/vacuum/vacuum_repair_1.JPG)

With no obvious damage or blocking of those parts, my friend contacted the manuacturer, which attributed the issue to a faulty motherboard and/or cliff sensors. They sent some replacement parts, so this repair job should be just swapping the board and the sensors. 
![Replacement parts provided by the manufacturer](/assets/pic/vacuum/vacuum_repair_2.JPG)

Unfortunately, with the new parts installed, the fault persisted completely unaltered. Well, while we are at it, we might try to dig a bit more. 


#### Looking further
Given that the manual tells us pretty clearly that the fault should be a "cliff sensor or bumper failure", and that we just replaced the optical cliff sensors, the bumper would be the next guess. On the sides are those plastic parts that get pushed inwards and block an optical sensor. My first guess would be that some piece of dirt made it into the optical path and blocks the sensor all together, so let's have a look.
![Location of optial bumper sensors](/assets/pic/vacuum/vacuum_repair_3.JPG)

Upon removing the cover, it turned out that the receiver (a phototransistor) pins had broken off the PCB. That's our fault, which perfectly explains the behavior. 
![Broken optical bumper sensor](/assets/pic/vacuum/vacuum_repair_4.JPG)

#### Fixing the broken optical sensor
Luckily, the pin broke a tiny bit below the clear plastic casing of the phototransistor, so with a little bit of tounge-twisting and some copper wire it was possible to solder the original part back in place. In case this had not been possible, I'd assume that most of those optical sensors with the right form factor would do the job here, but I did not have any at hand. 
![Soldering back the original phototransistor](/assets/pic/vacuum/vacuum_repair_5.JPG)

I put some hotglue around the soldered pins when closing the black cap to support them a bit better and avoid breaking in the future. Watch out not to get any hotglue in the optical path when doing this, though.
![Fixed optical sensor](/assets/pic/vacuum/vacuum_repair_6.JPG)

#### A bad design example
But now I'm really wondering why the pins broke in the first place. Free-standing packages with all pins in one line (like a free-standing TO-220 for example) are known to be somewhat prone to breaking in presence of vibrations, but this part is supported by the plastic case, so this seems quite unlikely to me. However, pressing the bumper a bit revealed all too clear why the pins broke: Unlike I would naturally assume, the bumper is not stopped by some piece of plastic or other endstop, but by the optical sensor itself! 
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_7.JPG)
The whole force of the impact has to be taken by those four small copper pins. Given that vacuum cleaner robots bump into things on a daily bases, I am pretty amazed that it did even last that long. This a very surprising and strange case of bad design in a product that otherwise seems pretty well-built mechanically. It is also completely unnecessary as the optical sensor would naturally have allowed to detect the bumping movement without any force. With so many complicated injection-molded plastic parts, it would have been all too easy to include some sort of tab to take the impact before the optical sensor. There is even this elongated hole in the bottom which contains the movement of the bumper. 
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_8.JPG)
Had they just made that slot 2mm shorter, there would not have been any issue. Either it was really overlooked, or we have a textbook-style case of planned obsolescence here. (This is my personal opinion, who knows for sure.)

#### Making it better than it was
It would be nice to add a sturdy endstop for the bumper somewhere, otherwise it might break the optical sensor quite quickly, especially now that the pins might not be as strong as they were before. The next piece of structural plastic is conveniently just behind, so let's measure the gap.
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_9.JPG)

This small woodscrew (3x20mm) has just about the right length to make for a nice and adjustable endstop if screwed in the housing. 
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_10.JPG)

In order not to break the plastic, I pre-drilled some 1.5mm holes with a cordless drill.
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_11.JPG)

On the other side of this plastic is the weel housing, where there are a few millimeters of space before the screw interferres with the wheel, but make sure that the screw is not too long. Also, be aware that the robot is a bit asymmetric, one side requires a slightly longer screw than the other. 
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_12.JPG)

Now we can nicely adjust the screw until the bumper triggers the optical sensor, but does not hit it. I later added some hotglue around the screw for good measure to prevent it from getting loose. 
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_13.JPG)

#### Summary
On this ILIFE Model V7s Plus vacuum cleaner robot, the bumpers lack any sort of dedicated mechanical end-stop. Instead, the force of a bumper impact is directly transferred to the optical sensor. This instance of bad design caused the soldered pins of the sensor to break over over time. A solution to this fault consists of fixing the pins by soldering extra copper wire to them. To avoid them breaking in the future, I added two woodscrews in the case to act as force-absorbers. 
![Vacuum cleaner](/assets/pic/vacuum/vacuum_repair_14.JPG)
Whith those modification, the robot is cleaning nicely again, and hopefully will continue to do so for a long time.

{% include button.html text="Drop me an Email" link="mailto:website.jheel@gmail.com" %}

<!-- more -->
