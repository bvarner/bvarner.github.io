Whole-house power consumption - Metrics Metrics Metrics. :-)

1.) If you want to get UART to RS-485 -- Forget pi485. After way too long searching (but a nicely educational experience with pi485) I finally found some cheap import boards created to bridge UART -> RS485 that have:
* Tx latching
* R/O jumper position (but it's not soldered on)
* Appropriate ESD & polarity protections on the RS-485 side.
* Rx / TX LEDs. :-)

They're about $12 for 5 of them on amazon. You'll need to add a few things (headers, etc.) or solder wires on by yourself, but it's well worth the cost. The down-side is that they sanded the tops of the ICs. So I'm not _sure_ what they're using. :-(

2.) I've put together [this simple circuit](https://github.com/bvarner/PZCT-02-BurdenShift) to create an appropriately sized burden to covert inexpensive current-output CT clamps to voltage-output, suitable to be fed to an ADC -- either the 10bit built into an arduino, or another chip, like the ADS1115.

Using this, I'm passively monitoring the hot legs of my house and shop electrical feeds.

I've been working on metrics / monitoring / etc.

Notes on that:

* I still love collectd. The sensors plugin works great on a raspberryPi with proper DT overlays. :-)
* I hate storage mediums that limit things to 1 second. This is just stupid. Carbon / Graphite / Whisper, etc. whatever you want to call it, they're fragile.
* Why do I need carbon / graphite / whisper to feed a Grafana dashboard? What a waste.
* Grafana is a _pain_ to build on a Raspberry PI B+ / Zero / W. The current binaries I could find posted were for the later ARMV7 based machines, not the ARM6+FPU. It took me a few days to finally get it building properly.
* I think I'm going to try to a different path to circumvent whisper, since I hate it. :-/

