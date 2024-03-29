# Twomes OpenTherm Monitor Shield hardware

This repository contains the open hardware design files for the Twomes OpenTherm Monitor device, consisting of:
* a Twomes OpenTherm Monitor Shield with a [WeMos D1 Mini shield](https://www.wemos.cc/en/latest/d1_mini_shield/index.html) form factor, to be placed on;
* a WeMos D1 Mini board, such as the [LilyGO TTGO T7 Mini32 V1.3 ESP32](https://github.com/LilyGO/ESP32-MINI-32-V1.3). 

The OpenTherm Monitor Shield is connected via one pluggable terminal block with screws to connect one wire pair leading to a [boiler that supports OpenTherm](https://www.otgw.tclcode.com/matrix.cgi#boilers) and via another one pluggable terminal block with screws to connect another wire pair leading to a [thermostat that supports OpenTherm](https://www.otgw.tclcode.com/matrix.cgi#thermostats). The Twomes OpenTherm Monitor can upload this measurement data to a Twomes server via Wi-Fi using secure HTTPS.

N.B. This is device  is NOT an OpenTherm gateway; it only monitors OpenTherm traffic and it cannot insert OpenTherm commands to the boiler or thermostat.

<img src="./images/pcb.jpg" width="600"  />

## Table of contents
* [General info](#general-info)
* [Producing](#producing)
* [Developing](#developing) 
* [Features](#features)
* [Status](#status)
* [License](#license)
* [Credits](#credits)

## General info
This repository contains the open hardware designs files for the Twomes OpenTherm Monitor device, It also includes a `docs` folder with recent printouts of the [schematics](./docs/twomes-opentherm-monitor-hardware-sch-v2.0.pdf) and [PCB layout](./docs/twomes-opentherm-monitor-hardware-pcb-v2.0.pdf). 

The associated firmware that you can run on this device can be found in [this repository](https://github.com/energietransitie/twomes-opentherm-monitor-firmware).

## Producing

### Printed Ciruit Board
To fabricate the printed circuit board you can use various PCB services. 

The folder [pcb/jlcpcb](./pcb/jlcpcb) includes all exported files needed to have the PCBs manufactured by [JLCPCB](https://www.jlcpcb.com). Upload the [zipped gerber files](./pcb/jlcpcb/gerber/gerber-OpenThermMonitorTwomes.zip) to the [JLCPCB quote page](https://cart.jlcpcb.com/quote), select the amount of PCBs and a colour for the silkscreen. All other options can be left on default. If SMT assembly is desired, also select this option before ordering. This will take you to a page where the BOM and POS file can be uploaded. Use the files [BOM-TwomesGateway.csv](./pcb/jlcpcb/assembly/BOM-Twomes-OpenTherm-Monitor.csv) and [CPL-TwomesGateway.csv](./pcb/jlcpcb/assembly/CPL-Twomes-OpenTherm-Monitor.csv).

N.B. The pluggable terminal blocks we used (see [features](#features) are not listed the BOM-*.csv file; they need to be ordered separately other services and soldered manually.

### Enclosure
To fabricate the enclosure you can use your own 3D printer or use a 3D printing service. 

<img src="./images/enclosure.jpg" height="600" />

The folder [enclosure/fabrication](./enclosure/fabrication) contains exported STL files for the [case](./enclosure/fabrication/twomes-opentherm-monitor-enclosure-case.stl) and [lid](./enclosure/twomes-opentherm-monitor-enclosure-lid.stl) of the Twomes OpenTherm Monitor. The STL files can be imported into any slicer and turned into G-Code for a 3D printer.

## Developing

### Printed Circuit Board
To change the hardware design of the PCB, you need:
* [KiCad](https://www.kicad.org/download/) installed to change te PCB design. 

The KiCad source files of the PCB can be found in the folder [pcb](./pcb).

To convert the PCBs into a format suitable for fabrication, consult the webpage of your PCB manufacturer of choice. For example, see the [JLCPCB guide on how to export Gerbers](https://support.jlcpcb.com/article/149-how-to-generate-gerber-and-drill-files-in-kicad) and the  [JLCPCB guide how to export the BOM and POS files](https://support.jlcpcb.com/article/84-how-to-generate-the-bom-and-centroid-file-from-kicad). You may also use a KiCad plug-in for this purpose such as [kicad-jlcpcb-tools](https://github.com/Bouni/kicad-jlcpcb-tools).

### Enclosure
To change the hardware design of the enclosure, you need either:
* [Autodesk Fusion 360](https://www.kicad.org/download/) installed (Autodesk provides 30 day free trials and [free one-year educational access](https://www.autodesk.com/education/edu-software/overview?sorting=featured&filters=individual) to its products and services for eligible students, teachers and research staff); 
* or [FreeCAD](https://www.freecadweb.org/), an open source alternative.

The source files of the enclosure can be found in the folder [enclosure](./enclosure). We include both .f3d source files and .step source files we obtained after conversion.

## Features
The Twomes OpenTherm Monitor Shield is a [WeMos D1 Mini shield](https://www.wemos.cc/en/latest/d1_mini_shield/index.html) that features the following main hardware components:
* two terminal blocks [CTB9209/2](https://nl.farnell.com/camdenboss/ctb9209-2/terminal-block-pluggable-2pos/dp/2493642), pluggable into terminal block headers [CTB9359/2](https://nl.farnell.com/camdenboss/ctb9359-2/terminal-block-header-2pos-th/dp/2493694) (one for thermostat, one for boiler), each with two positions;
* two optocouplers that electrically separate the OpenTherm circuit on the shield from the monitoring logic on the shield and the main board: the OpenTherm communication between thermostat and boiler still works even if the main board receives no power via its micro USB port or has crashed;
* recessed button that is positioned behind a pinhole in the device enclosure, which allows the end-user to do a Wi-Fi reset.

To-do:
* change design and JLCPCB files to take advantage of the new [one-sided hand-soldering option for through-hole parts](https://jlcpcb.com/smt-assembly) for the pluggable terminal blocks `J1` and `J2` and the pin headers `P1` and `P2`;

## Status
Project is: _in progress_

## License
The hardware designs in this repository are available under the [CERN-OHL-P v2 license](./LICENSE), Copyright 2022 [Research group Energy Transition, Windesheim University of Applied Sciences](https://windesheim.nl/energietransitie)

## Credits
This open hardware design is a collaborative effort of:
* Marco Winkelman · [@MarcoW71](https://github.com/MarcoW71)
* Sjors Smit · [@Shorts1999](https://github.com/Shorts1999)

Thanks also go to:
* Henri ter Hofte · [@henriterhofte](https://github.com/henriterhofte) · Twitter [@HeNRGi](https://twitter.com/HeNRGi)

We use and gratefully acknowlegde the efforts of the makers of the following designs:

* [KiCad Libraries](https://kicad.github.io/), by the KiCad Development Team, licensed under [an adapted version of the CC-BY-SA 4.0 License](https://www.kicad.org/libraries/license/)
* [Opentherm-monitor](https://www.domoticaforum.eu/uploaded/bwired/Open-Termostaat.pdf). In <i>Elektuur, 7-8/2001, pp. 22-23.
