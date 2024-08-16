![alt text](logo.png "Jambula OS (Pi Edition)")
# Jambula-OS

Jambula OS is a custom and embedded Linux distribution for use on SoC devices such as the Raspberry Pi 

It is mainly used by our company i.e. Jambula Labs to build smart devices such as JambulaTV, 
a low cost and smart home hub that automates several tasks in your house or apartment while providing security and 
privacy to you and your family. Read more about it at: https://jambulatv.com


<b>Pre-requisites</b>

Currently, Jambula OS (Pi Edition) is a console only platform running several open source and popular software 
services.  There's an initial ncurses style based setup program that allows you to configure the functions that
will be provided by your Raspberry Pi.  However, in order to use it effectively, you need to already be 
familiar with using Linux on the command line interface (CLI).

You will also need a Raspberry Pi 5 device with all accessories required to boot including and SD card.  


<b>Supported Boards</b>

1. Raspberry Pi 5 Model B Rev 1.0


![alt text](console.png "Jambula OS (Pi Edition)")

<b> How to quickly get started </b>

1. Download the latest Jambula OS image to a temporary directory:

   wget -P /tmp -c https://github.com/zikusooka/Jambula-OS/raw/main/jambulaOS-202407-181211-img.7z

2. Extract the above image to a temporary directory using p7zip tool (https://www.7-zip.org/download.html)

   cd /tmp

   7za e /tmp/jambulaOS-202407-181211-img.7z

3. Burn the resulting image i.e. sdcard.img to your SD card using a tool such as dd

   For example: If your SD card is mounted at /dev/sdb enter the following command line:

   dd status=progress if=/tmp/sdcard.img of=/dev/sdb

4. Insert SD card into your raspberry pi and power it on

5. During the first boot process, Jambula OS will perform an initial system 
   configuration and reboot automatically. Upon full reboot, a setup screen will be 
   presented to allow you setup your Pi according to your needs.

![alt text](jambula_os_setup.png "Jambula OS Setup")
 
6. Log in as root and use the default password of "Jambula"
   IMPORTANT: Please change this immediately

7. Enjoy!
