There are two main package managers for Mac command line programs - ports, and homebrew. Depending on what you have done you may already have one installed and can simply follow that section. If you have neither then I advise you use [Homebrew](https://brew.sh/).

### General Requirements

- Install [Xcode](https://itunes.apple.com/us/app/xcode/id497799835).
- Install the [Xcode command line tools](https://developer.apple.com/downloads/index.action).
- Install [git](http://git-scm.com/downloads), or `brew install git`.
- Install [Python 3](https://www.python.org/downloads/) (NOT 2), or `brew install python3`.
- Install the [ARM Embedded Toolchain](https://launchpad.net/gcc-arm-embedded), or follow instructions below.

- Accept the Xcode license by opening it, or running `xcodebuild -license`.
- Open a terminal for the following steps. Choose either the macports or homebrew section below - not both.

**OR**

- Install [Docker](../../tree/master/Dockerfiles) and follow these instructions after cloning the controller git repository.

### Homebrew

Install homebrew - http://brew.sh/

In general, install the following packages

```bash
brew install cmake libusb ctags ninja
```

If you want to build for Teensy 1, Teensy 2, or other AVR based chip, install the following

```bash
brew tap osx-cross/homebrew-avr
brew update
brew install avr-binutils avr-gcc avr-libc
```

If you want to build for Teensy 3, the Infinity Keyboard, or another ARM based chip, install the following

```bash
brew tap PX4/homebrew-px4
brew update
brew install gcc-arm-none-eabi dfu-util
```

**or**

```bash
brew tap Caskroom/cask
brew update
brew install Caskroom/cask/gcc-arm-embedded dfu-util
```

### Macports (Not Recommended)

Install macports - https://guide.macports.org/#installing.xcode

Run `sudo port selfupdate` to update the list of port packages.

In general, install the following packages

```bash
sudo port install cmake libusb ninja
```

If you want to build for Teensy 1, Teensy 2, or other AVR based chip, install the following

```bash
sudo port install avr-binutils avr-gcc avr-libc
```

If you want to build for Teensy 3, the Infinity Keyboard, or another ARM based chip, install the following

```bash
sudo port install arm-none-eabi-binutils arm-none-eabi-gcc dfu-util
```

If you don't know what to install, then install everything above. It won't hurt! :D

### What's next

Please see [[Configuration|Configuration]] to setup your keyboard.
