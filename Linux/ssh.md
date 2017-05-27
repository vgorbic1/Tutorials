## Secure Shell
Unlike `telnet` all `ssh` traffic is encrypted. To login to another machine use it's IP (or domain name) and a username on that machine:
```
ssh username@122.122.122.122
```
If you are connecting to this machine  for the first time, the following may come up:
```
The authenticity of host '192.168.0.25 (192.168.0.25)' can't be established.
RSA key fingerprint is 54:53:c3:1c:9a:07:22:0c:82:7b:38:53:21:23:ce:53.
Are you sure you want to continue connecting (yes/no)?
```
It tells you that it cannot recognize this machine, and it is asking you to verify the machine's identity. Press `yes`. Your 
machine will add this RSA kiey fingerprint to the list of known host in `~/.ssh/known_hosts. The host record in this file
may be hashed (encrypted).

### Securely Login to Another Machine without a Password
1. Create a SSH authentication key pair on the local machine:
```
ssh-keygen
```
You currently have three choices for the type of key you create using `-t`:
- dsa (Digital Signature Algorithm), which is now deprecated by OpenSSH due to security issues, so don’t use that.
- rsa (named for the surnames of its creators), which is widely-supported and
quite secure, provided you use at least 2048 bits for the key length (the number after -t). If
you’re really paranoid, go for 3072 or even 4096—just be aware that the longer the key length,
the longer it takes to encrypt and decrypt.
- ecdsa (Elliptic Curve Digital Signature Algorithm) isn’t widely supported yet, so
you might want to hold off using that just yet. 

The public key by default is stored at `~/.ssh/id_rsa` and a public key at `~/.ssh/id_rsa.pub`.

2. Transfer the public key to the remote machine:
```
ssh-copy-id -i ~/.ssh/id_rsa.pub username@122.122.122.122
```
3. Check that the public key on the remote machine was copied successfully. Loggin to it as usual:
```
ssh username@122.122.122.122
```
Now no password is needed.

### Secure File Transfer
Unlike `ftp` all `sftp` traffic is encripted. The `sftp` uses SSH to encrypt everything. If you can ssh to a machine
you also can sftp to it.
```
sftp username@122.122.122.122
```
Use the following commands after that:

Command | Meaning
-- | --
cd | change directory
exit | close the connection
get | copy the specified file to the local machine
help | get help on commands
lcd | change the directory on the local machine
lls | list fiels on the local machine
ls | list files on the remote machine
put | copy the specified file to the remote machine
rm | remove the specified file from the remote machine

If the SSH server to which you're connecting via sftp has changed the default port (22), then
you’re not going to be able to connect. To use the non-default SSH port (or to work with any
other special changes to SSH the server admin has made), you pass that option along in your
sftp command with `-o`, followed by the specific SSH option. So, for instance, if the SSH
server uses port 2345 instead of 22, you would connect using:
```
sftp -oPort=2345 
```
(notice there is no space after `-o` and the SSH option). If you have to include additional SSH options,
just repeat the `-o,` like this:
```
sftp -oPort=2345 -oPasswordAuthentication=no
```
### Secure File Copy
To secure copy files from one machine to another:
```
scp ~/filename username@122.122.122.122:filename
```
To secure copy many files:
```
scp *.jpg username@122.122.122.122:/home/username/images
```
To secure copy files from the remote directory to local machine:
```
scp username@122.122.122.122:/home/dir* ~/images
```
### Secure File Transfer and Backup
