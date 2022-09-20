# Command Skill

## pushed popd
切換dir

## rsync
```
rsync -av --delete /cygdrive/d/from_dir/ /cygdrive/d/to_dir/ --exclude=.svn --exclude=tmp --exclude=log
```

## 檔名加時間
```
myfile_`date '+%F_%T'`.txt
```

## awk and xargs
```
ps -ef | grep '/usr/bin/ssh' | awk '{print $2}' | xargs kill -9;
```

## grep 正則
```
正則
grep "^\[2015\/11\/07" development.log > tmp.log
```

## curl


## date with timezone
```
TZ=America/New_York date
```

## sudo without password
```
sudo echo 'yuxing ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/90-cloud-init-users
```

## resize partition
```
resize /block_name
fuser -k /block_name
umount /block_name
resize2fs -f /dev/storage_block_name
mount /block_name
mount -o remount,rw /block_name
```

## killall


