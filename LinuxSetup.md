Linux is the ideal build environment.
And the easiest way to install all the necessary dependencies is to use Docker.

### Docker

Most Linux distributions have a `docker` package available.
You won't have to worry about having the incorrect package versions by using docker as the Dockerfiles are supported by the developers.

- Install `git`
- Install [Docker](../../tree/master/Dockerfiles)

And you should be all ready to start building and testing firmware.

### Arch Linux

All packages are available in the official Arch repositories (AUR not needed).

In general, install the following packages

    pacman -S --needed git cmake ninja python libusb ctags gcc lsb-release

If you want to build for Teensy 1, Teensy 2, or other AVR based chip, install the following

    pacman -S --needed avr-binutils avr-gcc avr-libc

If you want to build for Teensy 3, the Infinity Keyboard, or another ARM based chip, install the following

    pacman -S --needed arm-none-eabi-binutils arm-none-eabi-gcc arm-none-eabi-newlib dfu-util

If you want to build the bootloader, install the following

    pacman -S --needed ruby
    gem install serialport

If you want to debug,

    sudo pacman -S --needed screen
    cp 98-kiibohd.rules /etc/udev/rules.d
    udevadm control --reload-rules

If you don't know what to install, then install everything above. It won't hurt! :smiley:

### Ubuntu

If you are on Ubuntu 12.04 LTS please make sure you have all the updates. If you are on a pre 12.04 OS please consider upgrading as the older kernel has an issue with the serial console.

Open up a terminal and run the following commands (you can copy/paste if you want). Note: You will be asked for your password - it is needed to get administrator privileges to install software. Also, you will not see anything as you type your password, it is normal, they hide the letters for security :)

In general, install the following packages

    sudo apt-get install git cmake exuberant-ctags libusb-1.0-0-dev ninja-build gcc python3 lsb-release bsdmainutils

If you want to build for Teensy 1, Teensy 2, or other AVR based chip, install the following

    sudo apt-get install binutils-avr gcc-avr avr-libc

If you want to build for Teensy 3, the Infinity Keyboard, or another ARM based chip, install the following

    sudo apt-get install binutils-arm-none-eabi gcc-arm-none-eabi libnewlib-arm-none-eabi dfu-util

If you want to build the bootloader, install the following

    sudo apt-get install ruby ruby-dev
    sudo gem install serialport

If you want to debug, install

    sudo apt-get install screen

If you don't know what to install, then install everything above. It won't hurt! :D

### Other OS

If you do not see your distribution listed then you can still build as long as you can find the packages to install. These depend a bit on which targets you are trying to build, but the general ones are:

- cmake (2.8 and higher)
- git
- ctags (recommended, not required)
- python3
- libusb1.0 (and -devel)
- make (or ninja)
- gcc (necessary for host-side KLL testing)

AVR Specific (Teensy 1.0/++,2.0/++) (try to use something recent, suggested
versions below)

- avr-gcc (~4.8.0)
- avr-binutils (~2.23.2)
- avr-libc (~1.8.0)

ARM Specific (Teensy 3.0/3.1, Infinity Keyboard, McHCK)

- arm-none-eabi-gcc
- arm-none-eabi-binutils
- arm-none-eabi-newlib

### What's next

Please see [[Configuration|Configuration]] to setup your keyboard.
