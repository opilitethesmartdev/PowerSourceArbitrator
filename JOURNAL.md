---
title: "PowerSourceArbitrator"
github: "https://github.com/opilitethesmartdev/PowerSourceArbitrator"
description: "Simple module that safely arbitrates two loads with their own power supplies and switches them around as necessary"
created_at: "2026-10-16"
total_time: "2h"
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

# October 16, 2026 (entry 2): Experimented with setups
<!-- fabricate:entry 532 -->

So i played around with the circuit a little, mostly because something was sketchy **and** i did **NOT** like the voltage drop - it was **INSANE** (like 3V!!!).
So i spend around an hour testing stuff out, experimenting, and ended up with this design:
![](https://fabricate.hackclub-assets.com/9bfa58202f9f07d65ee6bee8c7c4f3785679c920247525cc12e1f192d5e9bd4e/image-png/image.png)
Note that it now uses N-channel MOSFETs instead of P-channel, and how its total voltage drop (when only one source feeds both is only 0.8V! 
![](https://fabricate.hackclub-assets.com/6fddfa479ead9a81c333f0a877f2377f3de934331ad9a089b070bd0f46efdaf0/image-png/image.png)
But, again, something is kinda sketchy - mostly because i can't really tell whether the N-MOSFETs are actually off or 50 ohm taste better than mosfets (ifykyk reference) (idk maybe not but still i cant really tell).

So, next step will be some real time experimenting, with ACTUAL transistors (i have some uh IRLZ44s lying around for stuff). Stay tuned ig (do ppl actually read these or is this only for the submission)?

Timelapse: https://lapse.hackclub.com/timelapse/HRWkrYtNx8xA

**Total time spent: 1h 12m**
