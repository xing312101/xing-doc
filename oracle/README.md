# Oracle
> https://www.oracle.com

## Download Oracle Database
https://www.oracle.com/tw/database/technologies/oracle-database-software-downloads.html

## Download ODAC (Oracle.dataAccess.Client)
https://www.oracle.com/database/technologies/dotnet-odacdev-downloads.html

## Download Oracle Client
https://www.oracle.com/tw/database/technologies/instant-client/winx64-64-downloads.html
- Client version 11.2.0.3 or 11.2.0.4 at least



## Drop table
```
DROP TABLE "DATABASE"."TABLE_NAME" CASCADE CONSTRAINTS PURGE;
DROP SEQUENCE "DATABASE"."TABLE_NAME_SEQ";
```
## Truncate table
```
Truncate Table TABLE_NAME;
```

## Create table
```
CREATE SEQUENCE "DATABASE"."TABLE_NAME_SEQ" MINVALUE 1 MAXVALUE 9999999999999999999999999999 INCREMENT BY 1 START WITH 10000 CACHE 20 NOORDER NOCYCLE ;
CREATE TABLE "DATABASE"."TABLE_NAME_SEQ" ("ID" NUMBER(38,0), "USER_ID" NUMBER(38,0), ...) SEGMENT CREATION IMMEDIATE PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645 PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT) TABLESPACE "DATABASE" ;
```

## pdate version Date
### 查詢Oracel version and Timezone version
```
select * from v$timezone_file;
SELECT * FROM v$version
```
### fix timestamp 異常
發生在升級Oracle版本時發生的，11.2升到12.1時，不確定客戶如何升級，但是資料庫的timestamp發生異常。
```
UPDATE users SET CREATED_AT = TO_DATE(to_char(CREATED_AT, 'yyyy-mm-dd hh24:mi:ss'), 'yyyy-mm-dd hh24:mi:ss');
```

## SQL plus 登入資料庫
```
sqlplus userName/userPassword@//host:port/SID

sqlplus user/password@(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=xxx.xxx.xxx)(PORT=1532)))(CONNECT_DATA=(SERVICE_NAME=servicename)))
```

## oracle 條件數量不能超過1000個 with rails
```
ex: select * from users where id in (1 .. 1000) OK
select * from users where id in (1 .. 1001) FAIL

# Rails
user_ids = found_user_ids.in_groups_of(1000, false)
user_ids.each do |user_ids_of_1000|
query << "users.id in (#{user_ids_of_1000.join(',')})"
end
filter_query = query.join(' or ')
```


##
