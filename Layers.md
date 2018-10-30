For a complete reference, please read the kll spec pdf, downloadable [here](https://input.club/kll).

Version 0.3d is the current one.

This here is just a short, practical guide. These topics are the advanced features of the software.

**TODO and WIP..**

# Macros

Macros let you execute a combination of keys and are defined with + sign.

For example to have Ctrl-C, Alt-F5, Ctrl-Alt-Delete, on F1,F2,F3 (on 2nd layer) those lines are needed in that layer's kll file:

```
U'F1' : U"Ctrl" + U"C";
U'F2' : U"Alt" + U"F5";
U'F3' : U"Ctrl" + U"Alt" + U"Delete";
```

# Sequences

Sequences let you execute key presses one after another.

So for example write a word 'Cool', or 'download' or even a password.

```
U"F1" : 'Cool';
U"F2" : 'download';
```

Or execute your frequently used key combination.
You can also mix uses of sequences and macros at once.

```
U"F3" : 'make', U"Enter";
U"F4" : U"F2", U"Home", U"_", U"Enter";
```

so F3 will now type make and press Enter.

Sequences (and Macros too) can also work as **triggers**.

E.g. a sequence of Ctrl press and then Alt, could do something, like e.g. change to layer 2.

```
U"Ctrl", U"Alt" : layerLock(1);
```

# Layers

As we know the base layer is defined in defaultMap.kll.

Let's have a new layer now.
We need a key binding that will let us use the new 2nd layer.
To add it, put 2 lines in defaultMap.kll, for example:

```
S0xF1 : U"Function1"
U"Function1" : layerLock(1);
```

I'm assuming that scan code 0xF1 will be the key for this.

To have a 2nd layer we need a new file, let's name it layer2.kll.
There can be many such layers, and they are named PartialMaps.
We need to include them in setup, if you use a bash file search the line with PartialMaps and use our new file layer2.kll, so finally:

```
PartialMaps[1]="layer2"
```

If you use a define for CMake or edit CMakeLists.txt search for PartialMaps parameter.

You can have a lot of layers this way. But the number of "Function" keys is limited to 16.

So for example having a 3rd layer you would have a new file layer3.kll and define

```
PartialMaps[2]="layer3"
```

and then have a binding to

```
S0xF2 : U"Function2"
"Function2" : layerLock(2);
```

and so on.

Layer numbers start from 0. But 0 is the default layer from defaultMap.kll which is the fall back layer if a key is not redefined in any later file like layer2.kll.

There are other possible Function1 key **behaviours**:

- layerLock(1) - This will act as a on/off toggle. First press will turn on 2nd layer, next press will turn it off.
- layerShift(1) - Access the 2nd layer when this key is being held. If released, it goes back to default.
- layerLatch(1) - When pressed will enable 2nd layer for the next key. After that press it goes back to default.
- layerRotate(0) - This will cycle through all available layers (for only 2 it works just as layerLock). (0) goes to next layer, (1) to previous (i.e. this is not the layer number-1 as before).
- layerState(1,0) - E.g. this will set a state 0 (off) to layer 1 (2nd).

I should also mention that layers are **stacked**.
So, if you press layerLock(1) and then layerLock(2), you'll access keys from 3rd layer, and if not found then from 2nd, then if not found, from defaultMap. If you press layerLock(2), it will turn off 3rd layer (remove it from stack) and go back to 2nd layer, until you press layerLock(1).

# Capabilities

**TODO**

in defaultMap.kll

```
action1 => CustomAction_usbCode_capability( usbCode : 1 );  # Single 8-bit argument
```

use example, in another kll

```
U"A" : action1(0x04);
```
