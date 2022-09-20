# Windows

## Printer
```
copy file_path printer_path

# 利用其他程式送到printer
# 小畫家
mspaint /p file_path /pt printer_path
# adobe
AcroRd32.exe /n /t file_path
```

## like linux commander
### cygwin
```
安裝時這些建議勾選
vim
openssh
rsync
unzip
zip
cygrunsrv
cron
tar
util-linux
ncurses
imagemagic
```

## DNS Cache
### 清除DNS Cache
```
Windows 要清掉 DNS Cache
方法1
執行 cmd ipconfig /flushdns
看到此行字即完成: successfully flushed the dns resolver cache
方法2
控制台 -> 管理工具 -> 服務重新啟動 DNS Client 和 DHCP Client 服務即可.
```
