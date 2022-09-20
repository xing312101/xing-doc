# Linux

## virtualbox shared folder permission
```
sudo usermod -aG vboxsf $USER
```

## version
```
lsb_release -a
uname -a
cat /etc/issue
cat /etc/lsb-release
cat /proc/version

cat /etc/redhat-release # Redhat only
rpm -q redhat-release # Redhat only

uname -m 查32bit或64bit
getconf LONG_BIT 查32bit或64bit
```

## Reset Ubuntu Root Password in recovery mode
```
1. Go to recovery mode
2. Select “root Drop to root shell prompt”
3. Remount the root with write access
   # mount -rw -o remount /
4. Reset username or password
   # ls /home
   # passed username
```


