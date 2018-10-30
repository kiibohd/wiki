This page describes how to build the keyboard firmware.
If you wish to compile the bootloader instead,
see the [[Bootloader|Bootloader]] page.

# If you are new to this, try using the compilation scripts [HERE](https://github.com/kiibohd/controller/tree/master/Keyboards)

Fewer things to mess up.

## Building

From the main directory, run:

```bash
$ mkdir build
$ cd build
$ cmake ..
$ make
```

**Note:** If you are using windows, please use "wincmake" instead of "cmake"

Example output:

```
$ cmake ..
-- Compiler Family:
arm
-- Chip Selected:
mk20dx128vlf5
-- Chip Family:
mk20dx
-- CPU Selected:
cortex-m4
-- Compiler Source Files:
Lib/mk20dx.c;Lib/delay.c
-- Bootloader Type:
dfu
-- Detected Scan Module Source Files:
Scan/MD1/scan_loop.c;Scan/MD1/../MatrixARM/matrix_scan.c
-- Detected Macro Module Source Files:
Macro/PartialMap/macro.c
-- Detected Output Module Source Files:
Output/pjrcUSB/output_com.c;Output/pjrcUSB/arm/usb_desc.c;Output/pjrcUSB/arm/usb_dev.c;
Output/pjrcUSB/arm/usb_keyboard.c;Output/pjrcUSB/arm/usb_mem.c;Output/pjrcUSB/arm/usb_serial.c
-- Detected Debug Module Source Files:
Debug/full/../cli/cli.c;Debug/full/../led/led.c;Debug/full/../print/print.c
-- Found Git: /usr/bin/git (found version "2.2.1")
-- Found Ctags: /usr/bin/ctags (found version "5.8")
-- Checking for latest kll version:
Current branch master is up to date.
-- Detected Layout Files:
/home/hyatt/Source/controller/Macro/PartialMap/capabilities.kll
/home/hyatt/Source/controller/Output/pjrcUSB/capabilities.kll
/home/hyatt/Source/controller/Scan/MD1/defaultMap.kll
/home/hyatt/Source/controller/kll/layouts/md1Overlay.kll
/home/hyatt/Source/controller/kll/layouts/stdFuncMap.kll
/home/hyatt/Source/controller/kll/layouts/hhkbpro2.kll
-- Configuring done
-- Generating done
-- Build files have been written to: /home/hyatt/Source/controller/build
[master]: make                                [~/Source/controller/build](hyatt@x230mas:pts/6)
[  5%] Generating KLL Layout
Scanning dependencies of target kiibohd.elf
[ 11%] Building C object CMakeFiles/kiibohd.elf.dir/main.c.o
[ 17%] Building C object CMakeFiles/kiibohd.elf.dir/Lib/mk20dx.c.o
[ 23%] Building C object CMakeFiles/kiibohd.elf.dir/Lib/delay.c.o
[ 29%] Building C object CMakeFiles/kiibohd.elf.dir/Scan/MD1/scan_loop.c.o
[ 35%] Building C object CMakeFiles/kiibohd.elf.dir/Scan/MatrixARM/matrix_scan.c.o
[ 41%] Building C object CMakeFiles/kiibohd.elf.dir/Macro/PartialMap/macro.c.o
[ 47%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/output_com.c.o
[ 52%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_desc.c.o
[ 58%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_dev.c.o
[ 64%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_keyboard.c.o
[ 70%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_mem.c.o
[ 76%] Building C object CMakeFiles/kiibohd.elf.dir/Output/pjrcUSB/arm/usb_serial.c.o
[ 82%] Building C object CMakeFiles/kiibohd.elf.dir/Debug/cli/cli.c.o
[ 88%] Building C object CMakeFiles/kiibohd.elf.dir/Debug/led/led.c.o
[ 94%] Building C object CMakeFiles/kiibohd.elf.dir/Debug/print/print.c.o
Linking C executable kiibohd.elf
[ 94%] Built target kiibohd.elf
Scanning dependencies of target SizeAfter
[100%] Chip usage for mk20dx128vlf5
     SRAM:  32%     5384/16384      bytes
    Flash:  18%     23384/126976    bytes
[100%] Built target SizeAfter
```

If you see "Build files have been written" then you are good. If you have errors then you are probably missing some software, so please see your OS's setup page.

### NOTES:

If you are on Windows and get the following error, you have not setup wincmake correctly:

```bash
$ make
[  5%] Generating KLL Layout
Scanning dependencies of target kiibohd.elf
[ 11%] Building C object CMakeFiles/kiibohd.elf.dir/main.c.o
../main.c:28:19: fatal error: macro.h: No such file or directory
 #include <macro.h>
                   ^
compilation terminated.
CMakeFiles/kiibohd.elf.dir/build.make:67: recipe for target 'CMakeFiles/kiibohd.elf.dir/main.c.o' failed
make[2]: *** [CMakeFiles/kiibohd.elf.dir/main.c.o] Error 1
CMakeFiles/Makefile2:98: recipe for target 'CMakeFiles/kiibohd.elf.dir/all' failed
make[1]: *** [CMakeFiles/kiibohd.elf.dir/all] Error 2
Makefile:75: recipe for target 'all' failed
make: *** [all] Error 2
```

If you have already added the line to your `~/.bashrc` try restarting your
cygwin shell. Please see [[Windows Setup|Windows Setup]]

If you are on Windows and get these (or similar) errors:

```
Linking C executable kiibohd.elf
../Lib/CMake/writer: line 6: $'\r': command not found
../Lib/CMake/writer: line 8: $'\r': command not found
: numeric argument required: exit: 127
[100%] Chip usage for mk20dx256
../Lib/CMake/sizeCalculator: line 9: $'\r': command not found
../Lib/CMake/sizeCalculator: line 10: $'\r': command not found
../Lib/CMake/sizeCalculator: line 11: syntax error near unexpected token `$'in\r''
'./Lib/CMake/sizeCalculator: line 11: `case "$2" in
CMakeFiles/SizeAfter.dir/build.make:49: recipe for target 'CMakeFiles/SizeAfter' failed
make[2]: *** [CMakeFiles/SizeAfter] Error 2
```

You have to replace line endings to Unix like (without \r) in those files:
Lib/CMake/writer and Lib/CMake/sizeCalculator, save them and run make again.
This can be done e.g. in Notepad++, menu Edit - EOL Conversion - UNIX Format.

## Installing Firmware

First place the keyboard into re-flash mode. This can be done either by
pressing the re-flash button on the PCB/Teensy. Or by entering the Kiibohd
Virtual Serial Port and using the 'reload' command.

The load script that is created during the build can install the firmware over
USB.

To load the newly built firmware, run: `./load`.

Note: If you get a permission denied error on Linux or Mac then please run the
command with sudo, or install the udev rule.

Note: On windows, be patient the first couple of times, Windows is slow at installing drivers...

### What's next

Please see the [[Debugging|Debugging]] page to fix any issues with your new firmware :)
