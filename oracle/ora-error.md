# ORA-ERROR


## ORA-04031: unable to allocate nn bytes of shared memory

```
path: /opt/oracle/product/12.1.0.2/dbhome_1/dbs/init.ora
```

> ref: https://smarttechways.com/2020/03/16/ora-04301-unable-to-allocate-xxx-bytes-of-shared-memory/

```
SQL> show parameter pool
SQL> show parameter sga_target
SQL> show parameter memory_target

=> SELECT name, value FROM v$parameter WHERE name IN ('shared_pool_size', 'large_pool_size', 'shared_pool_reserved_size', 'sga_target', 'memory_target');
```

#### Increasing the value of the INIT.ORA parameters “shared_pool_reserved_size”, “shared_pool_size” and “large_pool_size”.
```
ALTER SYSTEM SET shared_pool_size = 1g scope=both;
ALTER SYSTEM SET large_pool_size=100M scope=both;
ALTER SYSTEM SET shared_pool_reserved_size=512M scope=spfile;
```

#### If it not set then increase the SGA_TARGET or MEMORY_TARGET parameter as you set which will allocate more space to the Shared POOL size.
```
ALTER SYSTEM SET SGA_TARGET=3G scope=spfile;
OR
ALTER SYSTEM SET MEMORY_TARGET=3G scope=spfile;
```
