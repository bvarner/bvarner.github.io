# Hacking the Bryant / Carrier Touchscreen Thermostats

At this point, I've done a sizable amount of reversing on the wire protocol.

I've come to the following conclusions.

1. The wire protocol is little-endian. The addresses (and the serial I/O) make more sense in LE.

* Broadcasts from initial power own include the traditional serial sync 0x011f, immediately followed by 0xf1f1, if you look at it as LE. The 011f is a traditional serial protocol sync. The next byte is f1f1, which lets you determine that the sync byte 011f or 1f01 (depending upon endianess). So... in two bytes, you've got a 'SYNC' AND 'Oh, by the way, here's the endiness of this wire protocol'.
* The actual frames encoded on the wire have LE CRC16s!
* Address ranges make more sense. 0x011f + 1 = 0x0120 = thermostat address.
* The actual data _in_ the wire protocol... Now _that_ likely _is_ Big Endian, which isn't really a big deal. PIC / ARM / SH processors... all Big Endian by nature.

2. You have to _thinK_ like an embedded guy from the late 90's to figure this stuff out. This is low-level C stuff, most of the early communicating boards and equipment are based on PICs with tiny EEPROMS and small amounts of RAM. They run tight loops without an operating system, or with very little of one.

* It's very likely that we're dealing with raw structs dumped over the wire.
* There _has_ to be some form of standardized 'master list' of struct types, somewhere. Likely in the thermostat code.




