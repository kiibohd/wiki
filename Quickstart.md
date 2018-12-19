# Download the configurator

<!-- tabs:start -->

#### ** Windows **

v0.6.0 **pre-release**: [Download Windows installer](https://github.com/kiibohd/configurator/releases/download/v0.6.0-alpha/kiibohd-configurator-0.6.0-alpha-win.msi)

 - Kira support

?> The pre-release contains support for Kira, but is not yet feature complete.
Please check back often for future updates.

<!--
---
Old Versions:

*v0.4.1:* [Download](https://github.com/kiibohd/configurator/releases/download/v0.4.1/kiibohd-configurator-0.4.1-win.exe)

 - K-Type animation support

 - Requires [dfu-util](http://dfu-util.sourceforge.net/releases/)
-->

#### ** Mac **

v0.6.0 **pre-release**: [Download OSX installer](https://github.com/kiibohd/configurator/releases/download/v0.6.0-alpha/kiibohd-configurator-0.6.0-alpha-mac.dmg)

 - Kira support

?> The pre-release contains support for Kira, but is not yet feature complete.
Please check back often for future updates.

<!--
---
Old Versions:

v0.4.1: [Download](https://github.com/kiibohd/configurator/releases/download/v0.4.1/kiibohd-configurator-0.4.1-mac.dmg)

 - K-Type animation support

 - Requires dfu-util (available using [homebrew](https://brew.sh/), `brew install dfu-util`)
-->

#### ** Debian, Ubuntu, Mint **

v0.4.1:
 - [Download tar](https://github.com/kiibohd/configurator/releases/download/v0.4.1/kiibohd-configurator-0.4.1.tar.gz)
 - `sudo apt-get install dfu-util`

#### ** Fedora **

v0.4.1:
 - [Download tar](https://github.com/kiibohd/configurator/releases/download/v0.4.1/kiibohd-configurator-0.4.1.tar.gz)
 - `sudo dnf install dfu-util`

#### ** Arch **

v0.4.1:
 - [Download tar](https://github.com/kiibohd/configurator/releases/download/v0.4.1/kiibohd-configurator-0.4.1.tar.gz)
 - `pacman -S dfu-util`

#### ** Other Linux **

v0.4.1:
 - [Download tar](https://github.com/kiibohd/configurator/releases/download/v0.4.1/kiibohd-configurator-0.4.1.tar.gz)
 - Install [dfu-util](http://dfu-util.sourceforge.net) using your systems package manager

<!-- tabs:end -->

Other releases are available on github: [Browse all](https://github.com/kiibohd/configurator/releases)

# Choose your device

![configurator](./images/configurator-home.png "Configurator")

# Configure your Layout

Keys can be reassigned by clicking a switch and then clicking an action below. For more information see the [Keys](Configurator/Keys.md) page.

![keymap](./images/configurator-keymap.png "Configurator Keymap")

# Applying your changes

Press the lightning bolt icon at the top right of the toolbar.

![compile](./images/configurator-compile.png "Compile Button")

Once the download is complete you should see a green success message

![compile-success](./images/configurator-compile-success.png "Compile Success Toast")

### Entering Flash Mode.

1.  Flip your Keyboard over.
2.  With the keys down you should see a small hole on the the buttom of the board.
3.  While the keyboard is plugged in, use a paperclip or other small object to press the button inside the case.

- TIP: you can also configure a key combination to enter flash mode.

<!-- tabs:start -->

## ** Kira **

![flash-switch](../images/reset%20button.jpg 'Flash Button')

## ** WhiteFox / Nightfox **

#### Video

[![whitefox-flash](https://img.youtube.com/vi/okFwGmpq70Y/0.jpg)](https://www.youtube.com/watch?v=okFwGmpq70Y "WhiteFox Flashing Button Demonstration")

## ** K-Type **

#### Video

[![ktype-flash](https://img.youtube.com/vi/i5wFVnEJcok/0.jpg)](https://www.youtube.com/watch?v=i5wFVnEJcok "WhiteFox Flashing Button Demonstration")

<!-- tabs:end -->

#### Failsafe mode

In case the keyboard cannot load the flashed firmware it will go into failsafe mode. In this state the keyboard is unresponsive, but can still enter flash mode.

### Flashing

Once in flash mode, the red (no keyboard is in flash mode) text should dissapear.
You can then press the purple flash button.

![flash](./images/configurator-flash.png "Compile Button")

#### Exiting Flash Mode

The keyboard exists flash mode automatically after a successful flash.

If you do not wish to change the firmware you may press <kbd>ESC</kbd> or unplug the keyboard to exit flash mode manually.

# Done

Enjoy your new layout. For more advanced features and configuration please see the [Configurator](Configurator.md#customization) section of this wiki.
