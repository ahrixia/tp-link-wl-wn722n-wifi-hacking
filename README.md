# TP-Link WL-WN722N Monitor Mode 
TP-Link WL-WN722N v1 has monitor mode enabled on it but current version available of this model are V2/V3.
Luckily Aircrack-ng released compatible drivers for this wireless adpater. :) 

Run these set of commands on your kali machine: 
```
$ sudo apt update 
$ sudo apt upgrade 
$ sudo apt-get dist-upgrade
$ sudo apt-get install bc libelf-dev build-essential dkms
```

Now rebooting kali machine:
```
$ sudo apt-get install linux-headers-$(uname -r)
```
Plug in the TP-Link wireless adapter and run:
```
$ sudo rmmod r8188eu.ko
$ git clone https://github.com/aircrack-ng/rtl8188eus
$ cd rtl8188eus
$ sudo bash -c 'echo "blacklist r8188eu" > /etc/modprobe.d/realtek.conf'
```

Rebooting again and run:
```
$ cd rtl8188eus
$ sudo make
$ sudo make install
$ sudo modprobe 8188eu
```
After it is done, you can check for monitor mode via:

```
$ sudo ifconfig wlan0 down
$ sudo airmon-ng check kill
$ sudo iwconfig wlan0 mode monitor
$ sudo ifconfig wlan0 up
$ iwconfig 
```

**Note**: The wireless interface monitor mode will have same interface name as wireless interface. 

Eg- wlan0 or wlan1

**NOT** - wlan0mon or wlan1mon



