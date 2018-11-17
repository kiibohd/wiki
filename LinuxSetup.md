Package lists for some distributions are listed below.

If you do not see your distribution listed then you can still build as long as you can find the packages to install. These depend a bit on which targets you are trying to build, but the general ones are:

General

- git
- cmake (2.8 and higher)
- ctags (recommended, not required)
- python3
- libusb1.0 (and -devel)
- make (or ninja)
- gcc (necessary for host-side KLL testing)
- dfu-util

AVR Specific (Teensy 1.0/++,2.0/++) (try to use something recent, suggested
versions below)

- avr-gcc (~4.8.0)
- avr-binutils (~2.23.2)
- avr-libc (~1.8.0)

ARM Specific (Teensy 3.0/3.1, Infinity Keyboard, McHCK)

- arm-none-eabi-gcc
- arm-none-eabi-binutils
- arm-none-eabi-newlib

Debugging

- screen
- gdb
- JLinkExe

### Udev

Udev rules will allow you to flash your keyboard without needing to use sudo

```
cp 98-kiibohd.rules /etc/udev/rules.d
udevadm control --reload-rules
```

## Arch Linux

```
sudo pacman -S --needed git cmake ninja python libusb ctags gcc lsb-release
sudo pacman -S --needed avr-binutils avr-gcc avr-libc
sudo pacman -S --needed arm-none-eabi-binutils arm-none-eabi-gcc arm-none-eabi-newlib dfu-util
sudo pacman -S --needed ruby screen
sudo gem install serialport
```

## Ubuntu

NOTE: If you are on Ubuntu 12.04 LTS please make sure you have all the updates. If you are on a pre 12.04 OS please consider upgrading as the older kernel has an issue with the serial console.

Open up a terminal and run the following commands (you can copy/paste if you want). Note: You will be asked for your password - it is needed to get administrator privileges to install software. Also, you will not see anything as you type your password, it is normal, they hide the letters for security

```
sudo apt-get install git cmake exuberant-ctags libusb-1.0-0-dev ninja-build gcc python3 lsb-release bsdmainutils
sudo apt-get install binutils-avr gcc-avr avr-libc
sudo apt-get install binutils-arm-none-eabi gcc-arm-none-eabi libnewlib-arm-none-eabi dfu-util
sudo apt-get install ruby ruby-dev screen
sudo gem install serialport
```
