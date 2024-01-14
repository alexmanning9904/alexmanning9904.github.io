---
layout: post
title: Hardware-Accelerated Cryptopals - Set 1 Challenge 1
tags: cryptopals
published: false
---

This idea has been bouncing around my head for a few years now - the [cryptopals](https://cryptopals.com/) cryptography challenges are something that I learned about and attempted for the first time a few years back; sometime during college.  The first time around I used Python to tackle the challenged, although I admittedly didn't make it too far, maybe into set 2?  I wanted to give these challenges another go, but I thought I'd give the whole thing a bit of a twist both to keep things interesting, and to keep my FPGA skills up since they aren't being worked at all professionally right now.  I'm going to run through these challenges on a [Zybo Z7](https://digilent.com/shop/zybo-z7-zynq-7000-arm-fpga-soc-development-board/) development board, which has a Zynq 7000-series SoC.  The board choice was made simply because I already have one.  My goal is to execute each solution as fast as possible using hardware acceleration techniques where appropriate.  I haven't actually been able to find anybody else who has posted their execution times, so I'm arbitrarily taking [this solution set](https://github.com/ricpacca/cryptopals) as a benchmark.  The command I'm using is `python -m timeit "from <Solution> import main; main()"`  I'll acknowledge up front that the competition is already a bit apples-to-oranges:

    1. This set is written in Python, which means that it'll naturally be a bit slower than some other sets that I could have chosen.
    2. This set will also be running on my desktop PC (Intel Core isomething or other), which clocks in _much_ faster than the ARM chip inside the Zynq.
    3. I'm measuring real time, not CPU time.  The reference set will be at a disadvantage running on top of Windows, which may slow it down a bit whereas my solution set will be running bare-metal on the Zynq.

All in all, these comparisons will be fun, but should be taken as a curiosity only.  Maybe once I get the first set done I'll make a callout post or something to see if anyone can run these things faster.

# Set 1
## Challenge 1
__Benchmark Time:__ 51.1usec

The challenge part of this one is easy - convert a hex string to a base64 string.  My plan is to build a coprocessor in the PL that looks like:
```mermaid

flowchart FLOWCHART
    PS[Zynq 7000 Processing System]--- AXI Stream --> HEX_BIN[Hex to Binary]
    HEX_BIN--- AXI Stream --> BUF[Buffer]
    BUF--- AXI Stream --> BIN_B64[Binary to Base64]
    BIN_B64--- AXI Stream --> PS
```