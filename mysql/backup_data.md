# backup data

## mysqldump
```
mysqldump -u root -p'PASSWORD' DataName > /backup/backup.sql
```
## import
```
mysql -u root -p'PASSWORD' DataName < /backup/backup.sql
```
## crontab backup
```
0 0 * * * /usr/bin/mysqldump -uUser -pPawor -hHost db | gzip -9 -c > /home/ubuntu/backup/db_`date "+\%Y\%m\%d_\%H\%M\%S"`.sql.gz
```
## mysqldump parameters
```
mysqldump支援下列選項：

--add-locks
在每個表傾倒之前增加LOCK TABLES並且之後UNLOCK TABLE。(為了使得更快地插入到MySQL)。

--add-drop-table
在每個create語句之前增加一個drop table。

--allow-keywords
允許創建是關鍵字的列名字。這由表名首碼於每個列名做到。

-c, --complete-insert
使用完整的insert語句(用列名字)。

-C, --compress
如果客戶和伺服器均支援壓縮，壓縮兩者間所有的資訊。

--delayed
用INSERT DELAYED命令插入行。

-e, --extended-insert
使用全新多行INSERT語法。（給出更緊縮並且更快的插入語句）

-#, --debug[=option_string]
跟蹤程式的使用(為了調試)。

--help
顯示一條幫助消息並且退出。

--fields-terminated-by=...

--fields-enclosed-by=...

--fields-optionally-enclosed-by=...

--fields-escaped-by=...

--fields-terminated-by=...

這些選擇與-T選擇一起使用，並且有相應的LOAD DATA INFILE子句相同的含義。見7.16 LOAD DATA INFILE語法。

-F, --flush-logs
在開始傾倒前，洗掉在MySQL伺服器中的日誌檔。

-f, --force,
即使我們在一個表傾倒期間得到一個SQL錯誤，繼續。

-h, --host=..
從命名的主機上的MySQL伺服器傾倒資料。缺省主機是localhost。

-l, --lock-tables.
為開始傾倒鎖定所有表。

-t, --no-create-info
不寫入表創建資訊(CREATE TABLE語句）

-d, --no-data
不寫入表的任何行資訊。如果你只想得到一個表的結構的傾倒，這是很有用的！

--opt
同--quick --add-drop-table --add-locks --extended-insert --lock-tables。應該給你為讀入一個MySQL伺服器的盡可能最快的傾倒。

-pyour_pass, --password[=your_pass]
與伺服器連接時使用的口令。如果你不指定“=your_pass”部分，mysqldump需要來自終端的口令。

-P port_num, --port=port_num
與一台主機連接時使用的TCP/IP埠號。（這用於連接到localhost以外的主機，因為它使用 Unix套接字。）

-q, --quick
不緩衝查詢，直接傾倒至stdout；使用mysql_use_result()做它。

-S /path/to/socket, --socket=/path/to/socket
與localhost連接時（它是缺省主機)使用的套接字檔。

-T, --tab=path-to-some-directory
對於每個給定的表，創建一個table_name.sql檔，它包含SQL CREATE 命令，和一個table_name.txt檔，它包含資料。 注意：這只有在mysqldump運行在mysqld守護進程運行的同一台機器上的時候才工作。.txt檔的格式根據--fields-xxx和 --lines--xxx選項來定。

-u user_name, --user=user_name
與伺服器連接時，MySQL使用的用戶名。缺省值是你的Unix登錄名。

-O var=option, --set-variable var=option
設置一個變數的值。可能的變數被列在下面。

-v, --verbose
冗長模式。列印出程式所做的更多的資訊。

-V, --version
列印版本資訊並且退出。

-w, --where='where-condition'
只傾倒被選擇了的記錄；注意引號是強制的！
"--where=user='jimf'" "-wuserid>1" "-wuserid<1 br="">
最常見的mysqldump使用可能製作整個資料庫的一個備份：

mysqldump --opt database > backup-file.sql

但是它對用來自於一個資料庫的資訊充實另外一個MySQL資料庫也是有用的：

mysqldump --opt database | mysql --host=remote-host -C database

指定dump出來的語系
mysqldump --default-character-set=big5

or

mysqldump --default-character-set=latin1
```

## Export CSV
### using seq
```
mysql -uxxxxx -pwwwwww -h 184.106.139.250 -P 43306 database < sql.sql | sed 's/\t/,/g' > out.csv
```
### using sql
```
SELECT order_id,product_name,qty
FROM orders
INTO OUTFILE '/tmp/orders.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```
