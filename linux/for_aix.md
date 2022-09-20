# for AIX
```
1. 查看邏輯CPU個數
#pmcycles -m

2. 查看物理CPU個數
#prtconf|grep Processors

3. 確定CPU是幾核
用邏輯CPU除以物理CPU就是核數。

4. 查看單個CPU的詳細信息
#lsattr -E -l proc0
```
