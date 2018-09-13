# remotepy

Simple tool I use, to replace PuTTY for command line interface stuff.
```
usage : remotepy [args]
 -a, --add <device|username|ip|port>	add device to list
 -c, --connect [device]			connect to device
 -l, --list				list devices
```

### add device
To add a device you have to use `-a` argument with few params :
```bash
               name     username      IP     port
                 |        |           |       |
$ remotepy -a device1 matteyeux 17.142.160.59 22
$ remotepy -a device2 matteyeux 216.58.213.174 2222
```
Settings are set in an XML file in your Home directory. 

File is `.remotepy.xml`.

### list devices
You can list devices you added with `-l` arg
```
remotepy -l
===============
name	: device1
user	: matteyeux
ip	: 17.142.160.59
port	: 22
===============
name	: device2
user	: matteyeux
ip	: 216.58.213.174
port	: 2222
===============
```

### connect to device
To connect to a device, simply run remotepy with `-c` argument and the name of the device to connect to

```
$ remotepy -c device1
connect to device : device1
mathieu@17.142.160.59's password: 
Welcome to Ubuntu 18.04.1 LTS (GNU/Linux 4.10.0-37-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

Last login: Sun May 13 01:28:36 2018 from 216.58.213.174
➜  ~ 
```

### TODO
- Add a feature to remove a device
- Switch to sqlite3
- tkinter

Btw let me know if you can pwn those 2 IPs in the list.

~matteyeux
