# Category


* [Hardware Versions](https://github.com/96boards-hikey/tools-images-hikey960/blob/master/README.md#hardware-versions)
* [Simple Rescue Flashing](https://github.com/96boards-hikey/tools-images-hikey960/blob/master/README.md#simple-rescue-flashing)

## Hardware Versions

There are two versions of HiKey960: v1 and v2. One important difference you should know is: v1 is using Jumper (J2001), while v2 is using DIP switch (SW2201). Both are located in the bottom side of board.

* Jumper Pin 1-2 = DIP switch 1  (Auto power)
* Jumper Pin 3-4 = DIP switch 2  (Boot mode - "Recovery mode")
* JUmper Pin 5-6 = DIP switch 3  (Ext boot - "Fastboot mode")

## Simple Rescue Flashing

This document descirbes the steps to rescue flash the base firmware for the HiKey960 through the OTG port.

### Step 1: Set the board to recovery/forced-download mode:

* Remove power from the board
* Change Jumper/DIP switch settings, to enter recovery/forced-download mode:

Name          | Link / Switch       | State
------------- | ------------------- | ----------
Auto Power up | Link 1-2 / Switch 1 | closed / ON
Recovery      | Link 3-4 / Switch 2 | closed / ON
Fastboot      | Link 5-6 / Switch 3 | open / OFF

* Apply power to the board using [96Boards compliant power supply](http://www.96boards.org/product/power/)
* Insert USB Type-C cable (OTG port) to the board, and connect the other end to your Linux PC
* Check whether there is a device node "/dev/ttyUSBx". If there is, it means your PC has detected the target board; If there is not, try to repeat previous steps.

### Step 2: Flash the recovery image

Once again using the terminal on your host machine, execute the following command. Be sure to replace /dev/ttyUSBx with the USB value detected by your machine.

```sh
./recovery-flash.sh /dev/ttyUSBx
```

After it completes, the base firmware will be flashed to the device, this does not mean OS.

The board will then be in fastboot mode.

### Step 3: Set the board back to normal boot or fastboot mode.

- Remove power from the board
- Change Jumper settings, to use normal boot or fastboot mode

**Normal boot mode**

Name          | Link / Switch       | State
------------- | ------------------- | ----------
Auto Power up | Link 1-2 / Switch 1 | closed / ON
Recovery      | Link 3-4 / Switch 2 | oepn / OFF
Fastboot      | Link 5-6 / Switch 3 | open / OFF

**Fastboot mode**

Name          | Link / Switch       | State
------------- | ------------------- | ----------
Auto Power up | Link 1-2 / Switch 1 | closed / ON
Recovery      | Link 3-4 / Switch 2 | open / OFF
Fastboot      | Link 5-6 / Switch 3 | closed / ON
- Connect 1-2/DIP switch 1 ON

- Apply power to the board using 96Boards compliant power supply

## Troubleshooting

* If you run into trouble, see the [README-technical.md](README-technical.md) file in this directory.


