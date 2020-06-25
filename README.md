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
auto wlan0
iface wlan0 inet static
 address 100.89.170.51
 netmask 255.255.255.0
 wireless-channel 1
 wireless-essid Raspberry Pi
 wireless-mode ad-hoc
```

#### Makes changes to these following, according to your wish

##### Replace wlan0 to your WiFi port name in the following lines: 
> auto wlan0

> iface wlan0 inet static

This sets your WiFi address to be Static

##### Next change the subnet. 

> address 100.89.170.51


Note: Here I have entered " 100.89.170 " which is different from my original WiFi router subnet (100.89.173) that we checked ealier. Please make sure that these subnets are different from you original router. In the finall line I have given 51, you can use any number from 00 - 999. Finall remember this address. 

##### Replace SSID
> wireless-essid Raspberry Pi

This will be your SSID of this Ad-Hoc network. You can change "Raspberry Pi" to any name here. And that will be set as your SSID. 

#### Finally keep the rest as same as it is, Save the file and Exit. 


## Creating DHCP Server
#### While being there in the /etc/network/ directory install DHCP server package by typing in: 
```shell
$ sudo apt-get install isc-dhcp-server
```

Once this is installed, we need to change few setting in the following files. 

### Make changes in isc-dhcp-server file

Open isc-dhcp-server file by typing in: 
```shell
$ sudo nano /etc/default/isc-dhcp-server
```

##### isc-dhcp-server file
<img src="https://github.com/AswathGI/Ad-hoc-RaspberryPi/blob/master/Screenshot%202020-06-22%20at%2015.28.40.png" >

Inside this file, you should see something like this. 
Here, Enter the WiFi port name in any of these interfaces. 
I have used interfaces v4 as my interface and it looks like this: 
> INTERFACESv4="wlan0"

#### Finally, Save and Exit.

### Next, make changes in dhcpd.conf file

Enter into the file by typing this command: 
```shell
$ sudo nano /etc/dhcp/dhcpd.conf
```
##### The file should look something like this. 
<img src="https://github.com/AswathGI/Ad-hoc-RaspberryPi/blob/master/Screenshot%202020-06-25%20at%2001.06.30.png" >

#### Now, you have to make few changes.
##### Set Domain name
> option domain-name "example.org";

This is completely an optional step. If you don't have any domain name to be set, you can skip this step, but follow from the next step.
If you have a Domain name, replace "example.org" with your domain name. 

##### Set the Domain-name Server
Type this line below the Domain name.
> option domain-name-servers 8.8.8.8

I'm setting my server as "8.8.8.8" if you have set a server already, you can use that name here, else follow the same.

##### Authenticate


