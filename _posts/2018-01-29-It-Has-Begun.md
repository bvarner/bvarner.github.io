Over the last week, nearly all the parts have arrived. The linear bearings are in, my replacement rods from Amazon are in, and cut to size. Most importantly, the stepper motors are in. This makes it possible to start assembling the motion axes. So I have.

![Motors Arrived](/images/varnerized/steppers.jpg)
_The stepper motors have arrived!_

Some notes on parts:
* When ordering zip-ties, get the 100mm length. Or, expect to have to stretch the 80mm lengths just a bit before you can mount the linear bearings on the x-axis carriage. I was able to stretch the 80mm ones long enough without breaking to get them to work, but there were a few minutes of angst before I thought of that.
* The Y-table belt holder had to be modified to contact the y-motor endstop. This has been pushed to the github repo. It may be excessive, depending upon your frame components -- so you might need to tweak the variable in the SCAD file for a different extension / offset length.
* The linear bearing holders on the bottom of the y-table don't leave a lot of 'play' between the frame components and the holders. Beware clearance. I may make a new frame later on to mitigate this, depending on how much of a problem this becomes long-term.
* I'm also dealing with split wood from the plywood extrusion facimilies. I ended up making a second batch of the rear (shorter) struts out of solid poplar, and that has worked better -- but still not great. Having the holes that close to the edge (like you would attach a 3030 extrusion) is asking for splitting, even after pre-drilling pilot holes aggressively inward to the center of the strut.
* I switched to using stainless pan-head screws for the frame struts. Those are working much better than the machine cap screws. (no surprise there)

Assembling the frame is pretty straight-forward. I may adjust some of the SCAD models in the future to better handle my wood frame parts / adjustments. Specifically where the pilot holes are, and perhaps the extrusion replacement lengths.
I may have 'messed up' on how I cut the extrusion replacements, since I calculated that the frame should sit in the middle of where the frame should be, rather than trying to keep the 'face' of the frame in the correct spot. This may mean that my table won't move 'forward' enough. If I was using true PRUSA MK42 or MK52 heatbed, I'd definately have issues. With the undersized MK3 bed, I may be OK.

![Frame and Motors](/images/varnerized/frame_and_motors.jpg)
_The frame, motors, and motion axes._

As it stands, here's the frame and motion parts assembled.