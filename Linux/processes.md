## Processes Management
To check what is currently running providing realtime view of the system:
```
top
```
To see processes for a particular user:
```
top -u username
```
When the top table is displayed use these shortcuts:
- shift + n sorts by PID
- shift + p sorts by CPU usage
- shift + m sorts by memory usage

To see processes in teminal:
```
ps
```
To see processes in system:
```
ps aux
```
To see a particular user processes:
```
ps -u username
```
To see every running process for all users:
```
ps -e
```
To see a tree view of processes:
```
pstree
```

#### Monitoring Memory Use
To list memory usage in megabytes:
```
free -m
```
To see memory usage over a given time period:
```
vmstat 3 
```
3 means 30 seconds. Exit with ctrl+c

To display a Kernel slab (memory cash):
```
sudo slabtop
```

#### Monitoring  CPU
Install ```iostat```.
```
sudo apt-git install sysstat
```
To see the use of CPU (every 3 seconds):
```
iostat -c 3
```
To see information about the processor:
```
cat /proc/cpuinfo
```

#### Killing a Crashed Process
- Undentify the process id: ``` ps aux | grep 'firefox'``` Say it was 2620
- Use kill command: ```kill 2620```
- If it did not work, kill it with -9 flag: ```kill -9 2620```
To see who is logged in:
```
w
```
To see info about a user named tom:
```
w tom
```
To see all users:
```
users
```
To see how long the computer was running:
```
uptime
```
To see all information about the system:
```
uname -a
```
