# Database SQL
## sql select 串接 concat
```
MySQL: CONCAT( )
Oracle: CONCAT( ), ||
SQL Server: +
```

## group rownumber
```
WITH
USER_SCOPE AS (
	SELECT ROW_NUMBER() OVER (PARTITION BY NAME ORDER BY AGE DESC) AS RANK_NO, *
	FROM USERS
),
YANGEST_USERS AS (
	SELECT * FROM USER_SCOPE WHERE RANK_NO = 1
),
```

## group concat in db2
```
SELECT
		ITEM.ITEMNUM,
		LISTAGG(DISTINCT BAND_ITEMS.VENDOR,',')  WITHIN GROUP(ORDER BY VENDOR ASC)  AS BRAND_NAMES
	FROM
		ITEM
	INNER JOIN BAND_ITEMS ON
		ITEM.ITEMNUM = BAND_ITEMS.ITEMNUM
	GROUP BY
		ITEM.ITEMNUM;
```

## Next id value in db2
> https://www.ibm.com/docs/en/db2/11.5?topic=expressions-sequence-reference
```
QQ: does not work.
   INSERT INTO order(orderno, custno)
     VALUES (NEXT VALUE FOR order_seq, 123456);
or
   UPDATE order
     SET orderno = NEXT VALUE FOR order_seq
     WHERE custno = 123456;
or
   VALUES NEXT VALUE FOR order_seq INTO :hv_seq;
```
```
-- it can work
INSERT INTO table(TABLE_ID, value)
     VALUES (TABLE_IDSEQ.nextval, 'HelloWorld');
```