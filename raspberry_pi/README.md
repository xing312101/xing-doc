# Raspberry Pi

## Raspberry configuration

```
$ sudo rasp-config;
```
### Preference -> Raspberry Pi configuration

#### Change:

#### hostname (not to use default raspberrypi)

#### Interfaces : Enable

1. SSH
2. VNC
3. Serial Port
4. Serial Console
5. 1-Wire modules


## Initialize Your Raspberry Pi

1. update os packages
```
$ sudo apt-get update;
```

2. Enable VNC
```
Windows: https://www.realvnc.com/en/connect/download/vnc/windows/
MacOS: https://www.realvnc.com/en/connect/download/vnc/macos/
$ sudo raspi-config; #Change VNC enable)
$ sudo vi /boot/config.txt
# Uncomment "hdmi_force_hotplug=1"
```

3. Install python3
```
$ sudo apt-get install python3-pip;
```

4. Virtual keyboard
```
$ sudo apt-get install florence;
$ sudo apt-get install at-spi2-core;
```

5. OpenPLC install
```
https://www.openplcproject.com/runtime/raspberry-pi/
$ sudo apt-get install git
$ git clone https://github.com/thiagoralves/OpenPLC_v3.git
$ cd OpenPLC_v3
$ ./install.sh rpi
open browser "localhost:8080", login openplc/openplc
```



## VNC Viewer

## Open PLC


## Raspberry Pi to Install wlther
### Temperature Sensor python
```
sudo pip3 install w1thermsensor;
```


## Repository 'http://raspbian.raspberrypi.org/raspbian buster InRelease' changed its 'Suite' value from 'stable' to 'oldstable'
```
sudo apt update

sudo apt full-upgrade // 可以不用
```


## mysql => mariadb-server
```
sudo apt-cache search mysql // 找不到mysql

sudo apt-get install mariadb-server-10.3 // 改用這個

sudo mysql // 可以用mysql command
```

### 設定
```
use mysql;
UPDATE user SET password=password('123456') WHERE user='root';
UPDATE user SET plugin='mysql_native_password' WHERE user = 'root';
FLUSH PRIVILEGES;
exit
```
然後重開
```
sudo systemctl restart mariadb
```
