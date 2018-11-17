## Installing Firmware

First place the keyboard into re-flash mode. This can be done either by
pressing the re-flash button on the PCB/Teensy. Or by entering the Kiibohd
Virtual Serial Port and using the 'reload' command.

To load the newly built firmware, run: `./load`.

Note: If you get a permission denied error on Linux or Mac then please run the
command with sudo, or install the udev rule.


### Flashing - macOS

 1. Navigate to the directory you unzipped the firmware to
 2. With your keyboard in flash mode enter the command `dfu-util -D kiibohd.dfu.bin`
    - If the above fails, try running the command with `sudo` (i.e. `sudo dfu-util -D kiibohd.dfu.bin`)

### Flashing - linux

 1. Navigate to the directory you unzipped the firmware to
 2. With your keyboard in flash mode enter the command `dfu-util -D kiibohd.dfu.bin`
    - If the above fails, try running the command with `sudo` (i.e. `sudo dfu-util -D kiibohd.dfu.bin`)


### Flashing - Windows
 1. Copy the `kiibohd.dfu.bin` file from the unpacked firmware zip file into the same directory you installed `dfu-util`
 2. Open a command prompt (Start => cmd.exe)
 3. Change directories to the `dfu-util` directory - `cd "C:\<path>\<to>\<dir>"`
 4. Execute the command `dfu-util -D kiibohd.dfu.bin`

Note: be patient the first couple of times, Windows is slow at installing drivers...
