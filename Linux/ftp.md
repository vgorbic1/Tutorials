## FTP Security
One of the concerns is an anonymous access. A user must only list, download and upload files to a single "incoming" directory. Login credentials must be protected from disclosure too. Unfortunately, FTP is designed to transmit both authentication credentials and session data in clear text. Good FTP is anonymous FTP. Otherwise, use rsync, scp, and sftp.

#### ACTIVE / PASSIVE MODE FTP
FTP servers listen on port 21.  By default, whenever an FTP client wishes to download a file or directory listing, the FTP server initiates a new connection back to the client using an arbitrary high TCP port. This new connection is used for transmitting data, as opposed to the FTP commands and messages carried over the control connection. FTP with server-initiated data channels is called active mode FTP.
The only widely supported alternative to active mode FTP is passive mode FTP, in which the client rather than the server opens data connections. Passive FTP still uses separate connection to random high port.

#### FTPS
The FTPS protocol adds SSL (TLS) encryption to the FTP protocol, adding both encryption and, optionally, certificate-based authentication to FTP.
