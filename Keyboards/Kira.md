![Kira](https://cdn.discordapp.com/attachments/394307335704543232/534901510283198474/Kira_Main_Image.png)


## Firmware Update

?> **We recommend all customers to update their keyboard for the latest fixes and features.**<br/><br/>
   You can either use the installer below, or use the [Configurator](Quickstart.md)

<!-- tabs:start -->

#### ** Windows **

- Unplug your keyboard

- Install the [Windows Drivers](https://github.com/kiibohd/kiidrv/releases/download/v1.5.3-kiidrv/KiibohdDrivers.msi) (Necessary to flash properly.)

- Plug back in your keyboard

- Run the [Firmware Updater](https://drive.google.com/uc?export=download&id=1UnkVE6B9xxdoVHARt57xvsdCjU7AtRHG) (**v0.5.4** *Feb 2019*)

- Enter flash mode by pressing <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Esc</kbd>,
  or by pressing the reset button on the bottom of the board

![reset-button](../images/reset%20button.jpg ':size=400%')

Once in flash mode the orange led should be lit.
![bootloader-led](https://cdn.discordapp.com/attachments/325093040500768779/536057903631695882/IMG_20190118_214221278.jpg ':size=400%')

*Old versions can be found: [here](https://drive.google.com/open?id=16xcBCLXziE_xtGMr_lXkA5gqLEUjYSKC)*

#### ** Mac **

- Run the [Firmware Updater](https://drive.google.com/uc?export=download&id=15Na8t_u4O8tTK1tLip_aVB-E1cuVaYYp) (**v0.5.4** *Feb 2019*)

- Enter flash mode by pressing <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Esc</kbd>,
  or by pressing the reset button on the bottom of the board

![reset-button](../images/reset%20button.jpg ':size=400%')

Once in flash mode the orange led should be lit.
![bootloader-led](https://cdn.discordapp.com/attachments/325093040500768779/536057903631695882/IMG_20190118_214221278.jpg ':size=400%')

*Old versions can be found: [here](https://drive.google.com/open?id=1DDGFGd22UdYjQ1fEp7B-vbYrheurR0Jw)*

#### ** Linux **

- Download the [Firmware Updater](https://drive.google.com/uc?export=download&id=1eF_wv0RrWu_BfKMfz3xQlysUZZs0zNwt) (**v0.5.4** *Feb 2019*)

- Extract the file

- Run `flash.sh`

- Enter flash mode by pressing <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Esc</kbd>,
  or by pressing the reset button on the bottom of the board

![reset-button](../images/reset%20button.jpg ':size=400%')

Once in flash mode the orange led should be lit.
![bootloader-led](https://cdn.discordapp.com/attachments/325093040500768779/536057903631695882/IMG_20190118_214221278.jpg ':size=400%')

*Old versions can be found: [here](https://drive.google.com/open?id=17VZ90xKdOjmmNJRICWlIezg9hnpcwzmw)*

<!-- tabs:end -->

#### Fixed Issues

The following issues are fixed with a firmware update:

- When entering flash mode using the keycombo, the ctrl/shift keys may stay pressed
- The orange fade-in animation may show two different shades
- When using the developer debug terminal leds may flicker

## Customizing

**Configurator now available!**

The [Quickstart guide](Quickstart.md) should help you configure your device

## Default Layout

![layout](../images/kira/layout.png "Kira Base Layout")

### Lighting Layer
The Animation layer is accessible with by holding <kbd>Right Alt</kbd> + <kbd>Right Control</kbd>.

![layer2-combo](../images/kira/layer2-combo.png "Kira Layer 2 Combo")
![layer1](../images/kira/layer2.png "Kira Layer 2")

| Key Combo | Action |
|-----------|--------|
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F1</kbd> | Change key colors |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F2</kbd> | Change underglow color |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F3</kbd> | Change key fade period |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F4</kbd> | Change underglow fade period |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F5</kbd> | Change lock led fade period |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F6</kbd> | Change layer highlight fade period |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F7</kbd> | Change animation |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>-</kbd> | **New firmware:** Decrease Brightness<br/>**Shipping firmware:** Increase Brightness |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>+</kbd> | **New firmware:** Increase Brightness<br/>**Shipping firmware:** Decrease Brightness |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>Backslash</kbd> | Toggle gamma correction (changes color representation) |

#### Fading

By default the keyboard will gradually "breath" in and out. The speed of this can be changed.

| Key Combo | Action |
|-----------|--------|
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F12</kbd> | Change key fade |
| <kbd>Right Alt</kbd> + <kbd>Right Control</kbd> + <kbd>F11</kbd> | Change underglow fade |

### Control Layer
The Control layer is accessible with by holding <kbd>Right Shift</kbd> + <kbd>Right Control</kbd>.

![layer1-combo](../images/kira/layer1-combo.png "Kira Layer 1 Combo")

![layer1](../images/kira/layer1.png "Kira Layer 2")

#### Media Keys

| Key Combo | Action |
|-----------|--------|
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Home</kbd>     | Volume Down |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>End</kbd>      | Volume Up |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>PgUp</kbd>     | Play / Pause |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>PgDn</kbd>     | Mute |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Num Lock</kbd> | Previous Track |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Numpad /</kbd> | Next Track |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Numbad *</kbd> | Rewind |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>Numbad -</kbd> | Fast Forward |

#### Save Lighting Settings

After saving your lighting settings they will automatically take effect when the keyboard is plugged in.

Saving currently works for
* Brightness
* Currently active animations
* Fade configuration

| Key Combo | Action |
|-----------|--------|
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>F12</kbd> | Save animation & brightness |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>F11</kbd> | Load saved animation & brightness |
| <kbd>Right Shift</kbd> + <kbd>Right Control</kbd> + <kbd>F10</kbd> | Load default animation & brightness |

## Changing the ring

![ring](../images/Kira%20Back%20Frame%20off.jpg "Kira With Ring Removed")

Easily remove the ring from the Kira by gently lifting from the back until it releases and then the front to remove it entirely.

To replace the ring, gently attach the front and lower the back until it snaps into place.

[hotswap](../Hotswap.md ':include')


## Default Animations

| Animation |
|-------|
| Miami Wave |
| Rainbow Wave |
| Pastel Rainbow |
| Kira Wave |
| Orange |

## Default Colors

| Color |
|-------|
| <kbd class="color" data-color="#C12D1D"></kbd> Blood Orange |
| <kbd class="color" data-color="#EE6D28"></kbd> Peach |
| <kbd class="color" data-color="#E09E3B"></kbd> Cream |
| <kbd class="color" data-color="#E5C943"></kbd> Beige |
| <kbd class="color" data-color="#1EB8CD"></kbd> Cyan |
| <kbd class="color" data-color="#00B3A6"></kbd> Teal |
| <kbd class="color" data-color="#2082C6"></kbd> Blue |
| <kbd class="color" data-color="#4354C1"></kbd> Indigo |
| <kbd class="color" data-color="#711C9E"></kbd> Purple |
| <kbd class="color" data-color="#CD3B70"></kbd> Violet |
| <kbd class="color" data-color="#B8343E"></kbd> Salmon |
| <kbd class="color" data-color="#28FF28"></kbd> Pastel Green |
| <kbd class="color" data-color="#FFFF28"></kbd> Pastel Yellow |
| <kbd class="color" data-color="#FF2828"></kbd> Pastel Red |
| <kbd class="color" data-color="#7F28FF"></kbd> Pastel Purple |
| <kbd class="color" data-color="#2828FF"></kbd> Pastel Blue |
| <kbd class="color" data-color="#FF5000"></kbd> Kira Orange |
| <kbd class="color" data-color="#EF0A81"></kbd> Kira Pink |
| <kbd class="color" data-color="#810AEF"></kbd> Kira Purple |
| <kbd class="color" data-color="#0A3CFF"></kbd> Kira Blue |

<script type="text/javascript">
    keyColor(document.getElementById("color0"), 0xC1, 0x2D, 0x1D);
</script>

## Unbricking

Please follow the [Unbrick guide](./BOSSA.md).

## Known Issues

- Some leds occasionally freeze if the led controller chip misbehaves
 - Unplugging and replugging the keyboard should fix the animations

- High RF Interference may cause the board to reset
 - Adding a choke may help. [See here](KiraRF.md)

Firmware issues can be reported on [Github Issues](https://github.com/kiibohd/controller/issues).

## Resources

### Case Files

To be released after shipping

### PCB Files

To be released after shipping

### Firmware

https://github.com/kiibohd/controller/tree/master/Keyboards
