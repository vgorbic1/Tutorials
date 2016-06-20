## Processes Management
To check what is currently running providing realtime view of the system:
```
top
```
To see processes in teminal:
```
ps
```
To see processes in system:
```
ps aux
```
#### Killing a Crashed Process
- Undentify the process id: ``` ps aux | grep 'firefox'``` Say it was 2620
- Use kill command: ```kill 2620```
- If it did not work, kill it with -9 flag: ```kill -9 2620```
