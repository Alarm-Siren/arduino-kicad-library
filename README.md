# Arduino KiCad Library
*Version 2.0.1*

Library of schematic components and footprints of common Arduino boards for KiCad.

Currently included are:
- Arduino 101 Shield
- Arduino Due Shield
- Arduino Leonardo Shied
- Arduino M0 Shield
- Arduino M0 Pro Shield
- Arduino Mega 2560 Shield
- Arduino Micro Socket
- Arduino Mini Socket
- Arduino Nano Socket
- Arduino Uno Shield
- Arduino Zero Shield
- Arduino Pro Mini Socket
- Pro Mini Clone Socket

Shield means the Arduino is designed to plug in from beneath your PCB; socket means it is designed to plug in from above.

# Compatibility with KiCad 5
This library is in the new KiCad 6 "S-Expressions" format, and is not compatible with KiCad 5. If you need compatibility with KiCad 5, please use version 1.4.1 of this repository - but be aware that said version does not contain all features and is not being maintained.

## Comments, Requests, Bugs & Contributions
All are welcome.  
Please file an Issue or Pull Request at https://github.com/Alarm-Siren/arduino-kicad-library

## License
Copyright 2017-2022, Nicholas Parks Young. All Rights Reserved.  
This library is licensed under the GNU LGPL v2.1, which can be found in file LICENSE.txt.

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
On the Arduino Platform, it is not possible to categorically state that the power pins are "power inputs" or "power outputs", as that depends on exactly how you're using the Arduino. For example, if you're powering the Arduino from USB then GND, +3.3V and +5V would be power outputs and VIN would do nothing, whereas if you're powering the Arduino from a battery via your Shield then VIN and GND are power inputs whilst +5V and +3.3V are power outputs. There are other, more esoteric possibilities too.

Regardless of the above, I needed to make a decision about what electrical type to apply to these pins. I could use something like Passive or Unspecified, but then KiCad's Electrical Rules Checker (ERC) tool would not be effective in catching errors on these pins at all, whilst using Power Output means it objects to you joining pins together (for example, joining all the GND pins into a common net) even when that's OK in some situations.

Therefore, I have decided to use Power Input as this presents the least issues. This means if you're actually using any of the power pins as Power Outputs in your schematic, by default the ERC will complain that the relevant nets are undriven. To fix this you will need to add the special "PWR_FLAG" component to the affected net.

NOTE: As of version 2.0.0, on the 5V-based Arduino boards the 3.3V output pin has been changed to Power Output, as these will be powered by an on-board regulator and should not have external power fed into them.

### Reset
Reset pins on the Arduino Platform have interesting electrical characteristics, which mean that no KiCad electrical type exactly matches their functionality. I settled on Open Collector as the nearest candidate, but unlike a true Open Collector pin on an integrated circuit, the reset pins on the Arduino Platform have an internal weak pull-up, and the reset button that can strongly pull low, so your circuit needs to be able to cope with all these situations.

In other words, if you use the reset pin as an input to your shield then you do not need to add a pull-up (doing so will actually make it less responsive if not break it); conversely if you want to drive the reset line in order to reset the Arduino you need to ensure that you only ever pull it low - if you pull it high at the same time as an unwitting user hits the physical reset button, you've created a short between power and ground which will likely fry whatever chip is on your shield.

### TL;DR:

*The KiCad ERC cannot catch all the possible electrical errors on your schematic as it doesn't natively support the reset and power pins' electrical types. Even if the ERC says its OK, double check it manually.*

*If the ERC says that your power pins are undriven, first manually check they are being driven. If they are driven, then add a "PWR_FLAG" component to the net to make the error go away.*
