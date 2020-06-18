# ubuntu-20.04-dell-xps-15-2020
Installing ubuntu 20.04 LTS on Dell XPS 15 9500 2020. 

System has 32 GB RAM, Core i7 CPU, nVidia GeForce GTX 1650 Ti graphics card.

## Window and BIOS config

Follow along from here:
https://medium.com/@tylergwlum/my-journey-installing-ubuntu-18-04-on-the-dell-xps-15-7590-2019-756f738a6447
12

Boot into Windows. 
Use cmd, running as administrator and run

`bcdedit /set {current} safeboot minimal`

Restart and push F2 to boot into BIOS. 
In BIOS select “Storage” from the list on the left.
Under “SATA Operation” select AHCI radio button
Hit “Apply Changes” button, and confirm
Select “Exit” and reboot into windows

Windows will be in safe mode

Run cmd as admin
`bcdedit /deletevalue {current} safeboot`

Reboot windows, should be OK.

Reboot back into BIOS and disable secure boot.

## Install Ubuntu

Reboot with Ubuntu USB key for install. Use F12 key to change boot order for USB.
Option for HDD encryption not present in dual boot situation.
Installed and booted OK. 

## nVidia graphics

Nvidia detecting, needed to update the pci ids database to properly find it:
Sudo update-pciids

lspci | grep -i nvidia

Detects it and names it properly, but does not show up under ubuntu-drivers devices

Add graphics drivers ppa
```
sudo add-apt-repository ppa:graphics-drivers/ppa
```
https://forums.linuxmint.com/viewtopic.php?t=276004
I have an nvidia GeForce GTX 1650 Ti which does not seem to have a linux driver available, at least not obviously supported. It's not auto-detected by any of the Ubuntu driver tools, so I Installed latest manually.
```
sudo apt-get install nvidia-driver-440
```
and all was hunky-dory. PRIME and other features work.

## External Monitor

Detects presense of monitor, can display. There are issues if I try to change the arrangement of the monitors so that instead of side-by-side the external is on top. It just won't do it and often stops displaying on 2nd monitor after attempting to apply.

## SD-Card Reader

Ubuntu has difficulty detecting insertion of card. Typing lspci miraculously causes discovery sometimes.

No issues in Windows; not a hardware problem.

No issues mounting SD-Card using external USB adaptor.

## Firmware updater

The linux firmware updater appears to work correctly

https://itsfoss.com/update-firmware-ubuntu/

## References

Install ubuntu 18.04 on xps 15 2019
https://medium.com/@tylergwlum/my-journey-installing-ubuntu-18-04-on-the-dell-xps-15-7590-2019-756f738a6447


Install ubuntu 19.10 on Dell xps 15 7590 2020
https://medium.com/@voghDev_63848/my-journey-installing-ubuntu-19-10-on-the-dell-xps-15-7590-2020-cfffd912cb2a


Install ubuntu 20.04 on Dell xps 15 9500 2020 (similar to this one)
https://medium.com/@asad.manji/my-journey-installing-ubuntu-20-04-on-the-dell-xps-15-9500-2020-8ac8560373d1

Ubuntu-Dell-XPS-15-2019
https://github.com/TillmannBerg/Ubuntu-Dell-XPS-15-2019
