## Networking
Testing, measuring, and managing your networking devices and connections.
To get a quick look at all of your running network devices use *interface configuration*:
```
ifconfig
ifconfig -a  // to see even those that aren't currently running
```
- `ath0` - is a wireless card
- `lo` - is the loopback interface, which enables a machine to refer to itself. The loopback address is always represented by the IP address of 127.0.0.1.
