## Selecting Microcontroller

This is where you select the chip you want to compile for. The build system
will automatically select the compiler needed to compile for your chip.

Open up CMakeLists.txt in your favourite text editor. You are looking for:

```cmake
###
# Chip Selection
#

#| You _MUST_ set this to match the microcontroller you are trying to compile for
#| You _MUST_ clean the build directory if you change this value
#|
set( CHIP
#	"atmega32u4"       # Teensy   2.0 (avr)
#	"at90usb1286"      # Teensy++ 2.0 (avr)
#	"mk20dx128"        # Teensy   3.0 (arm)
    "mk20dx128vlf5"    # McHCK    mk20dx128vlf5
#	"mk20dx256"        # Teensy   3.1 (arm)
    CACHE STRING "Microcontroller Chip" )
```

Just uncomment the chip you want, and comment out the old one. (Move the # from one line to another)

> NOTE: If you change this option, you will _need_ to delete the build
> directory that is created in the Building sections below.

