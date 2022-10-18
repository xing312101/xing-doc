# network
```
ifconfig
netstat -an
```


# find host name
```
lookup ifconfig and see en0

$ nslookup 9.197.176.53
```

# nmblookup
> https://helloworld.pixnet.net/blog/post/46310280-%E5%9C%A8freebsd-linux-%E4%B8%8B%E7%94%B1ip-%E6%9F%A5%E8%A9%A2%E5%8D%80%E7%B6%B2%E5%85%A7%E7%9A%84%E4%B8%BB%E6%A9%9F%E5%90%8D%E7%A8%B1

```
$ nmblookup -A 192.168.1.102
```

### install samba
```
$ cd /usr/ports/net/samba47
$ make install clean
```

### help
```
# nmblookup --help
Usage: <NODE> ...
  -B, --broadcast=BROADCAST-ADDRESS      Specify address to use for broadcasts
  -f, --flags                            List the NMB flags returned
  -U, --unicast=STRING                   Specify address to use for unicast
  -M, --master-browser                   Search for a master browser
  -R, --recursion                        Set recursion desired in package
  -S, --status                           Lookup node status as well
  -T, --translate                        Translate IP addresses into names
  -r, --root-port                        Use root port 137 (Win95 only replies to this)
  -A, --lookup-by-ip                     Do a node status on <name> as an IP Address

Help options:
  -?, --help                             Show this help message
      --usage                            Display brief usage message

Common samba options:
  -d, --debuglevel=DEBUGLEVEL            Set debug level
  -s, --configfile=CONFIGFILE            Use alternate configuration file
  -l, --log-basename=LOGFILEBASE         Base name for log files
  -V, --version                          Print version
      --option=name=value                Set smb.conf option from command line

Connection options:
  -O, --socket-options=SOCKETOPTIONS     socket options to use
  -n, --netbiosname=NETBIOSNAME          Primary netbios name
  -W, --workgroup=WORKGROUP              Set the workgroup name
  -i, --scope=SCOPE                      Use this Netbios scope
```

