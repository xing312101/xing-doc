# Oracle Client

## Lib
```
sudo apt-get install libaio1 #maybe need
```

## download
> referrence: http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html

windows的rails上使用建議下載x86版本，除非railsinstaller支援x64
```
instantclient-basic
instantclient-sdk
instantclient-sqlplus

$ sudo ln -s libclntsh.so.11.1 libclntsh.so
```

##.bashrc
```
export ORACLE_HOME=/opt/oracle/instantclient_11_2
export LD_LIBRARY_PATH=$ORACLE_HOME:$LD_LIBRARY_PATH:
export TNS_ADMIN=$ORACLE_HOME
export NLS_LANG=AMERICAN_AMERICA.AL32UTF8
```

## tnsnames.ora
在 $TNS_ADMIN下create file tnsnames.ora
```
XXXXX_dev_tns =
(DESCRIPTION =
(ADDRESS_LIST =
(ADDRESS = (PROTOCOL = TCP)(HOST = host)(PORT = port))
)
(CONNECT_DATA =
(SERVICE_NAME = SID)
)
)
```
