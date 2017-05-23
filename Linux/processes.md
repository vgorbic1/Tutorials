## Processes Management

To see how long the computer was running:
```
uptime
```
To see all information about the system:
```
uname -a
```
To check what is currently running providing realtime view of the system:
```
top
  // or 
htop  // not all systems have it. 
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
STAT:
- R - runnting
- S - sleeping
- T - stopped 
- Z - zombie (not good)

To see all and every processes in system:
```
ps aux
```
To see all processes without cropping the view:
```
ps aux -w
```
To see a particular user processes:
```
ps U username
```
To see every running process for all users:
```
ps -e
```
To find a particular process or program:
```
ps aux | grep [f]irefox
```
To see a tree view of processes:
```
ps axjf
 // or
pstree  // not all systems have it
```
#### Ending the Runnig Process
To end process and give the program a chance to shut down any other programs depending upon it, close files
opened by it, and so on:
```
kill processid
```
To end a stuborn process that is still running after the previous option:
```
kill -9
```
To kill all commands with the same name:
```
killall commandname
```
Algorithm:
- Undentify the process id: ``` ps aux | grep 'firefox'``` Say it was 2620
- Use kill command: ```kill 2620```
- If it did not work, kill it with -9 flag: ```kill -9 2620```

#### Monitoring Memory Use
To list memory usage in megabytes:
```
free -m
```
To see memory usage over a given time period:
```
vmstat 3 
```
where 3 means 30 seconds. Exit with `ctrl+c`

To display a Kernel slab (memory cash):
```
sudo slabtop
```
#### Monitoring System Disk Usage
To see the disk usage:
```
df
```
The `df` command shows results in kilobytes by default, but it’s usually easier to comprehend if you instead
use the `-h` option:
```
df -h
```
To see how much space the current directory uses:
```
du -hs
```
To see how much space the current directory and all subdirectories separately use:
```
du -h
```
#### Monitoring CPU
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
