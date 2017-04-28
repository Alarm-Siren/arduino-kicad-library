# Arduino KiCad Library
Library of schematic components and footprints of common Arduino boards for KiCAD.

Currently included are:
- Arduino 101 Shield
- Arduino Due Shield
- Arduino Leonard Shied
- Arduino Mega 2560 Shield
- Arduino Micro Socket
- Arduino Uno Shield
- Arduino Zero Shield

Shield means the Arduino is designed to plug in from beneath your PCB; socket means it is designed to plug in from above.

## Library Setup
To add this library to your KiCad Project, do the following steps:
1. Copy the source files to your Project. Make sure that the Arduino.pretty folder structure is preserved.
2. In EeSchema (the schematic editor of KiCad) go to Preferences -> Component Libraries. Click the "Add" button next to "Component library files".
3. Navigate to your project folder, select "arduino.lib" and click "open".
4. You may wish to adjust the newly added arduino schematic library to be near the top of the load order using the "Up" and "Down" buttons, but this is optional and is only relevant if you have other libraries that use the same names for parts.
5. OK out and exit EeSchema. Open PcbNew (the PCB editor of KiCad) go to Preferences -> Footprint Libraries Manager.
6. Select the "Project Specific Libraries" tab and then click "Append Library".
7. In the new line of the table, set Library Path to "$(KIPRJMOD)\Arduino.pretty" and ensure Plugin Type is "KiCad". Options and Description can be left blank. You should set Nickname to something descriptive - like "Arduino" for example!
8. All done: you are now ready to use these schematic components and footprints!

## Comments, Requests, Bugs & Contributions
All are welcome. Please file an "Issue" in the Bug Tracker.

## License
This library is licensed under the GNU LGPL v2.1, which can be found in file LICENSE.txt.
