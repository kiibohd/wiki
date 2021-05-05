# Install the drivers

<!-- tabs:start -->

#### ** Windows **

![drivers](./images/drivers.png ':size=400%')

 - Unplug your keyboard

 - Download and run:

[Windows Driver Installer](https://github.com/kiibohd/kiidrv/releases/download/v1.5.3-kiidrv/KiibohdDrivers.msi) (Necessary to flash properly.)

 - Plug back in your keyboard

#### ** Mac **

*Nothing to do.*

#### ** Debian, Ubuntu, Mint **

Run the following command in a terminal:

 - `sudo apt-get install dfu-util`

Download [https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules](https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules)

```
sudo cp 98-kiibohd.rules /etc/udev/rules.d
sudo udevadm control --reload-rules
sudo udevadm trigger
```

#### ** Fedora **

Run the following command in a terminal:

 - `sudo dnf install dfu-util`

Download [https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules](https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules)

```
sudo cp 98-kiibohd.rules /etc/udev/rules.d
sudo udevadm control --reload-rules
sudo udevadm trigger
```

#### ** Arch **

Run the following command in a terminal:

 - `sudo pacman -S dfu-util`

Download [https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules](https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules)

```
sudo cp 98-kiibohd.rules /etc/udev/rules.d
sudo udevadm control --reload-rules
sudo udevadm trigger
```

#### ** Other Linux **

- Install [dfu-util](http://dfu-util.sourceforge.net) using your systems package manager

- Download [https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules](https://raw.githubusercontent.com/kiibohd/controller/master/98-kiibohd.rules)

```
sudo cp 98-kiibohd.rules /etc/udev/rules.d
sudo udevadm control --reload-rules
sudo udevadm trigger
```

<!-- tabs:end -->

# Download the IC Configurator

<!-- tabs:start -->

#### ** Windows **

![configurator-install](./images/Configurator/install.png)

v1.1.0 **NEW**: [Download Windows Configurator](https://github.com/kiibohd/configurator/releases/download/v1.1.0/kiibohd-configurator-1.1.0-win.exe)

 - Fixes backend URL to use standard HTTP ports (works better with aggressive firewalls)

#### ** Mac **

v1.1.0 **NEW**: [Download OSX App](https://github.com/kiibohd/configurator/releases/download/v1.1.0/kiibohd-configurator-1.1.0-mac.dmg)

 - Fixes backend URL to use standard HTTP ports (works better with aggressive firewalls)

#### ** Debian, Ubuntu, Mint **

v1.1.0 **NEW**: [https://github.com/kiibohd/configurator/releases/download/v1.1.0/kiibohd-configurator-1.1.0-linux-x86_64.AppImage)
 - `chmod +x kiibohd-configurator-1.1.0-linux-x86_64.AppImage`
 - `./kiibohd-configurator-1.1.0-linux-x86_64.AppImage`
 
#### ** Fedora **

v1.1.0 **NEW**: [Download AppImage](https://github.com/kiibohd/configurator/releases/download/v1.1.0/kiibohd-configurator-1.1.0-linux-x86_64.AppImage)
 - `chmod +x kiibohd-configurator-1.1.0-linux-x86_64.AppImage`
 - `./kiibohd-configurator-1.1.0-linux-x86_64.AppImage`
 
#### ** Arch **

v1.1.0 **NEW**:
 - [Download AppImage](https://github.com/kiibohd/configurator/releases/download/v1.1.0/kiibohd-configurator-1.1.0-linux-x86_64.AppImage)
 - `chmod +x kiibohd-configurator-1.1.0-linux-x86_64.AppImage`
 - `./kiibohd-configurator-1.1.0-linux-x86_64.AppImage`

#### ** Other Linux **

v1.1.0 **NEW**:
 - [Download tar](https://github.com/kiibohd/configurator/releases/download/v1.1.0/kiibohd-configurator-1.1.0-linux-x64.tar.gz)
 - Extract the file
 - Run `kiibohd-configurator`

<!-- tabs:end -->

*Other releases are available on github:* [Browse all](https://github.com/kiibohd/configurator/releases)

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

<!-- tabs:start -->

## ** Kira **

Pressing <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Esc</kbd> will enter flash mode.

Alternatively, flip your Kira over find the reset button hole. Press the button with a thin object to put the keyboard into flash mode. You can use this method if your layout does not have a flashing hotkey assigned, or the layout is unknown.

![flash-switch](./images/reset%20button.jpg 'Flash Button')

Once in flash mode the orange led should be lit.
![bootloader-led](https://cdn.discordapp.com/attachments/325093040500768779/536057903631695882/IMG_20190118_214221278.jpg)

## ** WhiteFox / Nightfox **

Pressing <kbd>Fn</kbd> + <kbd>Esc</kbd> will enter flash mode.

#### Fallback Method

[![whitefox-flash](https://img.youtube.com/vi/okFwGmpq70Y/0.jpg)](https://www.youtube.com/watch?v=okFwGmpq70Y "WhiteFox Flashing Button Demonstration")

1.  Flip your Keyboard over.
2.  With the keys down you should see a small hole on the the buttom of the board.
3.  While the keyboard is plugged in, use a paperclip or other small object to press the button inside the case.

## ** K-Type **

Pressing <kbd>Fn</kbd> + <kbd>Esc</kbd> will enter flash mode.

#### Fallback Method

[![ktype-flash](https://img.youtube.com/vi/i5wFVnEJcok/0.jpg)](https://www.youtube.com/watch?v=i5wFVnEJcok "WhiteFox Flashing Button Demonstration")

1.  Flip your Keyboard over.
2.  With the keys down you should see a small hole on the the buttom of the board.
3.  While the keyboard is plugged in, use a paperclip or other small object to press the button inside the case.

## ** Gemini Dusk/Dawn **

Pressing <kbd>Fn</kbd> + <kbd>Esc</kbd> will enter flash mode.

#### Fallback Method

[![ktype-flash](https://img.youtube.com/vi/i5wFVnEJcok/0.jpg)](https://www.youtube.com/watch?v=i5wFVnEJcok "WhiteFox Flashing Button Demonstration")

1.  Flip your Keyboard over.
2.  With the keys down you should see a small hole on the the far right middle edge.
3.  While the keyboard is plugged in, use a paperclip or other small object to press the button inside the case through this hole.

<!-- tabs:end -->

### Flashing

Once in flash mode, the red (no keyboard is in flash mode) text should disappear.
You can then press the purple flash button.

![flash](./images/configurator-flash.png "Compile Button")

#### Exiting Flash Mode

The keyboard exists flash mode automatically after a successful flash.

If you do not wish to change the firmware you may press <kbd>ESC</kbd> or unplug the keyboard to exit flash mode manually.

# Done

Enjoy your new layout. For more advanced features and configuration please see the [Configurator](Configurator.md#customization) section of this wiki.
