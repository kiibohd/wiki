**Caveat:** It is unlikely this project will support the Teensy-LC as the SRAM specs are a bit on the low side (though it is possible)

# Define your matrix

First you need to define your keyboard matrix. Refer to the [Deskthority wiki](http://deskthority.net/wiki/KiCAD_keyboard_PCB_design_guide) if you are unsure about how to connect the switches.

From here you'll have an n x m matrix. Where n are the columns/strobes and m are rows/sense lines.

# Choose pins on the Teensy

You may choose any of the pins from 0 to 33; however, I recommend against using pin 13 as it is for the debug led (a lot harder to debug if things go really wrong). Pins 28 to 33 are on the underside of the Teensy PCB so they can be tricky to use unless you have a breakout pcb, like this [one](https://www.tindie.com/products/loglow/teensy-31-breakout/).

Unfortunately for us, [PJRC](http://pjrc.com) choose annoying names for all the pins which do not make sense from the firmware side. This means we have to map the PJRC gpio pin number to the actual GPIO pin.

| Pin | Name | Pin | Name | Pin | Name |
|-----|------|-----|------|-----|------|
| 0   | B16  | 13  | C5   | 26  | E1   |
| 1   | B17  | 14  | D1   | 27  | C9   |
| 2   | D0   | 15  | C0   | 28  | C8   |
| 3   | A12  | 16  | B0   | 29  | C10  |
| 4   | A13  | 17  | B1   | 30  | C11  |
| 5   | D7   | 18  | B3   | 31  | E0   |
| 6   | D4   | 19  | B2   | 32  | B18  |
| 7   | D2   | 20  | D5   | 33  | A4   |
| 8   | D3   | 21  | D6   |     |      |
| 9   | C3   | 22  | C1   |     |      |
| 10  | C4   | 23  | C2   |     |      |
| 11  | C6   | 24  | A5   |     |      |
| 12  | C7   | 25  | B19  |     |      |

[More detailed Teensy 3 pin mappings](https://github.com/kiibohd/controller/blob/master/Lib/pin_map.teensy3)

# Get the source code ready and compiling

**Note**: I suggest you fork this git repository first, if anything it makes it easier to backup your code and ask for help.

1. Setup machine so you can build the source code: https://github.com/kiibohd/controller/wiki
2. Download the source code: `git clone https://github.com/kiibohd/controller.git`
3. Try to build the default firmware to make sure everything is setup correctly: https://github.com/kiibohd/controller/wiki/Building

# Create a new Scan Module

Figure out what you want to call your keyboard. I'll be naming the example **kiilulz**. For most keyboards the easiest thing to do is to copy the **MD1** keyboard as it is a simple keyboard without any additional hardware features.

```bash
cd controller/Scan
cp -r MD1 kiilulz
cd ..
```

Next create a new build script (so you don't have to enter really long CMake incantations).

```bash
cd Keyboards
cp template.bash kiilulz.bash
```

We need to change three settings in kiilulz.bash:
* BuildPath to `kiilulzing`
* ScanModule to `kiilulz`
* Chip

Chip will be either be "mk20dx128" for Teensy 3.0 or "mk20dx256" for Teensy 3.1/2.

Now, try to run this script to see if you've done everything correctly so far.

```bash
./kiilulz.bash
```

Example output.
```bash
-- Compiler Family:
arm
-- Compiler Selected:
gcc
-- Chip Selected:
mk20dx128
-- Chip Family:
mk20dx
-- CPU Selected:
cortex-m4
-- Compiler Source Files:
Lib/mk20dx.c;Lib/delay.c
-- Bootloader Type:
Teensy
-- Detected Scan Module Source Files:
Scan/MatrixARM/matrix_scan.c;Scan/kiilulz/scan_loop.c
-- Detected Macro Module Source Files:
Macro/PartialMap/macro.c
-- Detected Output Module Source Files:
Output/pjrcUSB/output_com.c;Output/pjrcUSB/arm/usb_desc.c;Output/pjrcUSB/arm/usb_dev.c;Output/pjrcUSB/arm/usb_joystick.c;Output/pjrcUSB/arm/usb_keyboard.c;Output/pjrcUSB/arm/usb_mem.c;Output/pjrcUSB/arm/usb_mouse.c;Output/pjrcUSB/arm/usb_serial.c
-- Detected Debug Module Source Files:
Debug/cli/cli.c;Debug/led/led.c;Debug/print/print.c
-- Found Git: /usr/bin/git (found version "2.6.4") 
-- Found Ctags: /usr/bin/ctags (found version "5.8") 
-- Detected Layout Files:
/home/hyatt/Source/controller/Scan/MatrixARM/capabilities.kll
/home/hyatt/Source/controller/Macro/PartialMap/capabilities.kll
/home/hyatt/Source/controller/Output/pjrcUSB/capabilities.kll
/home/hyatt/Source/controller/Scan/kiilulz/defaultMap.kll
/home/hyatt/Source/controller/kll/layouts/md1Overlay.kll
/home/hyatt/Source/controller/kll/layouts/stdFuncMap.kll
/home/hyatt/Source/controller/kll/layouts/hhkbpro2.kll
/home/hyatt/Source/controller/kll/layouts/colemak.kll
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hyatt/Source/controller/Keyboards/kiilulzing
[  5%] Generating KLL Layout
Scanning dependencies of target kiibohd.elf
[ 10%] Building C object CMakeFiles/kiibohd.elf.dir/main.c.o
[ 15%] Building C object CMakeFiles/kiibohd.elf.dir/Lib/mk20dx.c.o
[ 20%] Building C object CMakeFiles/kiibohd.elf.dir/Lib/delay.c.o
[ 25%] Building C object CMakeFiles/kiibohd.elf.dir/Scan/MatrixARM/matrix_scan.c.o
[ 30%] Building C object CMakeFiles/kiibohd.elf.dir/Scan/kiilulz/scan_loop.c.o
[ 35%] Building C object CMakeFiles/kiibohd.elf.dir/Macro/PartialMap/macro.c.o
[ 40%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/output_com.c.o
[ 45%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_desc.c.o
[ 50%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_dev.c.o
[ 55%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_joystick.c.o
[ 60%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_keyboard.c.o
[ 65%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_mem.c.o
[ 70%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_mouse.c.o
[ 75%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_serial.c.o
[ 80%] Building C object CMakeFiles/kiibohd.elf.dir/Debug/cli/cli.c.o
[ 85%] Building C object CMakeFiles/kiibohd.elf.dir/Debug/led/led.c.o
[ 90%] Building C object CMakeFiles/kiibohd.elf.dir/Debug/print/print.c.o
[ 95%] Linking C executable kiibohd.elf
Creating iHex file to load:    kiibohd.teensy.hex
Creating Extended Listing:     kiibohd.lss
Creating Symbol Table:         kiibohd.sym
[ 95%] Built target kiibohd.elf
Scanning dependencies of target SizeAfter
[100%] Chip usage for mk20dx128
         SRAM:  45%     7448/16384      bytes
        Flash:  21%     28676/131072    bytes
[100%] Built target SizeAfter
Firmware has been compiled into: 'kiilulzing'
/home/hyatt/Source/controller/Keyboards
```

# Setup rows and columns

Now that the firmware compiles and we've created a separate Scan Module for changes, we can setup the firmware to use your defined rows and columns.

```bash
cd ..
cd Scan/kiilulz
```

The file we'll be editing first is `matrix.h`. If you have B3, B4, and A9 as columns and C3, C4, E9 as rows you'll set Matrix_cols and Matrix_rows as follows.

```C
GPIO_Pin Matrix_cols[] = { gpio(B,3), gpio(B,4), gpio(A,9) };
GPIO_Pin Matrix_rows[] = { gpio(C,3), gpio(C,4), gpio(E,9) };
```

Usually, if you've been following Teensy 2-like tutorials you can leave `Config Matrix_type = Config_Pulldown`. This configures the pull resistor on the row/sense side of the matrix.
* Config_Pulldown - Pull-down resistor
* Config_Pullup - Pull-up resistor
* Config_Opendrain - No pull resistor, use if you have external pull resistors

Don't use Open-drain unless you know what you are doing (or you'll get odd behaviour).

Make sure your changes worked.

```bash
cd ../../Keyboards
./kiilulz.bash
```

# Define the defaultMap.kll

Normally, you'd have to calculate the Scan Code of every key manually and set what you want the key to be. Fortunately, I'm lazy, so I've made this easy to do.
Since your firmware is nearly ready (except the defaultMap and layers) you can already start to try it out.

## Load firmware onto Teensy

In short you just need to get the kiibohd.teensy.hex file onto the Teensy. I've created a small script that **should** work, otherwise you can use the [Teensy Loader](http://pjrc.com/teensy/loader.html).

First, press the flash button on the Teensy. Then load the `.hex` file.

```bash
cd Keyboards/kiilulzing
./load
```

If the flashing was successful (and you haven't used pin 13) the debug led should turn off when flash completes.

## Accessing the debug cli

To figure out which Scan Codes we each key is mapped to we need to access the debug cli. Follow this wiki https://github.com/kiibohd/controller/wiki/Debugging to get access.

Once you have access to the cli enter the following command.

```bash
matrixDebug
```

Now, every time you press a key a Scan Code will print out. If your matrix pins were assigned in order (matrix.h), then you may even have sequential Scan Codes.

## Editing defaultMap.kll

```bash
cd Scan/kiilulz
```

Now that we can figure out where the Scan Codes are we can just edit the `defaultMap.kll`. In general the syntax is pretty straight forward. You can refer to the KLL spec for a complete syntactic reference: http://input.club/kll

For example if Scan Code 0x42 was mapped to Enter then you would set the following in `defaultMap.kll`.

```
S0x42 : U"Enter"
```

S is the prefix for Scan Codes and U is the prefix for USB codes.

**Note**: USB defines all keys as USB ANSI, so international keys have too be mapped to their equivalent. There is an automatic KLL mapping planned at some point, please file/check issues to see the status of this.

Once you've defined the full `defaultMap.kll` you should have a basic keyboard ready to go :D 

## Layers, Macros
More advanced topics like Macros, Layers etc. are covered in next wiki page: [[Layers, Macros|Layers, Macros]].
