![KiCad Library for Arduino banner logo](/resources/banner.png)

# KiCad Symbol & Footprint Library for Arduino Modules
*Version 4.2.0*

[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active) ![Required KiCad Version](https://img.shields.io/badge/kicad-%3E%3D6.0-critical) ![License](https://img.shields.io/github/license/alarm-siren/arduino-kicad-library) ![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/alarm-siren/arduino-kicad-library) ![Symbols](https://img.shields.io/badge/symbols-61-informational) ![Downloads](https://img.shields.io/github/downloads/alarm-siren/arduino-kicad-library/total)

This is a library of KiCad schematic symbols and PCB footprints for most Arduino modules. You can use them to make your own PCB design which will effortlessly connect with your chosen Arduino module.

Currently included modules:
- Arduino **101** Shield
- Arduino **Due** Shield
- Arduino **Giga R1 WiFi** Shield
- Arduino **Leonardo** Shield
- Arduino **M0** Shield
- Arduino **M0 Pro** Shield
- Arduino **Mega 2560 R3** Shield
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
- Arduino **Nano 33 BLE** Socket / Tile
- Arduino **Nano 33 BLE Sense** Socket / Tile
- Arduino **Nano 33 BLE Sense R2** Socket / Tile
- Arduino **Nano 33 IoT** Socket / Tile
- Arduino **Nano ESP32** Socket / Tile
- Arduino **Nano Every** Socket / Tile
- Arduino **Nano RP2040 Connect** Socket / Tile
- Arduino **Nicla Sense ME** Socket / Tile
- Arduino **Nicla Vision** Socket / Tile
- Arduino **Nicla Voice** Socket / Tile
- Arduino **Pro Mini** Socket
- Arduino **Uno R1** Shield
- Arduino **Uno R2** Shield
- Arduino **Uno R3** Shield
- Arduino **Uno R3 SMD** Shield
- Arduino **Uno R4 Minima** Shield
- Arduino **Uno R4 WiFi** Shield
- Arduino **Uno WiFi R2** Shield
- Arduino **Zero** Shield
- Clone **Mega 2560 Pro** Socket
- Clone **Pro Mini** Socket

*"Shield" means the module is designed to plug in from beneath your PCB. "Socket" means the module is designed to plug in from above your PCB. "Tile" means the module is designed to be soldered directly on to your PCB using surface-mount pads.*

## KiCad Version Compatibility
This library requires at least KiCad 6 to function, and is tested on KiCad versions 6.0.8 and 7.0.2. Note that the installation procedure is different for KiCad 6 and 7; please see the [Library Installation](#library-installation) section below.

## Comments, Requests, Bugs & Contributions
All are welcome!
Please open an [Issue](https://github.com/Alarm-Siren/arduino-kicad-library/issues) or [Pull Request](https://github.com/Alarm-Siren/arduino-kicad-library/pulls), as appropriate.

## Library Installation
To install this library in your copy of KiCad, choose the correct section for your version of KiCad and follow the steps given. These instructions only cover automated installation using KiCad's built-in Package and Content Manager (PCM); manual installation is possible but not supported.

### KiCad 7

**Warning**: Do not change the nickname prefix from that given in step 4 below. If you do so KiCad will not assign the correct footprints to the symbols by default.

1. Open KiCad and open the Preferences window at "Preferences" -> "Preferences..."
2. Select the "Plugin and Content Manager" section in the left-hand pane.
3. Ensure that the "Automatically add installed libraries to the global lib table" option is ticked.
4. Ensure that the "Library nickname prefix" is set to "PCM_".
5. Ensuring that the "Check for package updates on startup" option is ticked is recommended. **(Optional)**
6. Click "OK" to close the Preferences window.
7. Click the "Plugin and Content Manager" button.
8. Select the "KiCad official repository" from the top drop-down box (if not already selected).
9. Go the Libraries tab and locate the "KiCad Library for Arduino Modules" in the list.
10. Click the "Install" button for that entry in the list.
11. Click "Apply Pending Changes".
12. Close the "Applying Package Changes" window once it has finished.
13. You should now find that this library is listed in the "Installed" tab.
14. Close the Plugin and Content Manager.
15. You may need to restart KiCad for the library installation to fully take effect. **(Optional)**
16. All done: you are now ready to use these schematic components and footprints in your projects!

### KiCad 6
**Recommendation:** If you can, you should upgrade to KiCad 7.

**Warning**: Do not change the Nicknames from those given in steps 12 and 18 below. If you do so KiCad will not assign the correct footprints to the symbols by default.

1. Open KiCad and click the "Plugin and Content Manager" button.
2. Select the "KiCad official repository" from the top drop-down box (if not already selected).
3. Go the Libraries tab and locate the "KiCad Library for Arduino Modules" in the list.
4. Click the "Install" button for that entry in the list.
5. Click "Apply Changes".
6. Close the "Applying Package Changes" window once it has finished.
7. You should now find that this library is listed in the "Installed" tab.
8. Close the Plugin and Content Manager.
9. Go to the "Preferences" -> "Manage Symbol Libraries..." menu option.
10. In the Symbol Libraries dialogue that appears, switch to the "Global Libraries" tab (if not already selected).
11. Click "Add empty row to table" button (the button with a big cross in it, beneath the table).
12. In the new line of the table, set the Nickname to "PCM_arduino-library", and ensure the Library Format is set to "KiCad".
13. In the same line of the table, set Library Path to "${KICAD6_3RD_PARTY}/symbols/com_github_alarm-siren_arduino-kicad-library/arduino-library.kicad_sym".
14. Click "OK" to close the Symbol Libraries dialogue.
15. Go to "Preferences" -> "Manage Footprint Libraries..." menu option.
16. In the Footprint Libraries dialogue that appears, switch to the "Global Libraries" tab (if not already selected).
17. Click "Add empty row to table" button (the button with a big cross in it, beneath the table).
18. In the new line of the table, set the Nickname to "PCM_arduino-library", and ensure the Library Format is set to "KiCad".
19. In the same line of the table, set Library Path to "${KICAD6_3RD_PARTY}/footprints/com_github_alarm-siren_arduino-kicad-library/arduino-library.pretty".
20. Click "OK" to close the Footprint Libraries dialogue.
21. All done: you are now ready to use these schematic components and footprints in your projects!

## Donations

I really hope you've found this library useful. If you'd like to buy me a beer in thanks for the work I put into it, you can make a donation using the button below:

[![paypal](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UX25HM4CZFFWW)

## License & Legal
Copyright 2017-2023, [Nicholas Parks Young](https://github.com/Alarm-Siren).

Except as otherwise noted, all content of this library is licensed under the 
[Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/), with the following additional exception:
> To the extent that the creation of electronic designs that use the Licensed Material can be considered to be Adapted Material, the Licensor waives Section 3 of the Public License with respect to these electronic designs and any generated files which incorporate data provided as part of the Licensed Material.

[![CC BY-SA 4.0](https://licensebuttons.net/l/by-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-sa/4.0/)

### "KiCad Library for Arduino" Banner & Icon

The two images "resources/banner.png" and "resources/icon.png" are licensed under the [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/). These images are derivatives of ["Arduino Open-Source Community: Main Logotype RGB Colors" originally created by Arduino](https://www.arduino.cc/en/trademark/community-logo). 

Original Images: Copyright 2013, [Arduino](https://www.arduino.cc/). Derived Images: Copyright 2023, [Nicholas Parks Young](https://github.com/Alarm-Siren).

[![CC BY-SA-NC 4.0](https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

### Arduino Trademark

The word "Arduino" is a registered trademark of [Arduino](https://www.arduino.cc/). This trademark is used in this library to refer to Arduino products and to identify Arduino-related non-commercial content, as permitted by Arduino's [trademark guidelines](https://www.arduino.cc/en/trademark). This project is not affiliated with nor endorsed by Arduino.

### Warranty Disclaimer

This library is provided in the hope that it will be useful, but without any warranties of any kind. Your use of this library is at your own risk. For the full warranty disclaimer, see Section 5 of the [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## FAQ

Answers to some common questions about this library.

### Is this library in active development?

Yes. For the foreseeable future, I will be providing support, bug-fixes and updating the library with any new Arduino modules as they are released.

### What does the license exception in the License & Legal section mean?

This library uses the same license as KiCad's own built-in parts library does, including the exception. The KiCad Libraries team have a [page which explains the meaning of the exception](https://www.kicad.org/libraries/license/). My version of the exception uses slightly better wording, but the effect is the same.

### Why do the footprints not have an `Edge.Cuts` outline?

If I put in an `Edge.Cuts` outline, then those users who want to have a PCB larger than the module footprint would have to modify the footprint to do so. In my experience, it is far more common for users to want a PCB larger than the module anyway, so I prefer to cater to those users. If you want your PCB to be the same size and shape as the Arduino module, you can trace the `F.Silkscreen` or `B.Silkscreen` layer (as appropriate) out in the `Edge.Cuts` layer yourself, or you can modify the footprint to change the outline from `F.Silkscreen` or `B.Silkscreen` layer to `Edge.Cuts`.

### Why do the Nicla Vision and Nicla Voice tile footprints have cut-outs?

The cut-outs are necessary to accommodate components on the back of those modules; without them the components would physically prevent you from getting the module's pads down to the footprint's SMD pads.

### Why does the whole footprint have an `F.Courtyard` or `B.Courtyard` outline? I can't place my components where I need to!

Firstly, this does not stop you from placing your components wherever you want. It does mean that the KiCad DRC will, by default, report errors or warnings in some circumstances because the module footprint and your circuit's footprints' courtyards are overlapping, but you can ignore or disable these errors/warnings without issue.

Secondly, the intention is that it acts as a warning to the user that they've put components in the 'danger zone' between their PCB and the Module. I do not model all of the tall components on the module, so it is possible that a user might unknowingly place their own tall component in a position that would conflict with one on the module. My hope is that the DRC errors/warnings will flag this potential problem to the user to manually check that their placement does not conflict with the module.

In principle I'm open to marking the taller components specifically, which would remove this issue, but this is a lot of work and requires data I don't have access to for all the modules.

### Why is this Power Pin set to Power Input/Power Output/Unconnected? I get DRC errors because of it!

The short answer is that some power pins on some modules can be used as either inputs or outputs, depending on your circuit design / where you're powering the assembly from.

For those pins where I've been able to categorically confirm that the given power pin is `Unconnected` by default, or must necessarily be a `Power Input` or a `Power Output`, I have set it as such. For those pins that can be used as either an input or output, I have set it to `Power Input` as this is the more flexible option whilst still preserving some element of DRC capability. If you're using one of these `Power Input` pins as a `Power Output` from the module, you'll need to add the special `PWR_FLAG` component to the affected net to make the DRC error go away.
