# mount disk
```
mkfs.ext4 /dev/xvdXXXXX
mkdir /diskname
chown -R ubuntu:ubuntu /diskname
mount /dev/xvdXXXXX /diskname
vim /etc/mtab #拿 mount 指令
vim /etc/fstab #開機自動mount，將上一行取的指令放進來
```
