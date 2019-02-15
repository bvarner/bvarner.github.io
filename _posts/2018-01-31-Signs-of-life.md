All in all, this has gone surprisingly well so far. I have worked my way through the MK2s and MK3 assembly guides (switching between the two -- the frame and y-axis is MK3, the X, Z, and extruder are MK2s and have a mounted PSU, Heatbed, and extruder assembly (minus the hot-end, which I'm still waiting for... *cringe*). I also have a mess of cables. In the MK3 guide, they recommend doing cable management 'all at once' at the end. I have to agree that deferring cable management to the end seems to be the easiest route.

![It's a mess](/images/varnerized/its_a_mess.jpg)
_Cable Management is up next..._

For my major wiring, I didn't opt for 'speaker cable' as many do, but picked up a few feet of #12 THHN wire at my local home-center. You can purchase this stuff 'by the foot' off their reels -- where they'll cut to length and let you pick the color. The #12 is seriously stiff stuff, even though it's "stranded". It took me an hour or so to solder up the #12 wire to the IEC plug terminal tabs (I didn't want to spend the money / time trying to crimp yellow connectors for this) and get the PSU wired up properly, but it's done. It's worth mentioning that 3' of red and black was more than enough, and I only used a few inches of green for the ground plug to the PSU ground. I'll be trimming about 8" off the ends running from the PSU to the RAMPS board once I have the enclosure printed.

The PSU shroud has gone through a few revisions. My hole locations were off by ~4mm. I'll print the next iteration on this printer, when it's working. Until then, I drilled a couple mount holes where they needed to be to affix the PSU in the proper spot. Also, when printing this, use 4 vertical shells rather than 2 + infill. I'm having 'ridgity' issues with the ABS. I'll probably reduce the layer thickness from 0.2 to 0.15 as well, to see if I get better fusion. Also in the next iteration of the PSU cover, it'll have prettier corners, a bit more Varnerizing, and the IEC socket will be in a better location, to allow it to lock in position along the bottom better. Whoops.

I took the time to print labels for all my connectors and put them on the cable end connectors. This made it _much_ easier when plugging things into the RAMPS board. Currently both my Z axis motors use the same stepper driver. I notice a huge difference in holding power on those -- but on a TR8 threaded rod, it doesn't take a lot of holding force to keep things from wiggling. Yay.

I took the time to watch Tom Salanderers video of doing firmeware. It was hard to follow, and confusing in a few spots. Specifically around the `X_MIN_POS` and `Y_MIN_POS` portions, induction probe offset, and setting travel limits from "home". Let me try to clarify, as it applies to 'auto homing'.

* "Home" should be able to find where the printable `[0,0,0]` is on your build platform (the heated bed).
* The positive motions should be limited so that they don't exceed the build volume of your setup, and don't do damage to your axis motions.
* To handle 'z-home' probing with an induction sensor they use a 'safe' z-probing location. Typically this is the 'center' of the bed. I don't care for that. I'd rather have it do this near the `[0,0]` location, with the induction sensor as close to the x-y origin as possible. I don't know why. I just do. This is the `Z_SAFE_HOMING_X_POINT` and `Z_SAFE_HOMING_Y_POINT`, which are given in _induction sensor_ coordinates, not _nozzle_ coordinates. The firmware will move the carriage so that the induction sensor is in the spot you specify.

To make this all work, you need to follow this proccess to setup the constants in the [Marlin Configuration.h](https://github.com/bvarner/Marlin/blob/varnerized_prusa_1.1.8/Marlin/Configuration.h)...

1. With the printer _off_, move the Y-Table and X-Carriage over `[0,0]` on your print bed surface. Or put another way, use person power to position the nozzle where you want the `[0,0]` to be when you're printing.
2. Measure the distance from the X-carriage to the minimum x end stop in millimeters.
   The X-carriage can 'safely' move that distance 'below zero' before the endstop is triggered. In my case, it's 19mm.
   This means that my endstop is -19mm from 0 on the x axis.
   So, in the Configuration.h, I have `#define X_MIN_POS -19`, defining that the endstop is -19mm from 0.
3. Measure the distance from the Y-Table part that contacts the endstop to the y end stop switch in millimeters.
   The Y-table can 'safely' move that distance 'below zero' before the endstop is triggered. In my case, it's 17mm.
   This means that my endstop is -17mm from 0 on the y axis.
   So, in the Configuration.h I have `#define Y_MIN_POS -17`, defining that the endstop is -17mm from 0.
4. I never want my nozzle to 'crash', so I have my `Z_MIN_POS` defined as `0.10`. Prusa does the same, for what it's worth. I disabled this later on, and deeply regret it now.
5. The _printable_area_ on my MK3 bed, is roughly 200x200. The bed itself is 214x214, but there's ~7mm of padding I'm leaving for screw heads. This means I set `#define X_MAX_POS 200` and `#define Y_MAX_POS 200`, so that my Y and X axes don't stall out against the extents of their positive travel limits. I also set `#define X_BED_SIZE 200` and `#define Y_BED_SIZE 200`.
6. My z axis, I want to be able to stall out against the positive limit, to ensure that both motors have torqued the X-carriage parallel, and move in synch after stalling. So while my actual travel limit is ~195mm, I have set `#define Z_MAX_POS 200` to allow it to stall out at the top and lock in the carriage properly.
7. Measure the distance from the nozzle to the induction probe center along the X axis. Mine is 11mm to the left of the nozzle, or +11. I have set `#define X_PROBE_OFFSET_FROM_EXTRUDER 11`.
8. Measure the distance from the nozzle to the induction probe cetner along the Y axis. Mine is 2mm behind the nozzle, or +2. I have set `#define Y_PROBE_OFFSET_FROM_EXTRUDER 2`.
9. Enable 'safe' Z homing by: `#define Z_SAFE_HOMING`. I don't care for the default of using the center of the print bed for the homing position (if you were to try to re-home during a print centered in the bed, that would be an epic fail) so I also set the `Z_SAFE_HOMING_X_POINT` and Y points to move the sensor to the front left side of the table `[0,0]`.
10. Manually move your X carriage so that the nozzle would be over `[0,0]` on your print bed. Measure between the X limit switch and the current position. Your carriage can move this distance negative of `0` on the x-axis before hitting the endstop. So if there's 12mm between your x-carriage and limit switch when the nozzle is over `[0,0]`, your `X_MIN_POS` (where your lmit switch is in the cartesian plane) should be `-12`.
11. Manually move your y-table so that the nozzle would be over `[0,0]` on your print bed. Measure the distance between the endstop trigger for the y-table and the endstop. Negate the value, and that's your `Y_MIN_POS`, or where the nozzle is located in the cartesian plane when the limit switch is triggered.

The thing to remember in this process, is that everything is based on _nozzle location relative to the origin of the print area_.


