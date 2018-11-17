## Selecting Modules

> WARNING: Not all modules are compatible, and some modules may have
> dependencies on other modules.

This is where the options start getting interesting. The Kiibohd Controller
is designed around a set of 4 types of modules that correspond to different
functionality:

- Scan Module
- Macro Module
- Output Module
- Debug Module

The **Scan Module** is where the most interesting (or hardware) stuff happens. These modules
take in "keypress data".

- A converter Scan Module will interpret a protocol into key press/releases.
- A matrix Scan Module may inherit from the matrix module to scan keypress from a matrix.

This module just has to give press/release codes, but does have some callback control to other modules,
depending on the lifecycle for press/release codes (this can be very complicated depending on the protocol).
Each Scan Module has it's own default keymap/modifier map. (TODO recommend keymap changing in the Macro Module).

> Some scan modules have very specialized hardware requirements, each module directory should have at least a link to the needed parts and/or schematics (TODO!).

The **Macro Module** takes care of the mapping of the key press/release code into
an Output (USB) scan code. Any layering, macros, keypress
intelligence/reaction is done here.

The **Output Module** is the module dealing with output from the microcontroller.
Currently USB is the only output protocol. Different USB output
implementations are available, pjrc being the safest/least featureful one.
Debug capabilities may depend on the module selected.

The **Debug Module** enables various things like the Teensy LED on errors, debug
terminal output. (TODO get true UART working in avr, not just arm)

Open up CMakeLists.txt in your favourite text editor. Look for:

```cmake
###
# Project Modules
#

#| Note: This is the only section you probably want to modify
#| Each module is defined by it's own folder (e.g. Scan/Matrix represents the "Matrix" module)
#| All of the modules must be specified, as they generate the sources list of files to compile
#| Any modifications to this file will cause a complete rebuild of the project

#| Please look at the {Scan,Macro,Output,Debug} for information on the modules and how to create new ones

##| Deals with acquiring the keypress information and turning it into a key index
set(   ScanModule "Infinity_60"
    CACHE STRING "Scan Module" )

##| Provides the mapping functions for DefaultMap and handles any macro processing before sending to the OutputModule
set(  MacroModule "PartialMap"
    CACHE STRING "Macro Module" )

##| Sends the current list of usb key codes through USB HID
set( OutputModule "USB"
    CACHE STRING "Output Module" )

##| Debugging source to use, each module has it's own set of defines that it sets
set(  DebugModule "full"
    CACHE STRING "Debug Module" )
```

Look at each module individually for it's requirements. There is
chip/architecture dependency checking, but some permutations of modules may not
be tested/compile.

There are also CMake options for temporarily selecting modules. But it's
easier to just edit the file. e.g. `cmake -DScanModuleOverride=<module name>`.

