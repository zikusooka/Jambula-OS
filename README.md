![alt text](logo.png "Jambula OS (Pi Edition)")
# Jambula-OS

Jambula OS is a custom and embedded Linux distribution used by Jambula Labs. 

<b>Pre-requisites</b>

Currently, Jambula OS (Pi Edition) is a console only platform used as a mini server.  Therefore in order to use it
effectively, you need to already be familiar with using Linux via the command line interface.

You will also need a Raspberry Pi device with all accessories required to boot including and SD card.  Older Raspberry Pi models are supported out of the box

![alt text](console.png "Jambula OS (Pi Edition)")

<b> How to get started </b>

1. Download the latest Jambula OS image to a temporary directory:

   wget -P /tmp -c https://github.com/zikusooka/Jambula-OS/raw/main/jambulaOS-202311-img.7z

2. Extract the above image to a temporary directory using p7zip tool (https://www.7-zip.org/download.html)

   cd /tmp

   7za e /tmp/jambulaOS-img.7z

3. Burn the resulting image i.e. sdcard.img to your SD card using a tool such as dd e.g:

   dd status=progress bs=512 if=/tmp/sdcard.img of=/dev/sdb

4. Insert SD card into your raspberry pi and power it on

5. Log in as root and use the default password of "JambulaOS"
   IMPORTANT: Please change this immediately

6. Enjoy!
