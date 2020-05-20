While the printer upgrade is waiting on a few additional parts... (more on that later) it was time to revisit another project I've had going in parallel. Building my own model rocket engines from easily accessible goods you'd find in a store near you, or already around your house. I'm using supplies that are as close as your mailbox (for the newsprint), the local hardware store, and your neighborhood grocery. What follows is the account of an initial test firing. :-)

In order to document my progress and test my methods before putting these things into the air, I've designed and built a reasonably inexpensive test stand and customized software to control things.

I decided tonight was a good night for an integrated test, even though the software is still in a very ugly, very early state. I was hoping it would be reliable enough to recover the high-speed footage off the device, but just in case it wasn't going to work, I did a screen-capture recording of the slow-frame-rate stream my laptop displayed. Because you know, you want to keep _something_. ;-)

This test was with a motor casing I packed a month or so ago. It has more propellant than I'd actually want to use on a real rocket, but it was an old batch from before I started purifying the oxidizer.

The electric pyrotechnic igniter is home-made, and has an integrated plug to hold it in place.

The motor is in the test stand pointed _down_, with the nozzle aimed straight up.

The blue area of the graph is the weight of the motor (in grams, left y-axis). The constant slight deviation is noise from the power-supply, which suffers from a horribly choppy 60hz AC -> DC conversion.

In a perfect world, the cam stream on this video would be at 20 frames / second. The video of my laptop screen recorded at 30fps.

Everything started awesomely.

Igniter continuity detection works perfectly.
Countdown started, and system sanity checks passed.




Igniter started - 33:25
Smoke - 35:08
Igniter ejection - 35:13
Engine Thrust - 35:17 (~505g increase in ~132ms) 
Igniter disconnects - 35:21 (off camera)
Stand jumps - 35:22 (uh oh)
Graph updates - 35:23 (~264g in ~250ms)
Stand tilts - 36:02 (uh oh)
Stand empty - 36:09 (uh.... where'd it go?)

At this point, my own personal observations kick in.
The motor went airborne. I did not find it. I know it flew erratically, and I was unable to track it. I was, however glad I was in a safe spot inside out of harms way.

The way the scale reports mass (in the portion below the graph) is by calculating a rolling average of all the data points included in a given graph update (roughly 13 samples every 250ms). It's not great for instantaneous results.

After I went out looking for the motor, I forgot to 'stop' the data logging, ran the system out of memory, and failed to get the high-fps footage, or the high-res data logs from the scale. :-(

Next time, I'll set a recording limit of 15 seconds / mission, delay recording to start at 3 seconds remaining in the countdown, bolt the test stand down, and wrap tape around the motor to make sure it's 'snug' in the test stand.

Also, I'll make sure I pack several motors at a time, and be more careful about grain size. :-p

I _think_ what happened, was that the clay plug on the head end of the motor failed to hold pressure. There should not have been that much smoke and what-not come out the exhaust port at the 'head end' (bottom in the video) of the motor 1/4 of a second into the burn.

This is why i'm bummed I couldn't find the motor.
