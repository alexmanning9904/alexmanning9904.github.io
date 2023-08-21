---
layout: post
title: Hydroponics Control Board Design
tags: hydroponics
published: false
---
I eventually wanted to run this setup on a custom controller to make sure that packaging is nice and clean while I work software.  With the goal of starting small, I'd like the first version of this to have the following interfaces:
   - DC power input - Main power input; easier to buy a cheap PSU to handle wall-voltage conversion.
   - 15V Analog Out - for controlling my light with a bit better precision
   - Switchable 12V outs - for fans, air stone, whatever I end up needing.
   - Water level sensor - used to whine at me whenever water is low, and also to track refills to recommend water changes - easier than running a pH/EC sensor right now

This "V1" design should give me a minimum amount of plant monitoring to make sure that everything stays alive, without requiring periodic replanting thanks to the kratky bucket.  I'm thinking an ESP32-C3 for the main microcontroller - RISC-V means easy Ada integration, and WiFi makes it easy to send notifications.
