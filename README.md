![KiCad Library for Arduino banner logo](/resources/banner.png)

# KiCad Symbol & Footprint Library for Arduino Modules
*Version 3.0.0*

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

## KiCad Version Compatibility
This library requires at least KiCad 6 to function, and is tested on version 6.0.8.

## Comments, Requests, Bugs & Contributions
All are welcome!
Please open an [Issue](https://github.com/Alarm-Siren/arduino-kicad-library/issues) or [Pull Request](https://github.com/Alarm-Siren/arduino-kicad-library/pulls), as appropriate.

## License & Legal
Copyright 2017-2023, [Nicholas Parks Young](https://github.com/Alarm-Siren).

Except as otherwise noted, all content of this library is licensed under the 
[Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/), with the following additional exception:
> To the extent that the creation of electronic designs that use the Licensed Material can be considered to be Adapted Material, the Licensor waives Section 3 of the Public License with respect to these electronic designs and any generated files which incorporate data provided as part of the Licensed Material.

[![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/)

### "KiCad Library for Arduino" Banner & Icon

The two images "resources/banner.png" and "resources/icon.png" are are licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). These images are derivatives of ["Arduino Open-Source Community: Main Logotype RGB Colors" originally created by Arduino](https://www.arduino.cc/en/trademark/community-logo). 

[![CC BY-SA-NC 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Original Images: Copyright 2013, [Arduino SA](https://www.arduino.cc/).
Derived Images: Copyright 2023, [Nicholas Parks Young](https://github.com/Alarm-Siren).

### Arduino Trademark

The word "Arduino" is a registered trademark of Arduino SA. This trademark is used in this library to refer to Arduino products and to identify Arduino-related non-commercial content, as permitted by Arduino's [trademark guidelines](https://www.arduino.cc/en/trademark). This project is not affiliated with nor endorsed by Arduino.

## Donations

If you've found this library useful and you'd like to buy me a beer in thanks, you can make a donation using the button below:

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
9. In the Footprint Libraries dialogue that appears, switch to the "Project Specific Libraries" tab.
10. Click "Add empty row to table" button (the button with a big cross in it, beneath the table).
11. In the new line of the table, set Library Path to "${KIPRJMOD}\Arduino.pretty" on Windows or "${KIPRJMOD}/Arduino.pretty" on Linux/Mac, and ensure Plugin Type is "KiCad".
12. Set Nickname to "Arduino_Library". You can leave the Options and Description fields blank.
13. Close the Footprint Libraries dialogue and exit PCB Editor.
14. All done: you are now ready to use these schematic components and footprints!

## A note about Power and Reset pins

### Power
On Arduino modules it is not possible to categorically state the appropriate electrical type for some power pins, as that depends on exactly which module you're using and how it's connected in your design. Sometimes a pin must necessarily be a power input or output, or is internally disconnected by default, but some pins may be either depending on how you are using the module.

Regardless, I needed to make a decision about what electrical type to apply to these pins. I could use something like "passive" or "unspecified", but then KiCad's electrical rules checker (ERC) tool would not be effective in catching errors on these pins at all, whilst using "power output" can mean it objects to you joining pins together even when that's okay in some situations.

Therefore, I have adopted the following methodology for deciding the electrical type of a given power pin:
 1. Where I have been able to determine that a given power pin is internally disconnected by default, I have set the electrical type to "Unconnected".
 2. Where I have been able to determine that a given power pin must necessarily be a Power Output, I have set the electrical type to "Power Output". 
 3. In any other circumstance, or where I am lacking information, I have set the electrical type to "Power Input" as this presents the least issues. This means if you're actually using any of these power pins as 'Power Outputs' in your design, by default the ERC will complain that the relevant nets are undriven. To fix this you will need to add the special "PWR_FLAG" component to the affected net.
 
Two concrete examples:
 - For the Arduino Nano 33 BLE, the 5V pin is disconnected by default so it is assigned "Unconnected". The GND and 3.3V pins can be either inputs or outputs depending on how the module is being powered, so they are assigned "Power Input". VIN can only ever be used as an input, so it too is assigned "Power Input".
 - For the Arduino 101, both the 5V and 3.3V rails are used by internal circuitry of the module, and the module will create its own 3.3V rail from the 5V rail, thus the 3.3V pins must necessarily be a "Power Output" and is assigned as such. The GND, 5V and VIN pins can be either inputs or outputs depending on how the module is being powered, so they are assigned "Power Input".

### Reset
Reset pins on Arduino modules have interesting electrical characteristics, which mean that no KiCad electrical type exactly matches their functionality. I settled on "open collector" as the nearest candidate, but unlike a true open collector pin on an integrated circuit, the reset pins on Arduino modules have an internal weak pull-up and a reset button that can strongly pull low, so your design needs to be able to cope with all these situations. In other words, if you use the reset pin as an input to your PCB then you do not need to add a pull-up (doing so will actually make it less responsive if not break it); conversely if you want to drive the reset line in order to reset the module from your PCB, you need to ensure that you only ever pull it low: if you pull it high at the same time as an unwitting user hits the physical reset button, you've created a short between power and ground through the microcontroller: this would be very bad.

### TL;DR:

*The KiCad ERC cannot catch all the possible electrical errors on your design as it doesn't natively support the reset and power pins' electrical types. Even if the ERC says it's OK, double check it manually.*

*If the ERC says that your power pins are undriven, first manually check they are being driven. If they are driven, then add a "PWR_FLAG" component to the net to make the error go away.*
