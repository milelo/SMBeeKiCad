# SMBeeKiCad

Related GitHub projects:
* [SMBee Firmware] - The firmware source, build instructions and binaries.
* [SMBeeHive Programmer] - A low cost custom-jig and programmer for the SMBee.

![SMBee bottom](/doc/SMBee-bottom.svg)
![SMBee top](/doc/SMBee-top.svg)

# Manufacturing Data

It's fairly easy and inexpensive to have SMBee PCBs manufactured in low or high quantities. This is the information you need:

## Gerber files

The Gerber files defines the various layers that constitute a PCB design. The Gerber format is an open-standard 2D vector image format.

Generated gerber files for SMBee version:

| SMBee | Generated with KiCad | Download 
-|-|-
| 1.1.1 (latest)| 5.0.2-5-10.14 | [SMBee1.1.1.zip]

Typically just send the zip to the manufacturer. The file formats and identifying file extensions will be accepted by most manufacturers including:

* [ELECROW]
* [PCBs.io]
* [AISLER]

See the [SMBee PCB costs] spreadsheet for more information on manufacturers.

## Manufacturing options

Some manufacturers have additional options that need to be specified:

Parameter | value |
-|-
Layers | 2 |
Thickness | 1.6mm |
Finish | Gold |
Copper weight | 1oz |
PCB colour | Black |
Dimensions | 57 x 43mm
Castellated holes | No

# BOM (Build Of Materials)

This is the [SMBee BOM] Spreadsheet for the parts. It includes suggested and alternate parts suppliers and their prices dependant on order quantity.

# Assembly instructions

See the [Project documentation](https://milelo.github.io/smbee).

# The Bee Schematic

![Schematic](/doc/SMBeeSch.svg)

Key features & operation:
1. U1 is a high performance, low power 8 bit microcontroller with 1k byte flash and 32 byte RAM. Refer to the [ATtiny10 data sheet] for detailed information.
1. Port B connections PB0, PB1 and PB2 have tri-state outputs: high, low, or high impedance. See table 1 for the LED states.
1. PB0 and PB1 are each configured in the firmware as a pulse-width-modulator output to enable control of the LED brightness.
1. Simultaneous illumination of LED combinations that require conflicting values of PB2, can be achieved by multiplexing the states. See table 1. This isn't supported by the current firmware.
1. The two eye LED's are connected in parallel and can't be individually controlled.
1. BT1 can only supply about 26mA short circuit. Its internal impedance limits the LED current, typically to a maximum of 6mA. This eliminates the need for a resistor to limit the current.
1. The specified LED's have been carefully selected for their relatively low volt-drop at the operating current, their high efficiency and thin construction. Substituting other types is unlikely to give good results.
1. The forward volt-drop of the LED's and U1 drive transistors ensure U1 has enough voltage to function even when the battery is running very low.
1. The circuit can be configured to draw < 200nA in sleep mode.
1. To allow PB3 to be used as an input, SMBee is intended to be programmed using the high voltage programming method. Applying 12V to PRG will enable external programming using the TPI protocol.
1. The default PB3 reset function can be disabled with the RSTDISBL (reset disable) fuse, and configured as an input with an internal pull-up. The firmware can configure the input and pull-up to remain active when the MCU is in sleep mode and generate a wake-up interrupt when the button is pressed.
1. SW1 must be de-bounced in firmware (10ms settle time).
1. During flash programming the two-LED volt-drop is sufficient to isolate the external signals CLK & DAT from each other.

The LED's are activated according to the following table:

Description | Active </BR> LED ID | PB2 | PB1 </BR> PWM-B | PB0 </BR> PWM-A
-|-|:-:|:-:|:-:
Antenna R | Dar1        | 0 | 1	| X
Antenna L | Dal1	    | 0	| X	| 1
Eyes      | Del1 & Der1 | 1	| 0	| X
Sting     | Dst1	    | 1	| X	| 0

**Table 1**, Key: **0:** output-low, **1:** output-high, **X:** don't care, **PB:** Port B, **PWM:** Pulse Width Modulator.

# View or edit the PCB design

The PCB was designed using KiCad EDA software. If you would like to view or edit the design files, download it from [KiCad download] and install the software. 

Clone this repository into your local file space and open SMBee.pro.

[ATtiny10 data sheet]: https://ww1.microchip.com/downloads/en/DeviceDoc/atmel-8127-avr-8-bit-microcontroller-attiny4-attiny5-attiny9-attiny10_datasheet.pdf
[GITHUB-LOCATION]: https://github.com/milelo/SMBeeKiCad
[SMBee Firmware]: https://github.com/milelo/SMBeeFirmware
[SMBeeHive Programmer]: https://github.com/milelo/SMBeeHiveKiCad
[SMBee1.1.1.zip]: https://github.com/milelo/SMBeeKiCad/blob/master/gerber/SMBee1.1.1.zip?raw=true
[ELECROW]: https://www.elecrow.com/pcb-manufacturing.html
[PCBs.io]: https://www.pcbs.io/
[AISLER]: https://aisler.net/
[SMBee PCB costs]: https://docs.google.com/spreadsheets/d/1pC-4M-7qa12mT0QL2S9FdDb4QyRmq4kYofQHElQal1s/edit#gid=567507746
[SMBee BOM]: https://docs.google.com/spreadsheets/d/1pC-4M-7qa12mT0QL2S9FdDb4QyRmq4kYofQHElQal1s/edit#gid=1645088434
[SMBee tools]: https://docs.google.com/spreadsheets/d/1pC-4M-7qa12mT0QL2S9FdDb4QyRmq4kYofQHElQal1s/edit#gid=802410893
[KiCad download]: http://kicad-pcb.org/download/

---

This work is Copyright © 2019 Mike Longworth

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons Licence" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.
