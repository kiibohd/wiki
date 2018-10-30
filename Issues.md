This wiki is a list of known USB issues. Hopefully over time some of them may be fixed (or OSs and BIOSs patched...).

Please indicate hardware and software information if you notice your system exhibits the issue (this wiki is editable). If you have a custom kernel, please indicate and describe the changes.

Example

- Windows 10.1 (Lenovo X230)
- Arch Linux 4.8.13-1-ARCH (Supermicro MBD-X11SAE-M-O)

# Boot

## Keyboard stays in 6KRO (Boot) Mode on boot-up but works in NKRO Mode when plugged in

On some systems, often Windows, the BIOS seems to do a hand-over of the USB Keyboard and doesn't request an NKRO keyboard (like macOS does) during boot.
Another way to resolve this would be to force re-init USB devices during boot-up. Unfortunately this would cause issues when booting from a USB mass storage device (which is likely the cause of this whole problem).

### Known Affected Systems

- Windows 7 64 bit (Dell OptiPlex 790)

# Suspend/Resume

# HID
