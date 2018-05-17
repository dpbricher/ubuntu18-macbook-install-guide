# Installing Ubuntu 18.04 on a Mac

## State of this Guide

This is currently only a basic set of instructions that may not be overly clear in some areas. Will hopefully improve this later.

## About the Mac

| Feature   | Spec                                      |
|-----------|-------------------------------------------|
| Network   | BCM4350 802.11ac Wireless Network Adapter |
| Ports     | 2 USB-C ports, 1 headphones port          |
| Processor | Intel® Core™ i5-7360U CPU @ 2.30GHz × 4   |
| RAM       | 8GB                                       |
| Storage   | 256GB SSD                                 |

## Warnings

- OS behaviour is reasonably stable, but not entirely
- Camera does not work
- Internal speakers and headphone jack do not work
- Sometimes has issues switching between wifi networks

## Prerequisites

- Ethernet cable (with USB-C adaptor)
- USB with enough storage to create an Ubuntu startup disk (I think > 2GB is enough) and a USB to USB-C converter
- External keyboard and/or mouse (can use on-screen keyboard if only mouse)
- Linux OS with [Startup Disk Creator][] program to create startup disk from

## Steps

- Partition Mac SSD using 'Disk Utility' and add 2 partitions for Ubuntu:
  - One partition is for boot, and should be 1GB
  - The other is for the OS, and should be 8GB+
- Download [Ubuntu 16.04.4 desktop][] image
- Use [Startup Disk Creator][] to create a bootable USB from the image (I tried using UNetbootin for Mac initially, but it created flawed images)
- Boot Mac with Ubuntu USB plugged in and boot from it (hold 'option' during boot until boot devices appear)
- Mac keyboard and touchpad will not work, so use external ones
- Once booted, run the 'Install Ubuntu' program visible on the desktop. When it gets to the section that mentions erasing parts of the disk, choose the 'something else' option, and then select the follow changes before proceeding:
  - Entire SSD as disk to use for boot partition (this is a drop down list, should already by correct)
  - Use the 1GB partition (format as EXT4, mount point '/boot')
  - Use the 8GB+ partition (format as EXT4, mount point '/')
- Once installed, Mac should boot directly into Ubuntu, and the following will no longer work:
  - Keyboard
  - Touchpad
  - Wifi
  - Camera
- From Ubuntu, attach ethernet cable and update to Ubuntu 18.04 with the following terminal commands:
  - `sudo apt update`
  - `sudo apt upgrade`
  - `sudo apt dist-upgrade`
  - `sudo do-release-upgrade -d`
- Once the process has completed and the Mac has been restarted, (most of) the non-working peripherals can now be fixed

## Fixing Things

- Wifi: This can be fixed by running `sudo apt-get install firmware-b43-installer` (may require restart)
- Keyboard and touchpad: Build [macbook12-spi-driver][]s
- Boot back into Mac OS: Hold the 'option' key while booting and then pick the correct device. [rEFInd][] can also be installed from within Mac OSX.


[Boot-Repair]:            https://help.ubuntu.com/community/Boot-Repair
[macbook12-spi-driver]:   https://github.com/roadrunner2/macbook12-spi-driveri
[rEFInd]:                 http://www.rodsbooks.com/refind/
[Startup Disk Creator]:   https://en.wikipedia.org/wiki/Startup_Disk_Creator
[Ubuntu 16.04.4 desktop]: http://releases.ubuntu.com/16.04/ubuntu-16.04.4-desktop-amd64.iso
