## rtl8188eus development branch

# Realtek rtl8188eus &amp; rtl8188eu &amp; rtl8188etv WiFi drivers

[![Monitor mode](https://img.shields.io/badge/monitor%20mode-supported-brightgreen.svg)](#)
[![Frame Injection](https://img.shields.io/badge/frame%20injection-supported-brightgreen.svg)](#)
[![MESH Mode](https://img.shields.io/badge/mesh%20mode-supported-brightgreen.svg)](#)
[![GitHub issues](https://img.shields.io/github/issues/aircrack-ng/rtl8188eus.svg)](https://github.com/aircrack-ng/rtl8188eus/issues)
[![GitHub forks](https://img.shields.io/github/forks/aircrack-ng/rtl8188eus.svg)](https://github.com/aircrack-ng/rtl8188eus/network)
[![GitHub stars](https://img.shields.io/github/stars/aircrack-ng/rtl8188eus.svg)](https://github.com/aircrack-ng/rtl8188eus/stargazers)
[![GitHub license](https://img.shields.io/github/license/aircrack-ng/rtl8812au.svg)](https://github.com/aircrack-ng/rtl8188eus/blob/master/LICENSE)<br>
[![Android](https://img.shields.io/badge/android%20(8)-supported-brightgreen.svg)](#)
[![aircrack-ng](https://img.shields.io/badge/aircrack--ng-supported-blue.svg)](#)


# Supports
* Android 7
* MESH Support
* Monitor mode
* Frame injection
* Up to kernel v5.8+
... And a bunch of various wifi chipsets

# Howto build/install
1. Update your apt list `sudo apt update && sudo apt upgrade`
2. Install your linux header in order to compile the driver `sudo apt-get install linux-headers-$(uname -r)`
    - If this gives you an error, then you need to update your distro `sudo apt-get dist-upgrade` then reboot to upgrade the dirsto `sudo reboot`
3. Install extra `sudo apt install bc build-essential libelf-dev dkms`
4. Unload the driver `sudo rmmod r8188eu.ko`
2. Blacklist the original driver in order to use this one. `sudo echo 'blacklist r8188eu'|sudo tee -a '/etc/modprobe.d/realtek.conf'`
1. Clone the driver `git clone https://github.com/etahamad/rtl8188eus`
4. Enter the driver dir`cd rtl8188eus`
5. Compile the driver `sudo make && sudo make install`
6. Reboot in order to blacklist and load the new driver/module.
9. Load the new driver `sudo modprobe 8188eu`

# MONITOR MODE howto
Use these steps to enter monitor mode.
```
$ sudo airmon-ng check kill
$ sudo ip link set <interface> down
$ sudo iw dev <interface> set type monitor
```
Frame injection test may be performed with
(after kernel v5.2 scanning is slow, run a scan or simply an airodump-ng first!)
```
$ aireplay -9 <interface>
```

# NetworkManager configuration
Add these lines below to "NetworkManager.conf" and ADD YOUR ADAPTER MAC below [keyfile]
This will make the Network-Manager ignore the device, and therefore don't cause problems.
```
[device]
wifi.scan-rand-mac-address=no

[ifupdown]
managed=false

[connection]
wifi.powersave=0

[main]
plugins=keyfile

[keyfile]
unmanaged-devices=mac:A7:A7:A7:A7:A7
```

# Credits
Realtek       - https://www.realtek.com<br>
Alfa Networks - https://www.alfa.com.tw<br>
aircrack-ng.  - https://www.aircrack-ng.org<br>
<br>
And all those who may be using or contributing to it of anykind. Thanks!<br>
