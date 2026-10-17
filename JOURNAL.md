---
title: "PowerSourceArbitrator"
github: "https://github.com/opilitethesmartdev/PowerSourceArbitrator"
description: "Simple module that safely arbitrates two loads with their own power supplies and switches them around as necessary"
created_at: "2026-10-16"
total_time: "7h 36m"
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

# October 17, 2026 (entry 2): Experimented with new setups
<!-- fabricate:entry 559 -->

After the, uh, not too successful phyiscal test, i decided to take a closer look at the simulation. First, i decided to play around a bit with bipolar transistors (old-school NPN/PNP). But i had to understand how they worked, so i made some test circuits:
![](https://fabricate.hackclub-assets.com/4241a92fa9cec50c1e84a20d04e6d06181f40c0339021e6b7dc7b010e7f805a9/image-png/image.png)
But after quite a bit of iteration I realized that they weren't really the solution, and decided to look into diodes again - specifically ideal diodes, because i can't really afford the voltage drops (or so i thought). But first, again, i had to figure them out, so made this test circuit:
*(forward state)*
![](https://fabricate.hackclub-assets.com/9e6011fe779180b11f25e2d2e9ad3518e9c6c8a629849351bc7f964e22a8052e/image-png/image.png)
*(reverse state)*
![](https://fabricate.hackclub-assets.com/89d2a71bc0ab1c737d41f95dbce518a3af2c7c4ac635cf3286830c5562690506/image-png/image.png)
And uh it seemed to work. But not in the configuration i needed it to. 
So, after a few rounds of exploring the preset circuits in this simulator, i realized something (i should have **not** forgotten): I should get the design working first, then find a diode replacement later - because what sense does a perfect ideal diode setup make if the logic itself is bad?
So, i took normal diodes, ignored the voldate drops, and ended up with this circuit:
![](https://fabricate.hackclub-assets.com/3b8be16e049ce87e9cdbd75fa1a98c1167ad1936b43ea689833385d75a52e5ca/image-png/image.png)
It's basically 2 mosfets (one p, one n) with diodes that control the line - the nmos turns on when there is voltage, but the pmos blocks it when the other side has voltage too - with respective diodes to prevent backflow, it actually works (the test i do to differentiate actual blocking from "50 ohm taste better than 5V supply" is increasing one supply - i actually saw that the old prototypes would instantly fail the moment one supply is greater (even by like 10 mV)).
And luckily, this one doesn't. It actually takes 2V difference to cause a 1uA leak! (and i am **NOT** planning on having either 7V or 3v3 ANYWHERE near any 5V).
So yeah, that was this session.
Next time, i'll have to look into the diodes and voltage drops (or just be lazy and step it back up heh).

Timelapse: https://lapse.hackclub.com/timelapse/6WivjznwEfxq

**Total time spent: 2h**

# October 17, 2026 (entry 3): Implemented ideal diode, experimented with arrangements
<!-- fabricate:entry 596 -->

So, good news is, i finally implemented an ideal diode:
![](https://fabricate.hackclub-assets.com/0e80b3e98166c66189fb4b16fea773c964c217d2244ccb013030b6d56a6c2f44/image-png/image.png)
This is the same design found in Raspberry Pis and it works!
Voltage loss is merely 5-10 mV at 5V!

However ... I kinda did not notice how my whole setup was wrong - so i didn't do much progress. But hey, learning from mistakes is valuable experience, isn't it?
Anyways, the mistake i made is actually quite interesting. Look at this circuit:
![](https://fabricate.hackclub-assets.com/5c053454136f082f6f7a0387d15a1b3a276e73f96d1e8e83760ee5739ad1e474/image-png/image.png)
It looks alright, doesn't it? Well, there is a small issue that is easy to overlook.
Let's first remember what each part represents:
![](https://fabricate.hackclub-assets.com/d3a32d46a667d8185e07d7c0b03b550ae55b0a97d2494ec06cde259cfe0145e8/image-png/Screenshot%202026-10-17%20200512.png)
(edit: the radxa is a sbc, i put it there because this is project should be a part of another one of mine, so i might have forgotten its separate)
*Disclaimer: quick monologue section*
Actually, now that i think about it ... this might not be an issue after all?
(because it's actually sth separate. we dont have to emulate the radxa's load alongside ours)
No, wait, i was right
Or it might?
*monologue done
anyways, the issue is this:
![](https://fabricate.hackclub-assets.com/2e5f176a11df569ba6d98028ec03bc5c50429384f24732419f272fc8eda54bd9/image-png/Screenshot%202026-10-17%20200512.png)
See the ideal diode in the radxa? Well the issue is that i do not have access to the radxa's power lines. I can't just put a diode between its usb (power source) and internals!
Meaning, the actual correct way to have it is like this:
![](https://fabricate.hackclub-assets.com/bced4c3feeae06c2dda6deb379a1fa8b7254ffb4bee78d06512322098f5acfd2/image-png/image.png)
*(Note that the load is now behind the diode.)*
But that, unfortunately, also leads to this:
![](https://fabricate.hackclub-assets.com/983f19c29dccf6f04f4f05b6e8f1629452920659a6e77723bdd5eec742671c81/image-png/image.png)
Meaning, my original goal was **NOT** completed.
(Although this is theoretically valid for this project, meaning i could theoretically put that onto a pcb and give it for review) - idk, will have to think abt it

By the way, here is the link to the Falstad circuit:
https://www.falstad.com/s.php?s=zdKuAg

Timelapse: https://lapse.hackclub.com/timelapse/v5NNCTAiX8R1

**Total time spent: 2h 30m**
