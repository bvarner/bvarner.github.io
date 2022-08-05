---
layout: page
title: ANT CNC
tags:
  - varnerized
  - ANT
  - CNC
  - PCB
---
[The Varnerized ANT CNC](https://github.com/bvarner/varnerized_ant_cpcbm) is a very small CNC machine with a high resolution for repeatability.

![The Varnerized ANT CNC]($rootpath/pages/VarnerizedANT/current.jpg)

My machine is a bit different from the stock ANT it was derived from.

All adjustements are open-sourced, STLs and Fusion360 models are available, as is this [grbl fork for the ANT](https://github.com/bvarner/varnerized_ant_grbl) to control the spindle ESC with an arduino PWM timer.

My design differs in that:
* 8MM Rods are used (rather than the 6mm rods used by the ANT)
* My frame is 100mm wider on the X-Axis.
* I use an Arduino UNO, rather than an STM based ARM board.
* I used NEMA 17 stepper motors for all axis.
* TR8 lead screw with a 140 tooth GT2 belt reduction for the Z axis motion.
* D2826 1000kv BLDC outrunner, rather than the 'inrunner' models used by the ANT.
* I have completely redesigned the spoil board & hold downs.
* Added LED strip lighting to the sides, to illuminate the work area.
