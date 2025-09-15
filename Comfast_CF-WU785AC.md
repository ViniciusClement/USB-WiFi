* https://github.com/morrownr/USB-WiFi/blob/main/home/How_to_Modeswitch.md

* https://www.reddit.com/r/linux4noobs/comments/14cupwn/wireless_wifi_adapters_100_linux_compatible/

* https://oemdrivers.com/network-comfast-cf-wu785ac

* https://www.kali.org/docs/nethunter/wireless-cards/

## Kali Linux WiFi Alfa Adapter Fix

* https://www.youtube.com/watch?v=hEXwOkyYNL0

## Oficial Link
```
https://en.comfast.com.cn/index.php?m=content&c=index&a=show&catid=30&id=429
```

## Specification

```
COMFAST CF-WU785AC MT7612UN 1300Mbps Wireless Wifi Adapter
 
1. External 4*6dBi high-gain antennas provides better wireless penetration even in complex wireless environments such as multi-blocking or multi-interference.
2. Transmission rate upto 1300Mbps(5GHz: 867 Mbps, 2.4GHz:400Mbps), which greatly improves the overall wireless performance, faster speeds, and more enjoyable network enjoyment.
```

## Install wireless-adapter

* https://mirror2.openwrt.org/sources/compat-wireless-2010-06-28.tar.bz2
```
bzip2 -dfv compat-wireless-2010-06-28.tar.bz2
tar -xf compat-wireless-2010-06-28.tar
cd compat-wireless-2010-06-28
make load 
```

## Alternative
```
sudo apt update
sudo apt install firmware-misc-nonfree
sudo modprobe mt76x2u

```

## Building

```
┌──(root㉿kali)-[/opt/DPO]
└─# make -C os/linux/

┌──(root㉿kali)-[/opt/DPO]
└─# make 

┌──(root㉿kali)-[/opt/DPO]
└─# sudo apt update
sudo apt install firmware-misc-nonfree
sudo modprobe mt76x2u


┌──(root㉿kali)-[/opt/DPO]
└─# sudo apt update
sudo apt install firmware-misc-nonfree
sudo modprobe mt76x2u


######## Alternative

git clone https://github.com/ulli-kroll/mt7612u.git
cd mt7612u
make
sudo make install
sudo modprobe mt7612u
```

```
apt-get update && apt-get upgrade -y
apt-get dist-upgrade -y
reboot now
sudo apt-get install linux-headers-amd64 build-essential make git dkms bc
sudo apt install -y linux-headers-6.12.38+kali-amd64
sudo apt install -y build-essential dkms git


cd /usr/src
sudo git clone https://github.com/aircrack-ng/rtl8812au.git
cd rtl8812au
sudo make dkms_install
make && make install


sudo update-initramfs -u

sudo modprobe 8812au || sudo modprobe 8814au || true

# Verificar interfaces
ip link show

# Mensagens do kernel relacionadas ao driver
dmesg | grep -i 8812 -A5
dmesg | grep -i rtl -A5


```


## Configuration

```
Ensure usb-modeswitch is installed

$ sudo apt install usb-modeswitch usb-modeswitch-data


Execute usb-modeswitch in a terminal to see if it works

$ sudo usb_modeswitch -K -W -v 0e8d -p 2870


If successful, set it up to run automatically

edit the following file

$ sudo nano  /lib/udev/rules.d/40-usb_modeswitch.rules

below the following line

SUBSYSTEM!="usb", ACTION!="add",, GOTO="modeswitch_rules_end"

add two lines

# COMFAST CF-WU782AC WiFi Dongle, TEROW ROW02FD WiFi Dongle, COMFAST CF-WU785AC WiFi Dongle
ATTR{idVendor}=="0e8d", ATTR{idProduct}=="2870", RUN+="usb_modeswitch '/%k'"

save the file ( Ctrl + x, y, Enter )

create the file /usr/share/usb_modeswitch/0e8d:2870

$ sudo nano /usr/share/usb_modeswitch/0e8d:2870

put the following inside:

# COMFAST CF-WU782AC WiFi Dongle, TEROW ROW02FD WiFi Dongle, COMFAST CF-WU785AC WiFi Dongle
TargetVendor=0x0e8d
TargetProductList="7612"
StandardEject=1

save the file ( Ctrl + x, y, Enter ) and reboot
```


## USB WiFi chipset information for Linux

Updated as of 2025-04-20

This document is a summary that includes information about many modern USB WiFi chipsets. If you see errors in this information, please post in Issues.

Not all USB WiFi adapters are created equally.  While the chipset and driver dictate which WiFi features are supported (e.g. which frequency bands), the maker of the adapter is free to decide on the performance of the antenna(s), the quality of the amp and whether the device requires mode switching and so on.

| Chipset           | Interface | Standard | Maximum<br>Channel<br>Width   | Linux<br>In-Kernel<br>Driver | AP Mode        | Monitor Mode   | Recommended<br>For<br>Linux |
|:------------------:|-----------|----------|:-----:|:----------------------------:|:----------------:|:----------------:|:-----------------:|
Mediatek MT7927   | USB3      | WiFi 7   |  320  | pending       |  |  |  |
Mediatek MT7925   | USB3      | WiFi 7   |  160  |:heavy_check_mark: 6.7+       |:heavy_check_mark:|:heavy_check_mark:| Yes [4] |
Realtek RTL8912au | USB3      | WiFi 7   |  ?    |:x:       |  |  |  |
Realtek RTL8852cu | ?         | WiFi 6E  |  160  |:x: [6]                       |                  |                  | No  |
Realtek RTL8832cu | USB3      | WiFi 6E  |  160  |:x:                           |                  |                  | No  |
Mediatek MT7921au | USB3      | WiFi 6E  |   80  |:heavy_check_mark: 5.18+      |:heavy_check_mark:|:heavy_check_mark:| Yes |
Realtek RTL8852bu | ?         | WiFi 6   |   80  |:x: [6]                       |                  |                  | No  |
Realtek RTL8832bu | USB3      | WiFi 6   |   80  |:x:                           |                  |                  | No  |
Realtek RTL8852au | ?         | WiFi 6   |   80  |:x:                           |                  |                  | No  |
Realtek RTL8832au | USB3      | WiFi 6   |   80  |:x:                           |                  |                  | No  |
Realtek RTL8851bu | ?         | WiFi 6   |   ?   |:x:                           |                  |                  | No  |
Realtek RTL8831bu | USB3      | WiFi 6   |   ?   |:x:                           |                  |                  | No  |
Realtek RTL8814au | USB3      | WiFi 5   |   80  |:heavy_check_mark: 6.16+      |:heavy_check_mark:|:heavy_check_mark:| Yes |
Mediatek MT7662u  | USB2      | WiFi 5   |   80  |:heavy_check_mark: 5.9+ [6]   |:heavy_check_mark:|:heavy_check_mark:| No  |
Mediatek MT7612u  | USB3      | WiFi 5   |   80  |:heavy_check_mark: 4.19+      |:heavy_check_mark:|:heavy_check_mark:| Yes |
Realtek RTL8822bu | USB2      | WiFi 5   |   80  |:heavy_check_mark: 6.12+ [3][6]|:heavy_check_mark:|:heavy_check_mark:| No  |
Realtek RTL8812bu | USB3      | WiFi 5   |   80  |:heavy_check_mark: 6.12+ [3]   |:heavy_check_mark:|:heavy_check_mark:| Yes |
Realtek RTL8822cu | USB2      | WiFi 5   |   80  |:heavy_check_mark: 6.12+ [3][6]|:heavy_check_mark:|:heavy_check_mark:| No  |
Realtek RTL8812cu | USB3      | WiFi 5   |   80  |:heavy_check_mark: 6.12+ [3]|:heavy_check_mark:|:heavy_check_mark:| Yes |
Realtek RTL8812au | USB3      | WiFi 5   |   80  |:heavy_check_mark: 6.14+ [5]|:heavy_check_mark:|:heavy_check_mark:| Yes |
Mediatek MT7610u  | USB2      | WiFi 5   |   80  |:heavy_check_mark: 4.19+      |:heavy_check_mark:|:heavy_check_mark:| Yes |
Realtek RTL8821cu | USB2      | WiFi 5   |   80  |:heavy_check_mark: 6.12+ [3][6]|:heavy_check_mark:|:heavy_check_mark:| No  |
Realtek RTL8811cu | USB2      | WiFi 5   |   80  |:heavy_check_mark: 6.12+ [3]   |:heavy_check_mark:|:heavy_check_mark:| No  |
Realtek RTL8821au | USB2      | WiFi 5   |   80  |:heavy_check_mark: 6.14+ [5]  |:heavy_check_mark:|:heavy_check_mark:| No  |
Realtek RTL8811au | USB2      | WiFi 5   |   80  |:heavy_check_mark: 6.14+ [5]  |:heavy_check_mark:|:heavy_check_mark:| Yes |
Ralink RT3573     | USB2      | WiFi 4   |   40  |:heavy_check_mark: 3.12+      |:heavy_check_mark:|:heavy_check_mark:| Yes |
Ralink RT5572     | USB2      | WiFi 4   |   40  |:heavy_check_mark: 3.10+      |:heavy_check_mark:|:heavy_check_mark:| Yes |
Ralink RT3572     | USB2      | WiFi 4   |   40  |:heavy_check_mark: 2.6.31+    |:heavy_check_mark:|:heavy_check_mark:| Yes |
Ralink RT5372     | USB2      | WiFi 4   |   40  |:heavy_check_mark: 3.0+       |:heavy_check_mark:|:heavy_check_mark:| Yes |
Realtek RTL8192cu | USB2      | WiFi 4   |   40  |:heavy_check_mark: 2.6.33+    |:heavy_check_mark:|:heavy_check_mark:| Yes |
Mediatek MT7601u  | USB2      | WiFi 4   |   40  |:heavy_check_mark: 4.2+       |:x:               | limited          | Yes |
Ralink RT5370     | USB2      | WiFi 4   |   40  |:heavy_check_mark: 3.0+       |:heavy_check_mark:|:heavy_check_mark:| Yes |
Atheros AR9271    | USB2      | WiFi 4   |   40  |:heavy_check_mark: 2.6.35+    |:heavy_check_mark:|:heavy_check_mark:| Yes |
Ralink RT3070     | USB2      | WiFi 4   |   40  |:heavy_check_mark: 2.6.31+    |:heavy_check_mark:|:heavy_check_mark:| Yes |

## Mediatek MT7921AU (in-kernel driver is mt7921u) (WiFi 6E)

Adapters based on the mt7921au chipset have been available since July of 2022.

[1] USB support added with the mt7921u driver in kernel 5.18. Internal cards are supported by the mt7921e driver which has been in the kernel since 5.12.

[2] AP mode support added to the mt7921u driver in kernel 5.19. Firmware update is required also.

-----

## Realtek RTW88 (in-kernel driver) (WiFi 5)

[3] In-kernel support for the following chipsets was added in the rtw88 series of drivers with kernel 6.2, however, it is strongly recommended that you use kernel 6.12 or later due to dramatic improvements to the drivers that have taken place during 2024:

```
rtl8822bu
rtl8812bu
rtl8821cu
rtl8811cu
rtl8822cu
rtl8812cu
```
 
-----

[4] The driver for USB and PCIe went into Linux kernel 6.7. The first available USB WiFi adapter, Netgear A9000, became available in July of 2025

-----

[5] The new in-kernel drivers for the rtl8812au and rtl8821/11au chips are NEW as of kernel 6.14. If you want to install the new drivers on kernels less than 6.14, please go to the following repo:

https://github.com/lwfinger/rtw88

-----

[6] Chipset has bluetooth turned on. Recommend Linux users avoid chipsets with bluetooth turned on.



