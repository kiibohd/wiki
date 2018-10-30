Sometimes your keyboard doesn't work as expected. In most cases you've just uncovered some odd firmware corner case bug. This wiki describes the sort of information you can provide so that other keyboard hackers can help you out more quickly.

# General

Here are various tools that are either already available on your computer or are relatively easy to acquire that provide very useful information.

## Windows

TODO

- lsusb equivlaent
- dmesg event equivalent (shows a time-stamp'ish thing associated with USB insertion/removal events)

## Linux

Linux is probably the easiest to report.

dmesg shows various system events, such as when USB devices are connected and drivers are loaded. This can give indications on whether the keyboard has successfully initialized and isn't flaky (constantly disconnecting/reconnecting).

### dmesg

`dmesg | tail -n 50`

```dmesg
[ 2424.426106] NVRM: corruption and stability problems, and is not supported.
[ 2424.427006] nvidia-modeset: Allocated GPU:0 (GPU-2d2cc665-31f7-257d-e164-1b1b55d22705) @ PCI:0000:02:00.0
[ 2424.833498] snd_hda_codec_hdmi hdaudioC1D0: HDMI: invalid ELD data byte 41
[33897.878182] usb 3-2: new full-speed USB device number 13 using xhci_hcd
[34757.262658] perf: interrupt took too long (2541 > 2500), lowering kernel.perf_event_max_sample_rate to 78600
[37756.596746] usb 3-2: USB disconnect, device number 13
[44701.517445] usb 3-2: new full-speed USB device number 14 using xhci_hcd
[45315.354964] perf: interrupt took too long (3206 > 3176), lowering kernel.perf_event_max_sample_rate to 62100
[49115.452960] usb 3-2: USB disconnect, device number 14
[54713.232462] usb 3-6: new full-speed USB device number 15 using xhci_hcd
[54739.911224] usb 3-6: USB disconnect, device number 15
[54742.019576] usb 3-6: new full-speed USB device number 16 using xhci_hcd
[54747.459440] usb 3-6: USB disconnect, device number 16
[54763.239924] usb 3-5: new full-speed USB device number 17 using xhci_hcd
[54871.559821] usb 3-5: USB disconnect, device number 17
[54873.501664] usb 3-5: new full-speed USB device number 18 using xhci_hcd
[55037.024336] usb 3-5: USB disconnect, device number 18
[55039.864387] usb 3-5: new full-speed USB device number 19 using xhci_hcd
[55112.978729] usb 3-5: USB disconnect, device number 19
[55116.505588] usb 3-5: new full-speed USB device number 20 using xhci_hcd
[55116.704341] cdc_acm 3-5:1.0: ttyACM0: USB ACM device
[55116.704548] usbcore: registered new interface driver cdc_acm
[55116.704551] cdc_acm: USB Abstract Control Model driver for USB modems and ISDN adapters
[62334.262542] usb 3-12.4.2: USB disconnect, device number 10
[62812.743031] usb 3-12.4.4.4: USB disconnect, device number 12
[69580.783606] perf: interrupt took too long (4037 > 4007), lowering kernel.perf_event_max_sample_rate to 49500
[102823.058377] perf: interrupt took too long (5063 > 5046), lowering kernel.perf_event_max_sample_rate to 39300
[174482.288001] perf: interrupt took too long (6345 > 6328), lowering kernel.perf_event_max_sample_rate to 31500
[222582.835068] usb 3-5: USB disconnect, device number 20
[590544.677341] usb 3-12.4.3: new full-speed USB device number 21 using xhci_hcd
[590544.768390] usb 3-12.4.3: config 1 has an invalid interface number: 6 but max is 5
[590544.768397] usb 3-12.4.3: config 1 has no interface number 5
[590544.770443] drivers/hid/usbhid/hid-core.c: HID probe called for ifnum 0
[590544.771944] drivers/hid/usbhid/hid-core.c: submitting ctrl urb: Set_Report wValue=0x0200 wIndex=0x0000 wLength=1
[590544.772065] input: Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full as /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0/0003:1C11:B04D.0008/input/input14
[590544.824478] hid-generic 0003:1C11:B04D.0008: input,hidraw4: USB HID v1.11 Keyboard [Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full] on usb-0000:00:14.0-12.4.3/input0
[590544.824804] drivers/hid/usbhid/hid-core.c: HID probe called for ifnum 1
[590544.826175] drivers/hid/usbhid/hid-core.c: submitting ctrl urb: Get_Report wValue=0x0101 wIndex=0x0001 wLength=29
[590544.826518] input: Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full as /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.1/0003:1C11:B04D.0009/input/input15
[590544.877755] hid-generic 0003:1C11:B04D.0009: input,hidraw5: USB HID v1.11 Keyboard [Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full] on usb-0000:00:14.0-12.4.3/input1
[590544.878008] drivers/hid/usbhid/hid-core.c: HID probe called for ifnum 2
[590544.879011] drivers/hid/usbhid/hid-core.c: submitting ctrl urb: Get_Report wValue=0x0102 wIndex=0x0002 wLength=2
[590544.879255] drivers/hid/usbhid/hid-core.c: submitting ctrl urb: Get_Report wValue=0x0103 wIndex=0x0002 wLength=3
[590544.879673] input: Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full as /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.2/0003:1C11:B04D.000A/input/input16
[590544.930857] hid-generic 0003:1C11:B04D.000A: input,hidraw6: USB HID v1.11 Device [Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full] on usb-0000:00:14.0-12.4.3/input2
[590544.931211] cdc_acm 3-12.4.3:1.3: ttyACM0: USB ACM device
[590544.932229] drivers/hid/usbhid/hid-core.c: HID probe called for ifnum 6
[590544.933066] drivers/hid/usbhid/hid-core.c: submitting ctrl urb: Get_Report wValue=0x0100 wIndex=0x0006 wLength=6
[590544.933401] input: Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full as /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.6/0003:1C11:B04D.000B/input/input17
[590544.933598] hid-generic 0003:1C11:B04D.000B: input,hidraw7: USB HID v1.11 Mouse [Kiibohd Keyboard - MDErgo1 PartialMap pjrcUSB full] on usb-0000:00:14.0-12.4.3/input6
```

lsusb shows which all the currently connected USB devices on the system. The example below shows only one device, but please include the full output when reporting. Include both the short-form and long-form. sudo gives a bit more information on the long-form/verbose output that is useful. Don't worry about the Report Descriptors being UNAVAILABLE.

### lsusb

`lsusb`

```bash
Bus 006 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 005 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 002: ID 8087:8002 Intel Corp.
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 002: ID 8087:800a Intel Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 004: ID 2109:0812 VIA Labs, Inc. VL812 Hub
Bus 004 Device 003: ID 2109:0812 VIA Labs, Inc. VL812 Hub
Bus 004 Device 002: ID 2109:0812 VIA Labs, Inc. VL812 Hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 007: ID 0557:2419 ATEN International Co., Ltd
Bus 003 Device 005: ID 0557:7000 ATEN International Co., Ltd Hub
Bus 003 Device 011: ID 2109:2812 VIA Labs, Inc. VL812 Hub
Bus 003 Device 021: ID 1c11:b04d
Bus 003 Device 009: ID 1679:2001 Total Phase Beagle Protocol Analyzer
Bus 003 Device 008: ID 2109:2812 VIA Labs, Inc. VL812 Hub
Bus 003 Device 006: ID 067b:2303 Prolific Technology, Inc. PL2303 Serial Port
Bus 003 Device 004: ID 2109:2812 VIA Labs, Inc. VL812 Hub
Bus 003 Device 003: ID 0853:0107 Topre Corporation
Bus 003 Device 002: ID 5332:1300
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

`sudo lsusb -vvv`

```bash
Bus 003 Device 021: ID 1c11:b04d
Device Descriptor:
  bLength                18
  bDescriptorType         1
  bcdUSB               2.00
  bDeviceClass            0
  bDeviceSubClass         0
  bDeviceProtocol         0
  bMaxPacketSize0        64
  idVendor           0x1c11
  idProduct          0xb04d
  bcdDevice            1.00
  iManufacturer           1 Kiibohd
  iProduct                2 Keyboard - MDErgo1 PartialMap pjrcUSB full
  iSerial                 3 Clean master - 2016-06-12 15:53:25 -0700
  bNumConfigurations      1
  Configuration Descriptor:
    bLength                 9
    bDescriptorType         2
    wTotalLength          175
    bNumInterfaces          6
    bConfigurationValue     1
    iConfiguration          0
    bmAttributes         0xa0
      (Bus Powered)
      Remote Wakeup
    MaxPower              500mA
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        0
      bAlternateSetting       0
      bNumEndpoints           1
      bInterfaceClass         3 Human Interface Device
      bInterfaceSubClass      1 Boot Interface Subclass
      bInterfaceProtocol      1 Keyboard
      iInterface              4 Boot Keyboard
        HID Device Descriptor:
          bLength                 9
          bDescriptorType        33
          bcdHID               1.11
          bCountryCode            0 Not supported
          bNumDescriptors         1
          bDescriptorType        34 Report
          wDescriptorLength      63
         Report Descriptors:
           ** UNAVAILABLE **
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x81  EP 1 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0008  1x 8 bytes
        bInterval               1
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        1
      bAlternateSetting       0
      bNumEndpoints           1
      bInterfaceClass         3 Human Interface Device
      bInterfaceSubClass      0
      bInterfaceProtocol      1 Keyboard
      iInterface              5 NKRO Keyboard
        HID Device Descriptor:
          bLength                 9
          bDescriptorType        33
          bcdHID               1.11
          bCountryCode            0 Not supported
          bNumDescriptors         1
          bDescriptorType        34 Report
          wDescriptorLength     125
         Report Descriptors:
           ** UNAVAILABLE **
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x82  EP 2 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               1
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        2
      bAlternateSetting       0
      bNumEndpoints           1
      bInterfaceClass         3 Human Interface Device
      bInterfaceSubClass      1 Boot Interface Subclass
      bInterfaceProtocol      0
      iInterface              6 Media Keys
        HID Device Descriptor:
          bLength                 9
          bDescriptorType        33
          bcdHID               1.11
          bCountryCode            0 Not supported
          bNumDescriptors         1
          bDescriptorType        34 Report
          wDescriptorLength      53
         Report Descriptors:
           ** UNAVAILABLE **
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x83  EP 3 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0008  1x 8 bytes
        bInterval               1
    Interface Association:
      bLength                 8
      bDescriptorType        11
      bFirstInterface         3
      bInterfaceCount         2
      bFunctionClass          2 Communications
      bFunctionSubClass       2 Abstract (modem)
      bFunctionProtocol       1 AT-commands (v.25ter)
      iFunction               0
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        3
      bAlternateSetting       0
      bNumEndpoints           1
      bInterfaceClass         2 Communications
      bInterfaceSubClass      2 Abstract (modem)
      bInterfaceProtocol      1 AT-commands (v.25ter)
      iInterface              7 Virtual Serial Port - Status
      CDC Header:
        bcdCDC               1.10
      CDC Call Management:
        bmCapabilities       0x01
          call management
        bDataInterface          4
      CDC ACM:
        bmCapabilities       0x06
          sends break
          line coding and serial state
      CDC Union:
        bMasterInterface        3
        bSlaveInterface         4
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x84  EP 4 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0010  1x 16 bytes
        bInterval              64
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        4
      bAlternateSetting       0
      bNumEndpoints           2
      bInterfaceClass        10 CDC Data
      bInterfaceSubClass      0
      bInterfaceProtocol      0
      iInterface              8 Virtual Serial Port - Data
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x05  EP 5 OUT
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               0
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x86  EP 6 IN
        bmAttributes            2
          Transfer Type            Bulk
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0040  1x 64 bytes
        bInterval               0
    Interface Descriptor:
      bLength                 9
      bDescriptorType         4
      bInterfaceNumber        6
      bAlternateSetting       0
      bNumEndpoints           1
      bInterfaceClass         3 Human Interface Device
      bInterfaceSubClass      0
      bInterfaceProtocol      2 Mouse
      iInterface             10 Mouse
        HID Device Descriptor:
          bLength                 9
          bDescriptorType        33
          bcdHID               1.11
          bCountryCode            0 Not supported
          bNumDescriptors         1
          bDescriptorType        34 Report
          wDescriptorLength      51
         Report Descriptors:
           ** UNAVAILABLE **
      Endpoint Descriptor:
        bLength                 7
        bDescriptorType         5
        bEndpointAddress     0x89  EP 9 IN
        bmAttributes            3
          Transfer Type            Interrupt
          Synch Type               None
          Usage Type               Data
        wMaxPacketSize     0x0008  1x 8 bytes
        bInterval               1
Device Status:     0x0000
  (Bus Powered)
```

### udev

While also useful for debugging udev rules, you can also use the udev monitor to determine when devices are attached and initialized. Below is an example of the flash/bootloader jump button being pressed.

`sudo udevadm monitor --kernel --udev`

```bash
monitor will print the received events for:
UDEV - the event which udev sends out after rule processing
KERNEL - the kernel uevent

KERNEL[100908.330958] remove   /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0 (usb)
KERNEL[100908.331118] remove   /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3 (usb)
UDEV  [100908.332526] remove   /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0 (usb)
UDEV  [100908.345424] remove   /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3 (usb)
KERNEL[100908.618268] add      /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3 (usb)
KERNEL[100908.618574] add      /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0 (usb)
UDEV  [100908.637199] add      /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3 (usb)
UDEV  [100908.638837] add      /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0 (usb)
```

You can also print out the environment view, which will show you the information that udev has queried about the device at each stage.

`sudo udevadm monitor --kernel --udev --environment`

```bash
KERNEL[101543.258967] add      /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0 (usb)
ACTION=add
DEVPATH=/devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3/3-12.4.3:1.0
DEVTYPE=usb_interface
INTERFACE=255/255/255
MODALIAS=usb:v0403p6001d0600dc00dsc00dp00icFFiscFFipFFin00
PRODUCT=403/6001/600
SEQNUM=5763
SUBSYSTEM=usb
TYPE=0/0/0

UDEV  [101543.282830] add      /devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3 (usb)
ACTION=add
BUSNUM=003
DEVNAME=/dev/bus/usb/003/019
DEVNUM=019
DEVPATH=/devices/pci0000:00/0000:00:14.0/usb3/3-12/3-12.4/3-12.4.3
DEVTYPE=usb_device
DRIVER=usb
ID_BUS=usb
ID_FOR_SEAT=usb-pci-0000_00_14_0-usb-0_12_4_3
ID_MODEL=FT232R_USB_UART
ID_MODEL_ENC=FT232R\x20USB\x20UART
ID_MODEL_FROM_DATABASE=FT232 Serial (UART) IC
ID_MODEL_ID=6001
ID_PATH=pci-0000:00:14.0-usb-0:12.4.3
ID_PATH_TAG=pci-0000_00_14_0-usb-0_12_4_3
ID_REVISION=0600
ID_SERIAL=FTDI_FT232R_USB_UART_A50449P0
ID_SERIAL_SHORT=A50449P0
ID_USB_INTERFACES=:ffffff:
ID_VENDOR=FTDI
ID_VENDOR_ENC=FTDI
ID_VENDOR_FROM_DATABASE=Future Technology Devices International, Ltd
ID_VENDOR_ID=0403
MAJOR=189
MINOR=274
PRODUCT=403/6001/600
SEQNUM=5762
SUBSYSTEM=usb
TAGS=:seat:uaccess:
TYPE=0/0/0
USEC_INITIALIZED=101543266331
```

## macOS

TODO

- lsusb thing
- dmesg event equivalent (shows a time-stamp'ish thing associated with USB insertion/removal events)

# Advanced

If you really want to dive more deeply into reporting issues, here are a few things you can attempt. They require more knowledge about how things work, and perhaps even buying external tools to gather the information.

TODO

- Wireshark (Linux/Windows)
- Total Phase Beagle USB

## USB HID Debug Mode (Linux)

You can enable HID Debug Mode in the Linux Kernel. This allows you to print out what Linux thinks the USB descriptor looks like (and enables a more verbose dmesg). You'll need to add the following file to your system and reboot.

`/etc/modprobe.d/usb_debug.conf`

```bash
options hid debug=2
```

This will enabled the debugfs path (requires root) for USB HID. In general you shouldn't have to go this far unless you want to verify that the USB descriptors make all the keys you want to use available. There will be a report for each endpoint descriptor (which can vary depending on how your firmware was compiled). You can find the keyboard ID from lsusb (e.g. 1c11:b04d).

For example `/sys/kernel/debug/hid/0003:1C11:B04D.000B/rdesc`

```
05 01 09 02 a1 01 09 02 a1 02 09 01 a1 00 05 09 19 01 29 10 15 00 25 01 75 01 95 10 81 02 05 01 09 30 09 31 16 01 80 26 ff 7f 75 10 95 02 81 06 c0 c0 c0

  INPUT[INPUT]
    Field(0)
      Physical(GenericDesktop.Pointer)
      Logical(GenericDesktop.Mouse)
      Application(GenericDesktop.Mouse)
      Usage(16)
        Button.0001
        Button.0002
        Button.0003
        Button.0004
        Button.0005
        Button.0006
        Button.0007
        Button.0008
        Button.0009
        Button.000a
        Button.000b
        Button.000c
        Button.000d
        Button.000e
        Button.000f
        Button.0010
      Logical Minimum(0)
      Logical Maximum(1)
      Report Size(1)
      Report Count(16)
      Report Offset(0)
      Flags( Variable Absolute )
    Field(1)
      Physical(GenericDesktop.Pointer)
      Logical(GenericDesktop.Mouse)
      Application(GenericDesktop.Mouse)
      Usage(2)
        GenericDesktop.X
        GenericDesktop.Y
      Logical Minimum(-32767)
      Logical Maximum(32767)
      Report Size(16)
      Report Count(2)
      Report Offset(16)
      Flags( Variable Relative )

Button.0001 ---> Key.LeftBtn
Button.0002 ---> Key.RightBtn
Button.0003 ---> Key.MiddleBtn
Button.0004 ---> Key.SideBtn
Button.0005 ---> Key.ExtraBtn
Button.0006 ---> Key.ForwardBtn
Button.0007 ---> Key.BackBtn
Button.0008 ---> Key.TaskBtn
Button.0009 ---> Key.?
Button.000a ---> Key.?
Button.000b ---> Key.?
Button.000c ---> Key.?
Button.000d ---> Key.?
Button.000e ---> Key.?
Button.000f ---> Key.?
Button.0010 ---> Key.?
GenericDesktop.X ---> Relative.X
GenericDesktop.Y ---> Relative.Y
```
