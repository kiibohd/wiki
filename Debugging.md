The kiibohd firmware provides a virtual console that can be used to send commands to the keyboard (reboot to bootloader, change layers, etc) and to see output (useful for debugging your matrix, etc).

## Connecting

<!-- tabs:start -->

#### ** Linux **

I generally use screen, although minicom or other serial viewers will probably work.

```
$ screen /dev/ttyACM0
# (Might be ACM1, ACM2, etc.)
```

?> Note: You will need sudo/root priviledges if you haven't
installed the `98-kiibohd.rules` file to `/etc/udev/rules.d`.

#### ** Mac **

I recommend screen (can be installed via Macports).

```bash
$ screen /dev/tty.<usb something>
```

Note: Screen can be installed with macports or homebrew. See [[Mac Setup|Mac Setup]].

#### ** Windows **

**Windows 7, 8 Only**

Make sure the [Teensy Virtual Serial Port driver](http://pjrc.com/teensy/serial_install.exe) is installed.
Windows 10+ has a driver built-in.

[putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/) works well when using DTR/DSR or RTS/CTS flow control.
KiTTY has auto-reconnect feature so you don't have to reopen the window every refresh. Just don't type anything into a terminal while the port is inactive (read: controller is rebooting or frozen)

| Setting         | Value                                |
| --------------- | ------------------------------------ |
| Connection type | Serial                               |
| Serial line     | Your COM port, e.g. COM3             |
| Speed           | doesn't matter, it's auto-negotiated |

Under `Category->Connections->Serial`: `Flow control: DTR/DSR`.

If stuff is hard to read (you have a dumb colour scheme):
`Category->Window->Colours->Use system color`. That seems to make text at
least readable

<!-- tabs:end -->

To exit the screen program you can use `Ctrl + a`, followed by `k` and confirming with `y`.

## Commands

Once in serial console type `help` and press enter to get a list of useful commands.
Below is a listing of the resulting commands.

```
General Commands
 clear        Clear the screen.
 cliDebug     Enables/Disables hex output of the most recent cli input.
 help         You're looking at it :P
 led          Enables/Disables indicator LED. Try a couple times just in case the LED is in an odd state.
                Warning: May adversely affect some modules...
 reload       Signals microcontroller to reflash/reload.
 reset        Resets the terminal back to initial settings.
 restart      Sends a software restart, should be similar to powering on the device.
 version      Version information about this firmware.

USB Module Commands
 kbdProtocol  Keyboard Protocol Mode: 0 - Boot, 1 - OS/NKRO Mode
 outputDebug  Toggle Output Debug mode.
 readLEDs     Read LED byte:
                1 NumLck, 2 CapsLck, 4 ScrlLck, 16 Kana, etc.
 sendKeys     Send the prepared list of USB codes and modifier byte.
 setKeys      Prepare a space separated list of USB codes (decimal). Waits until sendKeys.
 setMod       Set the modfier byte:
                1 LCtrl, 2 LShft, 4 LAlt, 8 LGUI, 16 RCtrl, 32 RShft, 64 RAlt, 128 RGUI

Macro Module Commands
 capList      Prints an indexed list of all non USB keycode capabilities.
 capSelect    Triggers the specified capabilities. First two args are state and stateType.
                K11 Keyboard Capability 0x0B
 keyHold      Send key-hold events to the macro module. Duplicates have undefined behaviour.
                S10 Scancode 0x0A
 keyPress     Send key-press events to the macro module. Duplicates have undefined behaviour.
                S10 Scancode 0x0A
 keyRelease   Send key-release event to macro module. Duplicates have undefined behaviour.
                S10 Scancode 0x0A
 layerDebug   Layer debug mode. Shows layer stack and any changes.
 layerList    List available layers.
 layerState   Modify specified indexed layer state <layer> <state byte>.
                L2 Indexed Layer 0x02
                0 Off, 1 Shift, 2 Latch, 4 Lock States
 macroDebug   Disables/Enables sending USB keycodes to the Output Module and prints U/K codes.
 macroList    List the defined trigger and result macros.
 macroProc    Pause/Resume macro processing.
 macroShow    Show the macro corresponding to the given index.
                T16 Indexed Trigger Macro 0x10, R12 Indexed Result Macro 0x0C
 macroStep    Do N macro processing steps. Defaults to 1.

Scan Module Commands
 echo         Example command, echos the arguments.

Matrix Module Commands
 matrixDebug  Enables matrix debug mode, prints out each scan code.
                If argument T is given, prints out each scan code state transition.
 matrixState  Prints out the current scan table N times.
                 O - Off, P - Press, H - Hold, R - Release, I - Invalid
```
