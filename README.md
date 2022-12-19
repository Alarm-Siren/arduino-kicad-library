# KiCad Symbol & Footprint Library for Arduino modules
*Version 2.3.0*

This is a library of KiCad schematic symbols and PCB footprints for common Arduino modules. You can use them to make your own PCB design which will effortlessly connect with your chosen Arduino module.

Currently included modules:
- Arduino **101** Shield
- Arduino **Due** Shield
- Arduino **Leonardo** Shield
- Arduino **M0** Shield
- Arduino **M0 Pro** Shield
- Arduino **Mega 2560** Shield
- Arduino **Micro** Socket
- Arduino **Mini** Socket
- Arduino **MKR 1000 WiFi** Socket
- Arduino **MKR WiFi 1010** Socket
- Arduino **MKR FOX 1200** Socket
- Arduino **MKR WAN 1300** Socket
- Arduino **MKR WAN 1310** Socket
- Arduino **MKR GSM 1400** Socket
- Arduino **MKR NB 1500** Socket
- Arduino **MKR Vidor 4000** Socket
- Arduino **MKR Zero** Socket
- Arduino **Nano** Socket
- Arduino **Nano 33 BLE** Socket
- Arduino **Nano 33 BLE** Tile
- Arduino **Nano 33 BLE Sense** Socket
- Arduino **Nano 33 BLE Sense** Tile
- Arduino **Nano 33 IoT** Socket
- Arduino **Nano 33 IoT** Tile
- Arduino **Nano Every** Socket
- Arduino **Nano Every** Tile
- Arduino **Nano RP2040 Connect** Socket
- Arduino **Nano RP2040 Connect** Tile
- Arduino **Pro Mini** Socket
- Arduino **Uno R3** Shield
- Arduino **Uno R3 SMD** Shield
- Arduino **Uno WiFi R2** Shield
- Arduino **Zero** Shield
- Clone **Pro Mini** Socket

*"Shield" means the module is designed to plug in from beneath your PCB. "Socket" means the module is designed to plug in from above your PCB. "Tile" means the module is designed to be soldered directly on to your PCB using surface-mount pads.*

## Compatibility with KiCad 5
This library is in the new KiCad 6 "S-Expressions" format, and is not compatible with KiCad 5. If you need compatibility with KiCad 5, please use version 1.4.1 of this repository - but be aware that said version does not contain all features and is not being maintained.

## Comments, Requests, Bugs & Contributions
All are welcome!
Please open an [Issue](https://github.com/Alarm-Siren/arduino-kicad-library/issues) or [Pull Request](https://github.com/Alarm-Siren/arduino-kicad-library/pulls), as appropriate.

## License & Legal
Copyright 2017-2022, [Nicholas Parks Young](https://github.com/Alarm-Siren).

Except as otherwise noted, the content of this library is licensed under the 
[Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/), with the following exception:
> To the extent that the creation of electronic designs that use Licensed Material can be considered to be Adapted Material, the Licensor waives Section 3 of the Public License with respect to these electronic designs and any generated files which use data provided as part of the Licensed Material.

[![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/)

The word "Arduino" is a registered trademark of Arduino SA. This trademark is used in this library to refer to Arduino products and to identify Arduino-related non-commercial content, as permitted by Arduino's [trademark guidelines](https://www.arduino.cc/en/trademark). This project is not affiliated with nor endorsed by Arduino.

## Donations

If you've found this library useful and you'd like to make a donation towards its continued upkeep, click the button below:

[![paypal](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UX25HM4CZFFWW)

## Library Setup
To add this library to your KiCad Project, do the following steps:
1. Copy the source files to the root of your KiCad project's folder. Make sure that the Arduino.pretty folder structure is preserved.
2. In Schematic Editor go to "Preferences" -> "Manage Symbol Libraries..." menu option.
3. In the Symbol Libraries dialogue that appears, switch to the "Project Specific Libraries" tab.
4. Click "Add empty row to table" button (the button with a big cross in it, beneath the table).
5. In the new line of the table, set Library Path to "${KIPRJMOD}\arduino.kicad_sym" on Windows or "${KIPRJMOD}/arduino.kicad_sym" on Linux/Mac, and ensure Plugin Type is "KiCad".
6. Set Nickname to "Arduino_Library". You can leave the Options and Description fields blank.
7. Close the Symbol Libraries dialogue and exit Schematic Editor.
8. In PCB Editor go to "Preferences" -> "Manage Footprint Libraries..." menu option.
9. In the Footprint Libraries Libraries dialogue that appears, switch to the "Project Specific Libraries" tab.
10. Click "Add empty row to table" button (the button with a big cross in it, beneath the table).
11. In the new line of the table, set Library Path to "${KIPRJMOD}\Arduino.pretty" on Windows or "${KIPRJMOD}/Arduino.pretty" on Linux/Mac, and ensure Plugin Type is "KiCad".
12. Set Nickname to "Arduino_Library". You can leave the Options and Description fields blank.
13. Close the Footprint Libraries dialogue and exit PCB Editor.
14. All done: you are now ready to use these schematic components and footprints!

## A note about Power and Reset pins

### Power
On Arduino modules, it is not possible to categorically state that the power pins are "power inputs" or "power outputs", as that depends on exactly how you're using the module in your design. For example, if you're powering the module from the USB connector then GND, +3.3V and +5V would be power outputs and VIN would do nothing, whereas if you're powering the module from a battery via your PCB then VIN and GND are power inputs whilst +5V and +3.3V are power outputs. There are other, more esoteric possibilities too.

Regardless of the above, I needed to make a decision about what electrical type to apply to these pins. I could use something like "passive" or "unspecified", but then KiCad's electrical rules checker (ERC) tool would not be effective in catching errors on these pins at all, whilst using "power output" means it objects to you joining pins together (for example, joining all the GND pins into a common net) even when that's okay in some situations.

Therefore, I have decided to use 'power input' as this presents the least issues. This means if you're actually using any of the power pins as 'power outputs' in your design, by default the ERC will complain that the relevant nets are undriven. To fix this you will need to add the special "PWR_FLAG" component to the affected net.

*Note: as of version 2.0.0, on 5V-based modules the +3.3V output pin has been changed to "power output", as these will be powered by an on-board regulator and should not have external power fed into them.*

### Reset
Reset pins on Arduino modules have interesting electrical characteristics, which mean that no KiCad electrical type exactly matches their functionality. I settled on "open collector" as the nearest candidate, but unlike a true open collector pin on an integrated circuit, the reset pins on Arduino modules have an internal weak pull-up and a reset button that can strongly pull low, so your design needs to be able to cope with all these situations.

In other words, if you use the reset pin as an input to your PCB then you do not need to add a pull-up (doing so will actually make it less responsive if not break it); conversely if you want to drive the reset line in order to reset the module from your PCB, you need to ensure that you only ever pull it low: if you pull it high at the same time as an unwitting user hits the physical reset button, you've created a short between power and ground which will likely fry whatever chip is on your PCB.

### TL;DR:

*The KiCad ERC cannot catch all the possible electrical errors on your design as it doesn't natively support the reset and power pins' electrical types. Even if the ERC says its OK, double check it manually.*

*If the ERC says that your power pins are undriven, first manually check they are being driven. If they are driven, then add a "PWR_FLAG" component to the net to make the error go away.*
