# log rotated
```
# /etc/logrotate.conf

#see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4

# create new (empty) log files after rotating old ones
create

# use date as a suffix of the rotated file
dateext

# uncomment this if you want your log files compressed
#compress

# RPM packages drop log rotation information into this directory
include /etc/logrotate.d

# no packages own wtmp and btmp -- we'll rotate them here
/var/log/wtmp {
	monthly
	create 0664 root utmp
	minsize 1M
	rotate 1
}

/var/log/btmp {
	missingok
	monthly
	create 0600 root utmp
	rotate 1
}

# system-specific logs may be also be configured here.

/var/apache/logs/*log {
	daily
	missingok
	notifempty
	sharedscripts
	delaycompress
	copytruncate 0644 saiswebapp saisops
}

RailsPath/log/* {
	daily
	missingok
	notifempty
	sharedscripts
	delaycompress
	rotate 99999
	copytruncate 0644 saiswebapp saisops
}


其中 daily 表示每天整理，也可以改成 weekly 或 monthly
missingok 表示如果找不到 log 檔也沒關係
rotate 7 表示保留七份
compress 表示壓縮起來，預設用 gzip
delaycompress 表示延後壓縮直到下一次 rotate
notifempty 表示如果 log 檔是空的，就不 rotate
copytruncate 先複製 log 檔的內容後，在清空的作法，因為有些程式一定 log 在本來的檔名，例如 rails。另一種方法是 create。
minsize 1M <==檔案容量一定要超過 1M 後才進行 rotate (略過時間參數)
```
