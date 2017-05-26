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




