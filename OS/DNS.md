## Domain Name System (Domain Name Service)

Domain Names:
```
.com  .net
```
Host names:
```
(your computer name)  JACK-ASUS
```
Hosts are any stations  in network. They all have ```Host name``` and ```IP address```.

To get all information about the host:
```
ipconfig /all
```
Connect with DNS server and get IP address of the URL provided:
```
ping www.yahoo.com
```
To perform host lookup (Windows) check the file:
```
c:/Windows/System32/Drivers/etc/hosts
```

####DNS Levels
- **Root Server** "." (dot) knows where
- **Top Level Domain** aka TLD (.com .net .org) server knows where
- **Domain Servers** (Yahoo Google)

**Fully Qualified Domain Name** (FQDN) is anything with the dot at the end, representing the root server and showing all levels of DNS:
```
vwp-rt.wptech.com.
```
If you cannot resolve a URL without WWW, it is DNS misconfiguration. The DNS config needs one more record.

###DNS Records
- A Record name to IP address
- NS Record (Name Service)  identify the DNS servers responsible (authoritative) for a zone. These NS-records have the same name as the zone in which they are located.
- MX (Male Record) has IP address of your mail server.
- CNAME (Canonical Name) are domain name aliases. The most common use of the CNAME-record type is to provide access to a web-server using both the standard "www.domain.com" and "domain.com" (with and without the www prefix).
This is usually done by creating an A-record for the short name (without www), and a CNAME-record for the www name pointing to the short name.

12 Root operators (nonprofit organizations) are responsible for working all this DNS system. Particularly:
- ICANN (top level) - administrative role
- IANA (middle level) - responsible for the root zone file "."
- others (including VeriSign, NASA, US Army Research Lab) maintain root servers.
