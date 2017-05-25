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



