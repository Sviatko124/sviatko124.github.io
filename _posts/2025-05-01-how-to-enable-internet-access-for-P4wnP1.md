---
layout: post
date: 2025-05-01
author: Sviatko124
tags: P4wnP1
---
In this tutorial, I will provide step-by-step instructions on how to properly set up DNS resolving and connect your P4wnP1 to the Internet. 
Due to what this method does, the device's WIFI AP will go down, so it is necessary that you have a data cable so that you can connect to the P4wnP1 through SSH. 
Note: I am using NightRang3r's P4wnP1 image (https://github.com/NightRang3r/P4wnP1-A.L.O.A.-Payloads), but the following steps should be the same for the regular P4wnP1 A.L.O.A. as well. 
Note: I'm new to P4wnP1, and the following tutorial was compiled with the help of hours of searching the web. Eventually, I just found what worked for me, but don't think that the following is the only solution. 

## Set wlan0 to managed mode
This step is important because currently, wlan0 is responsible for handling its WIFI network. However, this is the only wireless interface that can be used to connect to the internet, so we need to change it into managed mode. 
To do that, run the following:

`sudo ifconfig wlan0 down`

`sudo iwconfig wlan0 mode managed`

`sudo ifconfig wlan0 up`


Now, you can run the `iwconfig` command, and you will see that wlan0 is now in managed mode, but is not associated to any WIFI network. 


# Set up DNS
### Edit resolv.conf
Open /etc/resolv.conf:

`sudo nano /etc/resolv.conf`

Then, write the following into the file:

```
domain home
nameserver 8.8.8.8
nameserver 8.8.4.4
```


### Edit dhcpcd.conf
Open /etc/dhcpcd.conf:

`sudo nano /etc/dhcpcd.conf`

Write the following at the end of the file:

```
interface wlan0
static domain_name_servers=8.8.8.8 8.8.4.4
```

To make sure that the dhcpcd service doesn't overwrite this, run the following command to make the file immutable:

`sudo chattr +i /etc/resolv.conf`


Then, restart dhcpcd:

`sudo systemctl restart dhcpcd`


If for any reason you need to make changes to the file, run the following command to be able to modify the file again:

`sudo chattr -i /etc/resolv.conf`



## Connect to WIFI

Now you can begin connecting to a WIFI network. For this, you will need a wireless network to connect to, as you will use the network name and password in the following steps. 
First, create a file in /etc/wpa_supplicant/ called wpa_supplicant.conf

`sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`

Write the following into the file:


```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US
network={
  ssid="<WIFI name>"
  psk="<WIFI password>"
  key_mgmt=WPA-PSK
}
```
Then, just run the following command, and you should be able to get a network connection:

`wpa_supplicant -Dnl80211 -iwlan0 -c/etc/wpa_supplicant/wpa_supplicant.conf`

If you want to be able to use the same terminal while connected to the internet, run the following command, which is just the previous one except it suppresses all output:

`nohup wpa_supplicant -Dnl80211 -iwlan0 -c/etc/wpa_supplicant/wpa_supplicant.conf &`


I hope that helped, and have a good day!
