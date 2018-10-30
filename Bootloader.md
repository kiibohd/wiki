Some devices like the Teensy already come with their own bootloader. However, if you buy an individual chip for a pcb, then it most likely does not come with a bootloader, and must be flashed on by hand.

You'll need to make sure your environment is setup first. [Linux](https://github.com/kiibohd/controller/wiki/Linux-Setup) or [macOS](https://github.com/kiibohd/controller/wiki/Mac-Setup) is recommended over [Windows](https://github.com/kiibohd/controller/wiki/Windows-Setup) (much easier).

Linux is always tested first, so when in doubt try loading up a VM with Ubuntu or Arch Linux.

While not recommended unless you have Arch Linux, there are also full manufacturing instructions, which details cabling and adapter setups: https://github.com/kiibohd/manufacturing/wiki

## Building Bootloader

```bash
cd Bootloader/Builds
# Select your MCU
./mk20dx256vlh7.bash
cd *mk20dx256vlh7*
# kiibohd_bootloader.bin
```

## Preparing Bus Pirate

The loading script requires a few additional ruby modules to be installed before it will work correctly.

```bash
gem install serialport libusb
```

Clone loading script.

```bash
cd Bootloader/Scripts
git clone https://github.com/kiibohd/programmer
```

## Loading Bootloader

It's recommended to use an SWD-type flasher like a Bus Pirate. There is a convenience script for loading the firmware once the system is setup.

```bash
cd Bootloader/Scripts
./swdLoad.bash <path to .bin> 0
./swdLoad.bash ../Builds/*mk20dx256vlh7*/kiibohd_bootloader.bin 0
```

The above script requires Ruby, Ruby serial port module, git, and a `/dev/buspirate` udev rule. If you don't want to create a udev rule, a symlink is also ok.

Most errors indicate problems with either cabling setup or missing ruby modules. Some chips may also become locked. Locked chips can be difficult to unlock without a JLink adapter. https://github.com/kiibohd/manufacturing

Additional Notes:

- https://github.com/mchck/mchck/wiki/Getting-Started (See Bus-Pirate section)
- https://wiki.archlinux.org/index.php/Bus_pirate

## Cygwin - Bus Pirate

As usual, Cygwin requires quite a bit more setup than Linux (or Mac).
First, install the following Cygwin packages.

- gcc-core
- gcc-g++
- ruby
- ruby-devel
- rubygems
- rubygems
- gmp
- libgmp-devel
- libusb1.0
- libusb1.0-devel
- libffi-devel
- make
- autotools

Next, install the Ruby gems.

```bash
gem install serialport libusb
```

Now, plug in the Bus Pirate.
Go to your device manager and locate the COMx port for the Bus Pirate and set the following.

```
Bits per second:   115200
Data bits:         8
Parity:            None
Stop bits:         1
Flow control:      None
```

Not the COMx number. For example, COM6 correlates to /dev/ttyS5 in Cygwin.

Clone the programmer [git repository](https://github.com/kiibohd/programmer).

Finally, ready to flash. Make sure to replace ttyS5 with your serial port.

```bash
git clone https://github.com/kiibohd/programmer.git
ruby programmer/flash.rb name=buspirate:dev=<serial port> <bootloader binary> <address>
ruby programmer/flash.rb name=buspirate:dev=/dev/ttyS5 kiibohd_bootloader.bin 0
```
