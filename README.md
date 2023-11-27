# Jambula-OS
Jambula OS is a custom and embedded Linux distribution used by Jambula Labs

Instructions
1. Download Jambula OS image i.e. jambulaOS-img.7z
2. Extract the above image to a temporary directory using p7zip tool
   cd /tmp
   7za e /tmp/jambulaOS-img.7z

3. Burn the resulting image i.e. sdcard.img to your SD card using a tool such as dd e.g.
  dd status=progress bs=512 if=/tmp/sdcard.img of=/dev/sdb
4. Insert SD card into your raspberry pi and boot
5. Enjoy!
