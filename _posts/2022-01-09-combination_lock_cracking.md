---
title: CNC combination lock cracking
categories:
- Mechanics
excerpt: Using the CNC router to brute-force all combinations of a combination lock.
feature_text: |
  ##  <font color='white'> What else can you do with a CNC router? </font>
feature_image: /assets/pic/cnc/cnc_banner.jpg
aside: true
---

#### Introduction
A friend of mine had an old combination lock lying around of which no key number combination be found anymore. Of course, probably not even 20 Euros could get you a new one, but why not try if we can crack it somehow? You can find loads of tutorials on the internet on how to crack one of these in minutes by hand. That was the original idea. However, these approaches mostly rely on pulling on the lever carefully and turning the knob meanwhile to feel some discontinuities and therefore retrieve some of the numbers.

In this case, however, the lock was of a little bit higher quality, meaning it was build in a way that you could not feel small discontinuities because it would have a strong indentation for each number that would "obscure" everything. Maybe somebody skilled in this regard could still do it, but my attempts of this technique were given up after a while.

#### Idea
A while ago, I saw on Youtube somebody using a stepper motor and a simple Arduino to brute-force all combinations of some sort of safe. I cannot quite remember which video it was, but there are a lot of them, just take a look. I thought this is a quite nice idea as stepper motors and the corresponding control electronics are very cheap these days. Even though it might take some time, this is no problem as the apparatus can just work on its own.

Rigging up a microcontroller, stepper motor, driver circuits etc. is still some work though and it came to my mind that all of this stuff is already in place ready to be used in my [CNC router](/cnc/2020/03/31/cnc-screen-printer/). One would just need to unscrew one stepper motor, make it somehow turn the knob on the combination lock and feed it with some g-code.

#### Implementation
I used a very minimalist Python script to generate a g-code file that causes the machine to just try each single one of the 20^3=8000 possible combinations. There is really not much to it, it just consists of three nested loops and writes to a text file. The first idea was to just use a spring to apply some force to the lever of the lock all the time so it would spring open once the right combination is dialed in. This, however, did not really work because constant tension would make the knob hard to turn. Maybe this is also some kind of security feature, I do not know.

In the end, I used a second axis of the machine to pull on a spring a little bit after each combination, but release the force before trying the next one. This increases the run time, but was the easiest fix I could think of in that moment. I made a few test runs and estimated that the exhausting all possible combinations would take about 11 hours. To stop the machine when the right combination is found, I used a small strip of sheet metal that triggers a limit switch, that is in series with the emergency stop of the machine. In the Python script, I would create a comment at the start of the g-code section for each combination. The last comment after the e-stop has been triggered should contain the right combination.

#### Trying it out

I started the apparatus in the morning and came checking every hour or so. That was quite fortunate, in fact, as one time, a rattling noise indicated that a setscrew of a motor pulley had come loose. That was quickly fixed, and after about 3 hours, the lock was indeed open.

![Some brake cable tensioning parts](/assets/pic/div/lock_cracking.jpg)
Combination lock cracking assembly

#### Further thoughts
This little project was bodged together in an afternoon and the cracking cycle started in the next morning. I did not think at all about how it could be optimized. Turns out, one could have saved a lot of time by considering some of the facts below.
* The locks are usually not made terribly accurate, so if you are just one number off, the mechanism tends to also find its way open. Trying every other number instead of every one would already reduce the number of combinations to 1000.
* The third rotor in a combination lock is dragged by the first and second, hence the the two clockwise rotations are necessary to align them. The second rotor is still dragged by the first one, requiring the full counter-clockwise rotation. The first rotor, however, is directly connected to the knob, so once rotor 3 and 2 are set, one can try all combinations of 1 in one sequence without touching 3 and 2, also saving a lot of time.
* The third rotor does not have to be driven clockwise for the first digit of the combination and the second rotor not necessarily counter-clockwise for the second digit. By considering some angle offset (think about it by looking at some animation of a combination lock), one can drive all rotors in both directions, just as it fits best, creating a large scope for further reduction of the way the machine has to move.
* More clever algorithms have been invented by very smart people.

If I have some time, it would be interesting to take a second go at this and see how fast you could make it. No time at the moment ;-)

{% include button.html text="Drop me an Email" link="mailto:website.jheel@gmail.com" %}

<!-- more -->
