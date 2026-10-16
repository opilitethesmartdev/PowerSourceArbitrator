---
title: "PowerSourceArbitrator"
github: "https://github.com/opilitethesmartdev/PowerSourceArbitrator"
description: "Simple module that safely arbitrates two loads with their own power supplies and switches them around as necessary"
created_at: "2026-10-16"
total_time: "48m"
---

# October 16, 2026: Project Setup, parts hunt
<!-- fabricate:entry 527 -->

I set up the project (the usual KiCad, GitHub, etc). 

I then spend quite some time hunting for MOSFETs, because **GOD** are P-MOSes hard to find.
I then realized that *maybe* i had the design all wrong, and iterated a bit on the schematic:
![](https://fabricate.hackclub-assets.com/ad8dc4fee6f05c3b37e8bf6983f6d14a2d2af1aea1a43a5fbffd11b3adf019c7/image-png/image.png)
I kinda have to look into the voltage drop (it's horrendeous rn - like 1.5V per FET), because else it wont really be worth it

Timelapse: https://lapse.hackclub.com/timelapse/mVTVqq3x5k1R

**Total time spent: 48m**
