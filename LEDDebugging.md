Sometimes when soldering LEDs they some of them don't work.
There can be a few causes of this.

1. LED soldered in the wrong direction (polarity)
2. Bad LED
3. Damaged trace on the pcb (disconnect/short)
4. Stray solder causing a short

# Debugging LEDs

Using the internal CLI it is possible to debug which LED(s) are not working.
This is particularily important when checking whether the LEDs were soldered in the correct direction.

1. Access CLI [Virtual Serial Port](Debugging.md)
2. Make sure any animations are disabled.
`aniStack` shows the active animations (this may vary depending on what has been flashed to your keyboard)
`aniDel 0` removes the animation at the top of the stack (only call `aniDel 0` the same number of times as your stack otherwise some version of firmware may crash and you will have to do this step again).
```
: aniStack
INFO - Stack Size: 2
 index(0) pos(1) loops(0) framedelay(0) frameoption(0) ffunc(0) pfunc(1)
 index(0) pos(1) loops(0) framedelay(0) frameoption(0) ffunc(0) pfunc(1)
: aniDel 0

: aniDel 0

: aniStack
INFO - Stack Size: 0
```
3. Enable pixel test 'roll' mode
```
pixelTest r
```
4. If necessary slow the frame speed (1-255, higher number translates to a larger divider, slowing the frames down)
```
ledFPS 100
```
5. Check to make sure each LED turns on in order, starting from the top left going to the right, then wrapping to the next line.
6. If any LEDs do not turn on or turn on unexpectedly, it is soldered in the wrong direction
7. If you would like to stop this test sequence you can either enter the `restart` command or unplug and plug back in your keyboard.

## Example - WhiteFox

This WhiteFox has 1 LED that has been soldered backwards.
![WhiteFox LEDs]()
