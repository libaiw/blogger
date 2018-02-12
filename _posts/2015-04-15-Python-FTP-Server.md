---
title: Simple Python to build FTP Server
---

### First, how to use one line of Python code to achieve FTP server

This is especially useful when you want to quickly share a directory, just one line of code.

FTP server, before I use the Linux vsftpd package to build FTP server, and now found that the use of pyftpdlib can be an easier way to achieve FTP server functions.

Environmental requirements

Python 
Windows / Linux
Environment to build

---
pip install pyftpdlib


One line of code to achieve FTP server

This is especially useful when you want to quickly share a directory with Python's -m option to run as a simple standalone server.

In the need to share the directory to execute the following command to share the current directory (anonymous login)

python -m pyftpdlib

At this point a simple FTP server has been built to complete, visit ftp://127.0.0.1:2121 (default IP 127.0.0.1, port 2121)



Renderings

Optional parameters

i specify the IP address (default is the machine's IP address)
p Designated port (default is 2121)
w write permission (default is read-only)
d designated directory (the default is the current directory)
u specify the user name login
P Set the login password
Simple example

The above command can already implement a simple FTP server, but to build a powerful and complete FTP service involves more configurations. In this case, you need to use the API provided by Pyftpdlib to write it. The following is a simple example

from
 pyftpdlib.authorizers
import
 
DummyAuthorizer
from
 pyftpdlib.handlers
import
 
FTPHandler
from
 pyftpdlib.servers
import
 
FTPServer
### Instantiate the DummyAuthorizer to create ftp users
authorizer =
DummyAuthorizer
()
### Parameters: user name, password, directory, permissions
authorizer.add_user (
'user'
,
'12345'
,
'/ opt / pyftp / test'
, perm =
'elradfmwMT'
)
### Anonymous login
### authorizer.add_anonymous ('/ home / nobody')
handler =
FTPHandler
handler.authorizer = authorizer
### Parameters: IP, port, handler
server =
FTPServer
((
'192.168.56.100'
,
twenty one
), handler)
server.serve_forever ()
perm permission options

Read permission:

"e" = change directory (CWD, CDUP command)
"l" = list file (LIST, NLST, STAT, MLSD, MLST, SIZE command)
"r" = retrieve file from server (RETR command)
Write permission:

"a" = Append data to existing file (APPE command)
"d" = delete file or directory (DELE, RMD command)
"f" = rename file or directory (RNFR, RNTO command)
"m" = create directory (MKD command)
"w" = Stores the file to the server (STOR, STOU command)
"M" = change file mode / permissions (SITE CHMOD command)
"T" = change file modification time (SITE MFMT command)

reference

Pyftpdlib Documentation:

http:
//pyftpdlib.readthedocs.io/en/latest/index.html
