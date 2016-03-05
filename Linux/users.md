## User Operations

**Change file owner**
```
sudo chown <new-username> <file-to-change>
```
**Change directory owner including all files in the directory**
```
sudo chown -R <new-username> <directory-to-change>
```
**Append a user to an existing group**
```
sudo usermod -a -G <group-name> <username>
```
**Check what groups the user belongs to**
```
groups <username>
 or
id <username>
```
