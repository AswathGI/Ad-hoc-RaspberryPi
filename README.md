# Ad-hoc-RaspberryPi

## Update the RPi
```shell
$ sudo apt-get update
$ sudo apt-get upgrade
```

## WLan ip_addresss
### Check the WLan ip_address that is connected to the RPi

```shell
$ ifconfig
```

<img src="https://github.com/AswathGI/Ad-hoc-RaspberryPi/blob/master/Screenshot%202020-06-22%20at%2015.04.02.png">

#### In my case WiFi ip_address is set to 
> 100.89.173.31

here the subnet of your ip_address is "100.89.173"

#### And the WiFi port name is 
> wlan0

Remember these. 

## Configure Network Interface

### Go to network setting Directory
```shell
$ cd /etc/network/
```
#### Then type check the list of files available
```shell
$ ls
```
#### You should find a file name called 
> interfaces

We have to edit this file now. 

#### Go to editing mode by typing in:
```shell
$ sudo nano interfaces
```
### You should see something like this
<img src="https://github.com/AswathGI/Ad-hoc-RaspberryPi/blob/master/Screenshot%202020-06-22%20at%2015.17.26.png">

#### Now add the following lines into this file: 
```shell
auto lo
iface lo inet loopback

iface eth0 inet manual

auto wlan0
iface wlan0 inet static
 address 100.89.170.51
 netmask 255.255.255.0
 wireless-channel 1
 wireless-essid Raspberry Pi
 wireless-mode ad-hoc
```

##### Makes changes to these following according to your wish
> address 100.89.170.51

First change the subnet. 
Note: Here I have entered " 100.89.170 " which is different from my original WiFi router subnet (100.89.173) that we checked ealier. Please make sure that these subnets are different from you original router. In the finall line I have given 51, you can use any number from 00 - 999. Finall remember this address. 

> wireless-essid Raspberry Pi

This will be your SSID of this Ad-Hoc network. You can change "Raspberry Pi" to any name here. And that will be set as your SSID. 

#### Finally keep the rest as same as it is, Save the file and Exit. 


## Creating DHCP Server
#### While being there in the /etc/network/ directory install DHCP server package by typing in: 
```shell
$ sudo apt-get install dhcp-server
```

