## Kali Linux
### Information Gathering and Reconnaissance
#### Use Recon-NG Framework:
```
> recon-ng
> show modules
> use module-name
```
#### Use Dmitry
```
> dmitry -s site.com
```
#### Use Netdiscover to find IPs and open ports on LAN

#### Use Nmap
```
> nmap -v -A site.com
```
Find open ports:
```
> nmap -r -v 192.168.1.5
```
Find what services are running on open ports:
```
> nmap -sS -Pn -A 192.168.1.5
```
