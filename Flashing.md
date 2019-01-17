?> The [Configurator](Quickstart.md) is the easiest way to flash your keyboard, but you can also do it manually if you desire.

## Install dfu

<!-- tabs:start -->

#### ** Windows **

- Download and run: [Windows Driver Installer](https://github.com/kiibohd/kiidrv/releases/download/v1.5.3-kiidrv/KiibohdDrivers.msi)
- Download [dfu-util](http://dfu-util.sourceforge.net) and extract to a folder
- Shift-Right Click and say "Open command window here"

#### ** Mac **

- Install [Brew](https://brew.sh/)

- Run the following command in a terminal:

 - `sudo brew install dfu`

#### ** Debian, Ubuntu, Mint **

Run the following command in a terminal:

 - `sudo apt-get install dfu-util`

#### ** Fedora **

Run the following command in a terminal:

 - `sudo dnf install dfu-util`

#### ** Arch **

Run the following command in a terminal:

 - `sudo pacman -S dfu-util`

#### ** Other Linux **

Install [dfu-util](http://dfu-util.sourceforge.net) using your systems package manager

<!-- tabs:end -->

## Download a .bin file for your keyboard

Official firmware files can be found on the [Github Releases](https://github.com/kiibohd/controller/releases) page

## Run dfu

In the terminal type `dfu-util -D keyboard.dfu.bin`

(*Replace keyboard.dfu.bin with the name of the bin file you downloaded*)
