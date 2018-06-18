# Arduino KiCad Library
*Version 1.4.1*

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

Shield means the Arduino is designed to plug in from beneath your PCB; socket means it is designed to plug in from above.

## Comments, Requests, Bugs & Contributions
All are welcome.  
Please file an Issue or Pull Request at https://github.com/Alarm-Siren/arduino-kicad-library

## License
Copyright 2017-2018, Nicholas Parks Young. All Rights Reserved.  
This library is licensed under the GNU LGPL v2.1, which can be found in file LICENSE.txt.

## Donations

If you've found this library useful and you'd like to make a donation towards its continued upkeep, click the button below:

[![paypal](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UX25HM4CZFFWW)

## Library Setup
To add this library to your KiCad Project, do the following steps:
1. Copy the source files to your Project. Make sure that the Arduino.pretty folder structure is preserved.
2. In Eeschema (the schematic editor of KiCad) go to Preferences -> Component Libraries. Click the "Add" button next to "Component library files".
3. Navigate to your project folder, select "arduino.lib" and click "open".
4. You may wish to adjust the newly added arduino schematic library to be near the top of the load order using the "Up" and "Down" buttons, but this is optional and is only relevant if you have other libraries that use the same names for parts.
5. OK out and exit Eeschema. Open Pcbnew (the PCB editor of KiCad) go to Preferences -> Footprint Libraries Manager.
6. Select the "Project Specific Libraries" tab and then click "Append Library".
7. In the new line of the table, set Library Path to "$(KIPRJMOD)\Arduino.pretty" on Windows or "$(KIPRJMOD)/Arduino.pretty" on Linux/Mac, and ensure Plugin Type is "KiCad". Options and Description can be left blank. You should set Nickname to something descriptive - like "Arduino" for example!
8. All done: you are now ready to use these schematic components and footprints!

## A note about Power and Reset pins

### Power
On the Arduino Platform, it is not possible to categorically state that the power pins are "power inputs" or "power outputs", as that depends on exactly how you're using the Arduino. For example, if you're powering the Arduino from USB then GND, +3.3V and +5V would be power outputs and VIN would do nothing, whereas if you're powering the Arduino from a battery via your Shield then VIN and GND are power inputs whilst +5V and +3.3V are power outputs. There are other, more esoteric possibilities too.

Regardless of the above, I needed to make a decision about what electrical type to apply to these pins. I could use something like Passive or Unspecified, but then KiCad's Electrical Rules Checker (ERC) tool would not be effective in catching errors on these pins at all, whilst using Power Output means it objects to you joining pins together (for example, joining all the GND pins into a common net) even when that's OK in some situations.

Therefore, I have decided to use Power Input as this presents the least issues. This means if you're actually using any of the power pins as Power Outputs in your schematic, by default the ERC will complain that the relevant nets are undriven. To fix this you will need to add the special "PWR_FLAG" component to the affected net.

### Reset
Reset pins on the Arduino Platform have interesting electrical characteristics, which mean that no KiCad electrical type exactly matches their functionality. I settled on Open Collector as the nearest candidate, but unlike a true Open Collector pin on an integrated circuit, the reset pins on the Arduino Platform have an internal weak pull-up, and the reset button that can strongly pull low, so your circuit needs to be able to cope with all these situations.

In other words, if you use the reset pin as an input to your shield then you do not need to add a pull-up (doing so will actually make it less responsive if not break it); conversely if you want to drive the reset line in order to reset the Arduino you need to ensure that you only ever pull it low - if you pull it high at the same time as an unwitting user hits the physical reset button, you've created a short between power and ground which will likely fry whatever chip is on your shield.

### TL;DR:

*The KiCad ERC cannot catch all the possible electrical errors on your schematic as it doesn't natively support the reset and power pins' electrical types. Even if the ERC says its OK, double check it manually.*

*If the ERC says that your power pins are undriven, first manually check they are being driven. If they are driven, then add a "PWR_FLAG" component to the net to make the error go away.*
