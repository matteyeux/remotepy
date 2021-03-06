# remotepy

Simple tool I use, to replace PuTTY for command line stuff.
```
usage : ./remotepy [args]
 -a, --add <device|username|ip|port>    add device to list
 -c, --connect [device]                 connect to device
 -d, --delete [device]                  delete device from list
 -l, --list                             list devices
```

### add device
To add a device you have to use `-a` argument with few params :
```bash
               name     username  IP/domain   port
                 |        |           |        |
$ remotepy -a device1 matteyeux 17.142.160.59 2222
$ remotepy -a device2 matteyeux google.com 22
```
Settings are set in an SQLite3 database named `.remotepy.db`. It should be located your in Home directory for both UNIX and Windows OS's

### list devices
You can list devices you added with `-l` arg
```bash
$ remotepy -l
===============
name	: device1
user	: matteyeux
ip	: apple.com
port	: 2222
===============
name	: device2
user	: matteyeux
ip	: 216.58.213.174
port	: 22
===============
```

Optionally if fping is installed on your machine, it will check the status of the host like this : 
```bash
$ remotepy -l
===============
name	: device1
user	: matteyeux
ip	: apple.com
port	: 2222
status  : down   <----
===============
name	: device2
user	: matteyeux
ip	: 216.58.213.174
port	: 22
status  : up     <----
===============
```
You can also list one device by giving it's name after `-l`. <br>

### update device settings

Use `-u` argument to update your device : `remotepy -u device1 port 22` 

To verify changes, list device info :

```
$ remotepy -l device1
===============
name	: device1
user	: matteyeux
ip	: apple.com
port	: 22
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

### ZSH autocompletion
Put this in `~/.zshrc`
```
_remotepy() {
  local cachedir="${XDG_CACHE_HOME:-$HOME/.cache}/remotepy"
  local hostnames="${cachedir}"/remotepy.txt
  mkdir -p "${cachedir}"
  if ! test "$(find "${hostnames}" -mmin -15 2>/dev/null)"; then
    echo "select device from devices;" | sqlite3 ~/.remotepy.db > "${hostnames}".new
    if test -s "${hostnames}".new; then
      mv "${hostnames}"{.new,}
    else
      touch "${hostnames}"
    fi
  fi
  compadd $(cat "${hostnames}")
}
compdef _remotepy remotepy
```

### TODO
- [X] Windows support
- [X] Switch to sqlite3
- [X] Add a feature to remove a device (should go with SQLite3)
- [X] update device settings
- [X] host status
- [ ] (maybe) implement a PuTTY like GUI

Btw let me know if you can pwn those 2 IPs in the list.

~matteyeux
