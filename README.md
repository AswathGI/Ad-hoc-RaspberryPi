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
