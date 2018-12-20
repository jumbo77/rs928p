Backup and Restore
db4ple edited this page on Jul 30 · 6 revisions
There is a number of reason why you should backup your precious configuration data, since it includes all the calibration information but also the display settings.

The some of the operation and and most configuration data of the UHSDR TRX is stored in a non-volatile memory, and read at startup from the non-volatile memory. During normal shutdown or when the user explicitly saves the configuration, this data is written to the non-volatile memory. The UHSDR supports two types of non-volatile memory:

Internal Flash Memory: That memory is built into the MCU. Every UHSDR TRX has such a flash memory. If only this flash memory is available (no external I2C EEPROM), it will be the primary configuration storage, from/to which the UHSDR firmware reads/writes the configuration at startup/shutdown.
External I2C EEPROM Memory: If installed (it is optional but recommended) and above the minimal size (32k or larger), this will be automatically the primary configuration storage, from/to which the UHSDR firmware reads/writes the configuration at startup/shutdown. Internal flash becomes in this case secondary storage, where a single configuration can be stored to and restored from. See below for more information on backup/restore.
Backup / Restore in Flash Memory
If you have an suitable EEPROM installed, the firmware can backup its configuration date (settings, calibration) into the MCU flash for later restore in case of problems or when trying out a new firmware.

Backup: This is simple, you go to the Standard menu, run "Backup Config", this will save your current configuration in the Flash area.

Restore: This is also simple but more dangerous, you go to the Standard menu, run "Restore Config", this will read the configuration in the Flash area AND THEN OVERWRITES YOUR EXISTING CONFIGURATION. Be careful!

Backup / Restore on External Computer (since 2.9.19)
DISCLAIMER: This is experimental! Restoring a configuration from other TRX may completely destroy your configuration and make your TRX behave weird. You have been warned.

These actions will backup and restore the data in the currently active primary configuration storage (either I2C EEPROM or flash, see above).

Requirements
To use this, you have to install UHSDR 2.9.19 or newer. No earlier firmware will work. The method uses the extended CAT commands (see https://github.com/df8oe/UHSDR/wiki/USB-CAT-and-AUDIO-Mode#extended-cat-command-set-from-2918), so a USB connection is required.

As a Windows (!) user, you may use the executable in uhsdr_tool.zip. Be aware, this is a command line tool designed to run from a command prompt window (e.g. "cmd.exe"). Just double clicking the executable will get you nowhere. Parameters are identical to the examples given below, just replace python uhsdr_tool.py with uhsdr_tool.exe

Otherwise

you will need Python (both latest 2.x and 3.x should work) to be installed. You also need pySerial to be installed. We will soon published a executable file at least for Windows, which will eliminate the need for a Python install.
And of course, the script uhsdr_tool.py from here: https://github.com/df8oe/UHSDR/tree/active-devel/mchf-eclipse/support/python
How to operate
Now run the script, under Linux or if python has been added to your Windows system path this is simple:

python uhsdr_tool.py -p 0 -b
will use COM0 (Windows) or /dev/ttyACM0 (Linux) and write to uhsdr_config.json

python uhsdr_tool.py -p 0 -r
will use COM0 (Windows) or /dev/ttyACM0 (Linux) and restore your configuration from uhsdr_config.json.

python uhsdr_tool.py -h
will show the help text with all available options.

python uhsdr_tool.py
will identify the serial port the UHSDR is connected to.
