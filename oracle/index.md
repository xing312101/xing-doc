# Index

## 查詢變慢

```
# 1. 找degree高的index
select degree from dba_indexes where index_name='index_name';

# 2. 關閉parallel query
alter index index_name noparallel;


```
