## Networking
Testing, measuring, and managing your networking devices and connections.
To get a quick look at all of your running network devices use *interface configuration*:
```
ifconfig
ifconfig -a  // to see even those that aren't currently running
```
- `ath0` - is a wireless card that is just Ethernet interface with some extra wireless goodies.
- `lo` - is the loopback interface, which enables a machine to refer to itself. The loopback address is always represented by the IP address of 127.0.0.1.
- `eth0` - is an Ethernet card, which is not activated if no cables are plugged into it.

To get a quick look at all running devices with newer command `ip`:
```
ip addr show up
```
To verify that a computer is running and accepting requests:
```
ping
```
Press `Ctrl+C` to stop. A successful `ping` means that network connectivity is occurring between the two machines.

To send `ping` with a limited number of packages:
```
ping -c 3
```
To show every step taken on the route from your machine to a specified host:
```
traceroute www.google.com
```
To combine `ping` and `traceroute` commands, use `mtr` if it is installed on the system.

To quickly find the IP address associated with a domain name:
```
host google.com
```
To find out a domain name associated with an IP (reverse DNSlookup):
```
host 65.12.232.12 
```
To find more information about the IP or domain:
```
dig www.google.com any
```
### Configuring a Network Interface
To change the IP address for the Ethernet card found at `eth0` to 192.168.0.125:
```
ifconfig eth0 192.168.0.125
  // or
ip addr add 192.168.0.125 dev eth0
```
By default, `eth0` only listens for packets sent specifically to it, but in order to sniff all the packets flowing by on a
network, you need to tell your card to listen to everything, which is known as *promiscuous mode*:
```
ifconfig eth0 promisc
ifpromisc eth0 // to shut down the promisc
```
To view the status of wireless network interface:
```
iwconfig
```
To display IP routing table:
```
route
```
Example:
```
Kernel IP routing table
Destination Gateway Genmask Flags Metric Ref Use Iface
192.168.0.0 * 255.255.255.0 U 0 0 0 eth0
default 192.168.0.1 0.0.0.0 UG 0 0 0 eth0
```
An IP address is composed of four octets, giving it the appearance of xxx.xxx.xxx.xxx, as in
192.168.0.124. When you send a packet out of your machine, the IP address that is the destination of
that packet is compared to the Destination column in the routing table. The Genmask column works
with the Destination column to indicate which of the four octets should be examined to determine the
packet’s destination.

For example, let’s say you enter ping 192.168.0.124 in your shell. A Genmask of
255.255.255.0 indicates that only the last octet—the number represented by 0—matters. In other
words, when looking at 192.168.0.124, only the .124 is important to route packets to that address.
Any packets intended for 192.168.0.1 through 192.168.0.255 (the limits of an IP address) match the
Genmask and the Destination, so they stay on the Local Area Network and avoid the router. That’s
why there’s an * in the Gateway column next to 192.168.0.0: No Gateway is needed because that
traffic is local.

On the other hand, everything else is by default intended for the router, which in this instance is at
192.168.0.1 in the Gateway column. The Genmask in this row is 0.0.0.0, indicating that any IP
address not matching 192.168.0.1 through 192.168.0.255 should be sent through 192.168.0.1 (because
192.168.0.1 is the Gateway, it’s a special case). 72.14.203.99, 82.211.81.166, and 216.23.180.5 all
match with 0.0.0.0, so they must all go through the Gateway for the Net.

###Troubleshooting Network Problems
Linux distributions nowadays usually “just work” when it comes to networking, but you might still
experience an issue. Following are some basic tips for troubleshooting network problems, based on
what I’ve covered in this chapter.

If your network interface appears to be up and running, but you can’t get on the Internet, first try
pinging your localhost device, at 127.0.0.1. If that doesn’t work, stop and go no further, because you
have a seriously damaged system. If that works, ping your machine’s external IP address. If that
doesn’t work, make sure networking is enabled on your machine. If it does work, now try pinging
other machines on your network, assuming you have any. If you’re not successful, it’s your interface
(assuming your router is okay). Make sure that your cables are plugged in (seriously). Use
ifconfig or ip addr show if it’s wired, or iwconfig or nmcli -p device status if
it’s wireless, to verify the status of your interface and use ifup or ip link set eth0 up to
turn the interface on, if necessary. Then try ping again.

If your attempt to ping another local computer was successful, next try pinging your router. If you
can’t get to a router and you’re pinging it using its IP address, I would reboot your router and see if
that fixes it. If you can get to other machines on your network, but you can’t get to your router, time to
check your routing tables with route or ip route show (refer to “Display Your IP Routing
Table”). If you’re missing items from your routing table, add them, as detailed in “Change Your IP
Routing Table.”

It’s much easier to diagnose and fix problems if you have a baseline from which to work. After
you know a machine’s networking is correct, run route and save the results, so you have a
stored blueprint if the routing table goes bonkers and you need to restore something later.

If you can get to your router, try pinging a machine you know will be up and running out on the
Internet, like www.google.com or www.ubuntu.com. If that doesn’t work, try pinging that same
machine’s IP address. Yes, that means that you need to have some IP addresses on a sticky note or in
a text file on your computer for just such an occasion as this. Here are a few that are good right now;
of course, they could change, so you really should look these up yourself.

How do you get those IP addresses? You can ping the machine using its domain name, and
ping gives you the IP address, or you can get the same info with traceroute. A quicker
method is with the host or dig commands, covered earlier in “Query DNS Records.”

If you can get to the IP address but can’t get to the domain name, you have a DNS problem. If you’re
using DHCP, it’s time to run dhclient (refer to “Grab a New Address Using DHCP”) to try to
renew the DNS information provided by your DHCP server. If you’re not using DHCP, find the DNS
information you need by looking on your router or asking your administrator or ISP, and then add it
manually as root to `/etc/resolv.conf` so that it looks like this, for example:
```
nameserver 24.217.0.5
nameserver 24.217.0.55
```
That’s nameserver (a required word), followed by an IP address you’re supposed to use for the
DNS. If your router can handle it, and you know its IP address (192.168.0.1, let’s say), you can
always try this first:
```
nameserver 192.168.0.1
```
Try ifdown and then ifup and see if you’re good to go. At this point, I need to point out a problem
that reader Brian Greer brought to my attention: “When manually adding a nameserver to
/etc/resolv.conf, it is only a temporary solution since dhclient overwrites this file on
release or reboot.” Thank you, Brian—you are completely correct! If you want your DNS changes to
persist across DHCP releases and reboots, you need to follow these steps.

First, start by backing up your current resolv.conf in case anything goes bump.
```
$ sudo cp /etc/resolv.conf /etc/resolv.conf.auto
```
Now you need to edit your dhclient.conf file, but first you have to find it, as the location of the
file depends upon your distro. (On Ubuntu 14.04 box, it’s at /etc/dhcp/dhclient.conf.)
If you can’t easily find it, you can always use the find command from Chapter 11, “The find
Command”:
```
$ sudo find /etc -name dhclient.conf
```
Once you’ve found `dhclient.conf`, edit it with your favorite editor, but be sure you open the
editor using sudo, or with the ability to authenticate when you point it at dhclient.conf,
because you need root privileges to edit that file. When it’s open, add the following line to the
document before the return subnet-mask line—and note the semicolon at the end!
```
prepend domain-name-servers 208.67.222.222, 208.67.220.220;
```
Save and exit `dhclient.conf`. Bring down the connection and then bring it up again, and then
check to make sure your DNS is in place with 
```
cat /etc/resolv.conf
```
Instructions for SUSE, Mint, and Cinnamon users can be found at
https://support.opendns.com/forums/21618384-Computer-Configuration.

If you’re still having problems, time to begin again, starting always with hardware. Is everything
seated correctly? Is everything plugged in? After you’re sure of that, start checking your software. The
worst-case scenario is that your hardware just doesn’t have drivers to work with Linux. It’s rare, and
growing rarer all the time, but it still happens.

Wireless cards, however, can be wildly incompatible with Linux thanks to close-mouthed
manufacturers who don’t want to help Linux developers make their hardware work. To prevent
headaches, it’s a good idea to check online to make sure a wireless card you’re thinking about
purchasing will be copasetic with Linux. Good sites to review include Linux Wireless LAN Support
(http://linux-wless.passys.nl) and the Ubuntu Wiki’s WirelessCardsSupported page
(https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported).

Oh, and to finish our troubleshooting: If you can successfully ping both the IP address and the domain
name, stop reading this—you’re online! Go have fun!
