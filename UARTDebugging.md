If there are more serious issues with the firmware, or you're trying to debug USB related issues (which prevents you from looking at the USB Virtual Serial Port). Otherwise, just use the [[Virtual Serial Port|Debugging]].

However, to use the external debugging you need some additional tools. And perhaps some minor soldering.

# Tools

Here's a list of tools needed, with a list of possible options.

- Second computer (might be optional)
- USB to UART adapter
  - https://www.sparkfun.com/products/12942
  - http://www.amazon.com/Plugable-Adapter-Prolific-PL2303HX-Chipset/dp/B00425S1H8/ + http://www.amazon.com/Ultra-Compact-RS232-Converter-Female/dp/B00OPTOKI0/
  - http://www.amazon.com/Blue3D-Ft232rl-Serial-Adapter-Arduino/dp/B012YUANZK/
- Breakout Cable
  - https://www.sparkfun.com/products/9556

One additional benefit of getting a Bus Pirate over the other options is that you'll now have a tool capable of flashing the bootloader! The other options can be a bit easier to setup or you may have parts like them just sitting around.

# Hardware Setup

You'll need to connect the USB to UART adapter. This will require locating 4 pins on the PCB.

- +5V
- Vss (otherwise known as GND)
- Tx (last Tx, i.e. Tx2, keyboard dependent)
- Rx (last Rx, i.e. Rx2, keyboard dependent)

Next you'll need to connect everything together.

1. Attach breakout cable to USB to UART adapter
2. Find the equivalent pins on the UART adapter

- +5V is often called Vcc (make sure it's 5V)
- Vss is often called Gnd
- Tx and Rx need to be swapped. This is because it's from the perspective of that device. Don't worry if you mix this up, you can just swap later.

3. Either solder header pins or wires to the keyboard pcb for the required pins
4. Connect the breakout cable to the keyboard pcb

- NOTE: Only connect the +5V _IF_ you are using a USB to Serial + Serial to UART adapter. The Serial to UART adapter needs to be powered which is why it's necessary. Otherwise you may run into issues rebooting the keyboard even after unplugging USB.

5. Plug in keyboard USB connector to computer
6. Plug in USB to UART adapter USB to computer (possibly second computer depending on what you're testing)

Once you're sure you've cable everything up correctly, it shouldn't matter which order you do the steps.

**Don't mix up +5V and Gnd/Vss**

# Firmware Setup

_This part is a bit more involved_

There are a few ways to configure CMake, but for simplicity I'm going to use the [Keyboard Build Scripts](https://github.com/kiibohd/controller/tree/master/Keyboards) as a base.

I'll be using [ergodox.bash](https://github.com/kiibohd/controller/blob/master/Keyboards/ergodox.bash) as the example. But this will apply to all other keyboards as well.

## CMake Configuration

Only one variable you need to change in `ergodox.bash`.

```bash
OutputModule="USBxUART"
```

For convenience you can also add `remote_reload` to your DefaultMap, this enables jumping to the bootloader from the cli. Very convenient for debugging, though a security hazard to leave on by default.

## USB Debug Modes

This part is optional, but highly recommended if you're trying to debug OS/USB related issues. If you're trying to gather data for a GitHub Issue/Support Request, definitely do this.

[usb_dev.c](https://github.com/kiibohd/controller/blob/master/Output/pjrcUSB/arm/usb_dev.c)

There are two different commented out defines in this file. One of them can be uncommented without any issues, the other, you have to be careful (i.e. don't do it unless you're _really_ digging deep into the USB code and don't mind possible firmware race condition crashes).

### Safe to Uncomment

```C
//#define UART_DEBUG_UNKNOWN 1
```

to

```C
#define UART_DEBUG_UNKNOWN 1
```

### Less Safe to Uncomment

```C
//#define UART_DEBUG 1
```

to

```C
#define UART_DEBUG 1
```

## Building Firmware

No you should be able to run the `ergodox.bash` script and the firmware will be configured with the CLI mirrored on both the USB virtual serial port and Serial Port/UART (there's also another UART only module, but that's for super serious issues and chip bringup).

When the serial port is muxed with the UART it will be noticeably slower even when accessing through USB. This, however, should not affect performance of any other keyboard functions. Really, it's just because the UART is slow, running at 115200 baud.

# CLI Setup

As usual each OS will have different instructions.

Unless you have setup differently the default serial settings are (both the keyboard and bus pirate):

- 115200 baud
- 8 data bits
- No parity
- 1 stop bit

<!-- tabs:start -->

#### ** Linux **

I generally like to use `screen` for serial ports on Linux, and it's the easiest to configure.
What you are looking for is something like `/dev/ttyUSB0`.

```bash
screen /dev/ttyUSB0 115200 8N1
```

?> Note: You will need sudo/root priviledges if you haven't
installed the `98-kiibohd.rules` file to `/etc/udev/rules.d`.

To exit, just kill the screen session. Ctrl+a, then k, then y.

#### ** Mac **

Screen is also available on Mac OS X through services such as Macports and Brew. I believe you'll be looking for something like `/dev/tty.<usb something>`. Afaik, this is not very predictable.

```bash
screen /dev/tty.usbsomething 115200 8N1
```

To exit, just kill the screen session. Ctrl+a, then k, then y.

#### ** Windows **

Sadly `screen` doesn't work well with serial ports under Windows, so I recommend [putty](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Check which COM port the virtual serial port has been assigned to: `Device Manager->Ports (COM & LPT)->Teensy USB Serial`. In brackets it will say which COM port (e.g. COM3)

putty works well when using DTR/DSR or RTS/CTS flow control.

| Setting         | Value                    |
| --------------- | ------------------------ |
| Connection type | Serial                   |
| Serial line     | Your COM port, e.g. COM3 |
| Speed           | 15200                    |

If stuff is hard to read (you have a dumb colour scheme):
`Category->Window->Colours->Use system color`.

That seems to make text at least readable.

<!-- tabs:end -->

## Bus Pirate

The Bus Pirate requires a bit of extra setup (mostly due to all the extra functionality it has).
Each step below is follow by the command. Press enter after each command.

- Enable UART mode
  - m
- Set baud rate to 115200
  - 3
- 8 bit and no parity
  - Enter
- 1 Stop bit
  - Enter
- Receive polarity Idle 1
  - Enter
- Open drain (H=Hi-Z, L=GND)
  - Enter
- Set to transparent bridge
  - (1)
- Confirm yes
  - y

Now your serial port session will be displaying the Kiibohd CLI as long as everything has worked so far, and the firmware isn't hung. A quick test is to press the flash button on the back of the pcb, the bootloader will display a message (NOTE: This doesn't work on the Infinity 60%).
