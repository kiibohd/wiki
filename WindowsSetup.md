# Docker

**Recommended (a)**

The easiest option is to setup [Docker](../../controller/tree/master/Dockerfiles) for your computer and use a native Linux compiler to build/test the firmware.
This should work for Windows 7+.

You'll need to have `git` installed in order to download the source code.

# Windows 10+ - Windows Subsystem for Linux

**Recommended (b)**

This is the next easiest option, just follow the instructions for [Ubuntu Linux](https://github.com/kiibohd/controller/wiki/Linux-Setup#ubuntu).

All Linux steps apply. **Except** when it comes to DFU and loading the firmware onto the keyboard.

# Windows 10 and Lower - Cygwin

Building on Windows should be fine for 99% of users, but takes a bunch of work to setup (because Windows is a crappy dev environment).
Cygwin is currently required along with some non-Cygwin compilers and utilities (because they are not available for Cygwin).
The dfu Bootloader will not build because of a Make 3.81+ bug/feature that removed support for non-Unix (Windows) filenames as dependencies of targets.
If you [replace the version of Make in Cygwin](http://stackoverflow.com/questions/601516/cygwin-make-error-target-pattern-contains-no) it should work.
However, make sure that the flash size is no larger than 4096 Bytes or the bootloader will not work. Things will likely break if there are **SPACES IN YOUR PATHS**. I install cygwin to `C:\cygwin64`.
If you are brave and have programming knowledge, I will accept patches to fix any issues
regarding spaces in paths.

## Cygwin

First make sure Cygwin is installed - http://www.cygwin.com/ - 32bit or 64bit
is fine. Make sure the following are installed:

- make
- git (needed for some compilation info)
- cmake
- gcc-core
- gcc-g++
- libusb1.0
- libusb1.0-devel
- python3
- ctags (recommended, not required)

Please note, I use cygwin term exclusively for any command line options.
Unless mentioned otherwise, use it. Do NOT use CMD or Powershell.

## CMake

Also install the [Windows version of CMake](http://cmake.org/cmake/resources/software.html) (3+ is ideal) - Select "Do not add CMake to system PATH".
This is in addition to the Cygwin version.
This is an easier alternative to installing another C compiler.
Add the following lines to your .bashrc, making sure the CMake path is correct:

```bash
echo "export wincmake_path='/cygdrive/c/Program Files/CMake/bin'" >> ~/.bashrc
```

**OR**

```bash
echo "export wincmake_path='/cygdrive/c/Program Files (x86)/CMake/bin'" >> ~/.bashrc
```

And if you want to run wincmake manually:

```bash
echo "alias wincmake=\"PATH='\$wincmake_path':'\${PATH}' cmake -G 'Unix Makefiles'\"" >> ~/.bashrc
```

## Python 3

Along with the Cygwin version of Python 3, you'll also need the Windows version of Python 3.
This is due to complications of requiring a non-Cygwin ARM compiler for KLL compilation.

Please install the latest stable version of [Python 3](https://www.python.org/downloads/windows/).

## Serial Drivers

**Note** Skip this step if you are using Windows 10 or higher, driver is installed automatically.

Install the [PJRC Virtual Serial Port Driver](http://pjrc.com/teensy/serial_install.exe).
This is necessary to communicate with the keyboards virtual terminal. It is not needed to build, but can be very helpful in debugging.

Next, install the compiler(s) you want.

## AVR GCC

AVR is used for "older" chips such as the Teensy 1.0(++), Teensy 2.0(++).

You just need the [Atmel AVR 8-bit Toolchain](http://www.atmel.com/tools/atmelavrtoolchainforwindows.aspx).
The latest should be fine, as of writing it was 3.4.3.

Extract the files to a directory, say `C:\avr8-gnu-toolchain`.
Then copy all the folders in that directory to the Cygwin `/usr/local` directory.
Mine is `C:\cygwin64\usr\local` (You can also just setup the paths, but this is
faster/simpler. Might screw up your Cygwin though).

## ARM EABI

ARM is used for "newer" chips such as Teensy 3.0/3.1, Infinity Keyboard, McHCK, etc.

Download the latest
[GNU Tools for Embedded Processors
gcc-arm-none-eabi](https://launchpad.net/gcc-arm-embedded/+download).

Download `gcc-arm-none-eabi*win32.zip`.

Then extract all the folders/files in the zip to the Cygwin `/usr/local` directory.
Mine is `C:\cygwin64\usr\local`.
Or, you can setup paths using the installer (you have to be more careful, avoid spaces in paths).

# What's next

Please see [[Configuration|Configuration]] to setup your keyboard.
