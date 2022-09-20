# MySQL
## Table size
```
SELECT concat(table_schema,'.',table_name),
concat(round(table_rows/1000000,2),'M') rows,
concat(round(data_length/(1024*1024*1024),2),'G') DATA,
concat(round(index_length/(1024*1024*1024),2),'G') idx,
concat(round((data_length+index_length)/(1024*1024*1024),2),'G') total_size,
round(index_length/data_length,2) idxfrac
FROM information_schema.TABLES
ORDER BY data_length+index_length DESC LIMIT 20;

# where table_schema='note'; note 改資料庫名稱
```

```
# 加總
SELECT round(sum(data_length)/(1024*1024),2) DATA_SUM,
-> round(sum(index_length)/(1024*1024),2) INDEX_SUM,
-> round(sum(data_length)+sum(index_length),2) TOTAL
-> FROM information_schema.TABLES
-> where table_schema='note';
```

## Database size
```
SELECT table_schema AS "Database name",
SUM(data_length + index_length) / 1024 / 1024 AS "Size (MB)"
FROM information_schema.TABLES
GROUP BY table_schema;
```

## table struct
```
SHOW FULL FIELDS FROM database.table
SHOW FULL FIELDS FROM table FROM database
SHOW FULL FIELDS FROM table # 若已經 use database 過了, 這樣子即可
DESC table //顯示比較少欄位的資料結構
```

## start, stop, restart MySQL
### On Linux start/stop/restart from the command line:
```
sudo /etc/init.d/mysqld start
sudo /etc/init.d/mysqld stop
sudo /etc/init.d/mysqld restart

sudo service mysqld start
sudo service mysqld stop
sudo service mysqld restart

sudo service mysql start
sudo service mysql stop
sudo service mysql restart
```

### On macOS Sierra & OS to start/stop/restart MySQL post 5.7 from the command line:
```
sudo launchctl load -F /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist
sudo launchctl unload -F /Library/LaunchDaemons/com.oracle.oss.mysql.mysqld.plist
```

### On OS X to start/stop/restart MySQL pre 5.7 from the command line:
```
sudo /usr/local/mysql/support-files/mysql.server start
sudo /usr/local/mysql/support-files/mysql.server stop
sudo /usr/local/mysql/support-files/mysql.server restart
```
