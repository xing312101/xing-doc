# CPU
```
cat /proc/cpuinfo # 真實的核數是 cpu cores 這個参數值
dmesg | grep CPU # CPU启動信息
cat /proc/cpuinfo |grep "physical id"|sort |uniq|wc -l # 物理CPU的個數
cat /proc/cpuinfo |grep "processor"|wc -l # 邏輯CPU的個數
cat /proc/cpuinfo |grep "cores"|uniq # CPU是幾核
cat /proc/cpuinfo |grep MHz|uniq # CPU的主頻
cat /proc/cpuinfo | grep name | cut -f2 -d: | uniq -c # cpu型號
getconf LONG_BIT # cpu運行位數
cat /proc/cpuinfo | grep flags | grep ' lm ' | wc -l # cpu是否支持64bit計算，大於0，說明支持64bit計算
在aix和ubuntu上可以使用lscpu命令查看cpu信息
```
