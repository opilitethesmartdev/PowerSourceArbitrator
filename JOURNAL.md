---
title: "PowerSourceArbitrator"
github: "https://github.com/opilitethesmartdev/PowerSourceArbitrator"
description: "Simple module that safely arbitrates two loads with their own power supplies and switches them around as necessary"
created_at: "2026-10-16"
total_time: "3h 6m"
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

# October 17, 2026: Experimented with physical transistors
<!-- fabricate:entry 553 -->

So, from last time, i wanted to put my circuit in the real world and test it out. It was more complicated than i acticipated - i was using my IRLZ44Ns, and the first issue was to even get them to work.
I couldnt figure it out, and, unfortunately, three of them are no longer amongst us:
![](https://fabricate.hackclub-assets.com/57ff2c05c59311d7110c34fd439112911142e59bf0aa32398f2a29d1ad175ca6/image-jpeg/20261017_100021.jpg)
They are now very extravagant 30 ohm resistors:
![](https://fabricate.hackclub-assets.com/804994eaee47f6a589cd4c7034b2b8f1de14a00cf993ed7d2f403b2e84d0ac0c/image-jpeg/20261017_100054.jpg)
But uh, at least their sacrifice was not in vain, because i learnt a very important lesson:
_Never **EVER** drive a high-side load with a low-side mosfet._
(Even though the simulation worked fine somehow - meh.)
Also, i at least set up the design:
![](https://fabricate.hackclub-assets.com/707e1fb8e822b0d3ab3bcdd93c1c84c4773cb695b83ddd58696dfe890817de97/image-jpeg/20261017_100140.jpg)
A button connects power to each side, and activates a mosfet - that would then do the actual board.
But uh i'll stay in simulation for now - don't wanna lose any more MOSFETs. =(
(ignore the scrap parts on the right)

Timelapse: https://lapse.hackclub.com/timelapse/qd0cvuPhl8u-

**Total time spent: 1h 6m**
