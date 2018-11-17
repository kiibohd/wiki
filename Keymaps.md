## Keymap Configuration

A keyboard layout is built up of 3 different kinds of keymaps in total.
The BaseMap, DefaultMap and PartialMaps.

For each type of keymap, it is possible to combine multiple .kll files together to create new ones using
the compiler. The order of the files matter, as the right-most file will overwrite any setting in the
previous files.

BaseMap defines what the keyboard can do. This includes specific capabilities of the keyboard (such as USB),
the mapping of Scan Codes to USB Codes and any specific configurations for the keyboard.
In general, the BaseMap rarely needs to be changed. Usually only when adding a new keyboard to the firmware
does the Basemap need any modification.
The BaseMap is what both DefaultMap and PartialMaps are based upon. This allows for a common reference
when defining custom keymappings.

The DefaultMap is the normal state of the keyboard, i.e. your default layer.
Using the BaseMap as a base, the DefaultMap is a modification of the BaseMap to what the keyboard should do.
Since the DefaultMap uses USB Code to USB Code translations, this means that keymaps used for one keyboard
will work with another keyboard.
For example, I use Colemak, so this means I only have to define Colemak once for every keyboard that supports
the kiibohd firmware. This is possible because every BaseMap defines the keyboard as a US ANSI like keyboard
layout.
The DefaultMap can also be thought of as Layer 0.

PartialMaps are optional keymaps that can be "stacked" on top of the DefaultMap.
They can be dynamically swapped out using the layer control capabilities.
A unique aspect of KLL layers is that it's a true stack of layers.
When a layer is activated, only the keys that are specified by the layer will change.
This means, if you define a layer that only sets `CapsLock -> LCtrl` and `LCtrl->Capslock` only those keys
will change when you active the layer. All the other keys will use the layer that is "underneath" to
lookup the keypress (usually the DefaultMap).

You can set the max number of layers by changing the `stateWordSize` define in one of your kll files.
By default it is set to 8 in Macro/PartialMap/capabilities.kll. This means you can have up to 256 layers
total (this includes the DefaultMap).
You can increase this number to either 16 or 32 (this will use more Flash and RAM btw) which will give you
2^16 and 2^32 possible layers respectively (65 535 and 4 294 967 295).

```cmake
###
# Keymap Configuration (do not include the .kll extension)
#

#| Do not include the .kll extension
#| * BaseMap maps the native keyboard scan codes to USB Codes so the layout is compatible with all other layouts
#| * DefaultMap allows the default keymap to be modified from the BaseMap
#| * PartialMaps is a set of dynamically set layers (there is no limit, but too many may use up too much RAM...)
#| BaseMap generally does not need to be changed from "defaultMap"
#|
#| Syntax:
#|  myMap
#|    * defines a single .kll layout file, double-quotes are needed to distinguish between layers
#|  "myMap specialLayer"
#|    * defines myMap to be the main layout, then replace specialLayers on top of it
#|
#| - Only for PartialMaps -
#|  "myMap specialLayer" "myMap colemak" dvorak
#|    * As before, but also generates a second layer at index 2 and third at index 3
#|
#| NOTE:  Remember to add key(s) to enable each Partial Layer
#| NOTE2: Layers are always based up the BaseMap (which should be an ANSI-like mapping)
#| NOTE3: Compiler looks in kll/layouts and the build directory for layout files (precedence on build directory)

##| Set the base keyboard .kll map, defaults to "defaultMap" if not found
##| Looks in Scan/<Module Name> for the available BaseMaps
set(     BaseMap "defaultMap"
        CACHE STRING "KLL BaseMap/Scancode Keymapping" )

##| Layer additonal .kll maps on the BaseMap, layers are in order from 1st to nth
##| Can be set to ""
set(  DefaultMap "md1Overlay stdFuncMap"
        CACHE STRING "KLL DefaultMap" )

##| ParitalMaps available on top of the BaseMap. See above for syntax on specifying multiple layers vs. layering
##| Can be set to ""
set( PartialMaps "hhkbpro2"
        CACHE STRING "KLL PartialMaps/Layer Definitions" )
```

