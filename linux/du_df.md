# du df
```
目錄下每一個檔案/資料夾的所佔空間
du -smh *

計算資料夾容量(total)
cd /test
du -s
441800 .
-s, --summarize : display only a total for each argument資料夾下每個資料夾的大小

cd /test
du -h
-h : 單位為 mb列出佔用空間前 5 名
du -s /var/* | sort -rn | head -5
xargs du -s：列出資料夾大小 (單位是 K)
```
