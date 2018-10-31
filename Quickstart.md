# Download the configurator

Available at https://github.com/kiibohd/configurator/releases/latest.

<!-- tabs:start -->

#### ** Windows **

Download kiibohd-configurator-XXXXX-win.exe

#### ** Mac **

- Download kiibohd-configurator-XXXXX-mac.dmg
- Install [dfu-util](http://dfu-util.sourceforge.net/releases/) using [homebrew](https://brew.sh/) - `brew install dfu-util`

#### ** Debian, Ubuntu, Mint **

- Download kiibohd-configurator-XXXXX-linux-YYYY.deb
- `sudo apt-get install dfu-util`

#### ** Fedora **

- Download kiibohd-configurator-XXXXX.tar.gz
- `sudo dnf install dfu-util`

#### ** Arch **

- Download kiibohd-configurator-XXXXX.tar.gz
- `pacman -S dfu-util`

#### ** Other Linux **

- Download kiibohd-configurator-XXXXX.tar.gz
- Using your system package manager install [dfu-util](http://dfu-util.sourceforge.net/releases/)

<!-- tabs:end -->

# Choose your device

![configurator](./images/configurator-home.png "Configurator")

## Official Input Club Keyboards

- [Infinity 60%](https://input.club/devices/infinity-keyboard/)
- [Infinity 60% LED](https://input.club/devices/infinity-keyboard/)
- [Infinity Ergodox](https://input.club/devices/infinity-ergodox/)
- [K-Type](https://input.club/k-type/)
- [WhiteFox](https://input.club/whitefox/)

## Other Keyboards

- Gemini Dusk
- Gemini Dawn

3rd party keyboards are not currently supported in the configurator.
For manually porting to new keyboards see the [Development](Development.md) section.

# Configure your Layout

Keys can be reassigned by clicking a switch and then clicking an action below. For more information see the [Customization](Customization.md) setction.

![keymap](./images/configurator-keymap.png "Configurator Keymap")

# Applying your changes

Press the lightning bolt icon at the top right of the toolbar.

![compile](./images/configurator-compile.png "Compile Button")

Once the download is complete press the flash button

### Entering Flash Mode.

1.  Flip your Keyboard over.
2.  With the keys down you should see a small hole on the left side in the middle of the board.
3.  While the keyboard is plugged in, use a paperclip or other small object to press the button inside the case.

- TIP: you can also configure a key combination to enter flash mode. On the default layout it's Fn-ESC.

<!-- tabs:start -->

## ** WhiteFox / Nightfox **

#### Video

[![whitefox-flash](https://img.youtube.com/vi/okFwGmpq70Y/0.jpg)](https://www.youtube.com/watch?v=okFwGmpq70Y "WhiteFox Flashing Button Demonstration")

## ** K-Type **

#### Video

[![ktype-flash](https://img.youtube.com/vi/i5wFVnEJcok/0.jpg)](https://www.youtube.com/watch?v=i5wFVnEJcok "WhiteFox Flashing Button Demonstration")

<!-- tabs:end -->

#### Failsafe mode

In case the keyboard cannot load the flashed firmware it will go into failsafe mode. In this state the keyboard is unresponsive, but can still enter flash mode:

1. Unplug an replug the USB cable
2. Press the flash button (as described above) twice in a row

### Flashing

Once in flash mode, the red (no keyboard is in flash mode) text should dissapear.
You can then press the purple flash button.

![flash](./images/configurator-flash.png "Compile Button")

#### Exiting Flash Mode

The keyboard exists flash mode automatically after a successful flash.

If you do not wish to change the firmware you may press ESC or unplug the keyboard to exit flash mode manually.

# Done

Enjoy your new layout :smiley:. For more advanced features and configuration please see the rest of this wiki.
