---
layout: post
title: VS1000 Pinout and Basic Control
tags: hydroponics
---

The VS1000 light arrived.  Reverse-engineering the remote-control protocol turned out to be surprisingly easy.  I broke out connections on an RJ11 cable, and got to probing it with a multimeter.  With the light turned on, the 4 pins show:

| Pin 1 | Pin 2 | Pin 3 | Pin 4 |
| --- | --- | --- | --- |
| +15V | GND | GND | +15V |

Both pairs are tied together, which makes sense, as it prevents any "mirroring" type issues in connectors or cables.  The +15V lines are a weak-pullup control signal, and when pulled down, they deactivate the light.  I ended up piecing together the following circuit on a breadboard to let me control the 15V lines with an arduino:
![Circuit](images/2023-06-26-Schematic.png)
The circuit works well for on-off control, which is really all that I need, at least in the near term.  I did give PWM dimming a shot, which sort of worked, but had a massive deadband.  For now, I'm comfortable running this at full power on a timer.  The next steps are to get this circuit off of the breadboard and into a moderately robust form, and install the whole thing into the greenhouse.
