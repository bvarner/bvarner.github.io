---
title: Using an Arduino Nano to burn Arduino Bootloaders
tags:
  - Arduino
  - KiCad
  - AntCNC
---
Here's a [KiCad](https://kicad.org) project for [Using an Arduino Nano as an Arduino ISP](https://github.com/bvarner/ArduinoNanoISP).

It produces this beautiful board:

![Board Top]($rootpath/files/ArduinoISPTop.jpg) ![Board Bottom]($rootpath/files/ArduinoISPBottom.jpg)

Which in this case, I managed to (successfully) mill on the [Varnerized ANT CNC](https://github.com/bvarner/varnerized_ant_cpcbm).

## Backstory
A few weeks ago the heater core on my [Varnerized Prusa](https://github.com/bvarner/varnerized_prusa_i3) started shorting out -- in the process
of replacing the heater, tuning the PID settings, and flashing the firmware back to the Arduino Mega that controls it, I found out (the hard way)
that the USB-C to USB-A converters I have will... rapidly brick an Arduino.

After confirming that it's only those converters that were the problem, I set about to 'unbrick' the Arduinos I'd bricked in the process of verifying that the cables were the problem.

This led me to this most helpful site about [Arduino as ISP and Arduino Bootloaders](https://docs.arduino.cc/built-in-examples/arduino-isp/ArduinoISP), which contains some sketches and circuits for using healthy Arduinos to burn bootloaders onto 'bricked' Arduinos.

I quickly breadboarded the circuits with parts I had on hand, got the Arduinos in working order, and was happy after I fixed the printer... sorta.

![reflashing the printer]($rootpath/files/reflashing_the_printer.jpg)


This is a pretty simple schematic, this is a pretty simple circuit, and it's one I can see myself using again in the future -- since I'm pretty sure this is the second time I've had to do this, and I didn't want to leave the circuit sitting on a breadboard on my desk for too long.
My old breadboard is pretty clunky.

![Old Breadboard]($rootpath/files/ArduinoISPBreadboard.jpg)



