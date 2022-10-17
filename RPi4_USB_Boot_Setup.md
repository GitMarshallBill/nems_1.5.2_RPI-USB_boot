# Getting the Pi 4 to USB boot NEMS 1.5.2

**NOTE:** Not all USB drives will work. I have tested a couple different ssd's and USB sticks from Samsung and SanDisk and have been successful.

 If the Raspberry Pi has not been updated you will need to have a micro sd card flashed with Raspberry Pi OS to boot the pi and do updates. If Pi eeprom and firmware already updated skip to Step 4

1. Boot the Raspberry Pi with the Raspberry Pi OS microSD card.

2. Open Terminal in Raspberry Pi OS (Note: you can do these steps from another computer via SSH if you want to set up the Pi headless).

3. Run the following:

   1. `sudo apt update`
   2. `sudo apt full-upgrade`
   3. `sudo rpi-update`
   4. `sudo reboot`
   5. `sudo rpi-eeprom-update -a`
   6. `sudo reboot`
   7. `sudo vcgencmd bootloader_version`

   This should output something like:

   pi@raspberrypi:~ $ sudo vcgencmd bootloader_version
   > Jul 16 2020 16:15:46  
   > version 45291ce619884192a6622bef8948fb5151c2b456 (release)  
   > timestamp 1594912546  

   **The date can be anything like July 16 2020 OR LATER!**

4) Open a terminal and run `sudo raspi-config`

5) Select 6 Advanced Options, Select A6 Boot Order, Select B1, select OK, Reboot

6)  Start here if Pi eeprom and firmware already updated

7)  Plug your USB drive into the Pi while it's booted and make sure the Pi recognizes it (it should appear on your desktop, or you can also look for it with lsusb). Not all external drives and USB to SATA adapters work out of the box.

8)  Flash NEMS OS onto your USB drive.

9)  Before you eject the boot volume, you need to replace some files on it with the latest versions from GitHub:

10)  Go to the GitHub repository (https://github.com/GitMarshallBill/nems_1.5.2_RPI-USB_boot.git) and download the zip or clone the project to your computer.
      
11)  Copy all downloaded files that end in .elf or .dat to the boot volume of your USB drive (replace the same-named files that already exist there - it should total about 22MB).
    
12) Eject the boot volume, and unplug the USB drive.

13) Shut down the Pi if it's currently running from the microSD card. Then unplug the microSD card, and plug in the USB drive.

14) Make sure you plug the drive into a USB 3.0 port (the blue-colored ones), and not one of the USB 2.0 ports (the black-colored ones), or else you'll be severely limited in throughput.

15) Power up the Pi, and after a minute or so (it has to expand the USB drive to fill the volume and then reboot), it should boot up!

**NOTE:**  You may run into this screen after the soft reboot:

*Raspberry Pi 4 failed to soft reboot with external USB SSD*

*It seems related to the bug Bootloader can't boot via USB-HDD after system reboot, and the solution (for now) is to unplug the Pi to power it down completely, then plug it back in. May be resolved!!*
