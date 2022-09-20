# sqflite
> https://pub.dev/packages/sqflite


#### 自建簡單helper範本
```
class DbHelper {
  String dbFileName = 'dbFileName.db';

  Database? _db;

  static DbHelper _instance = DbHelper._internal();

  factory DbHelper() {
    return _instance;
  }
  DbHelper._internal();

  Future<Database> get db async {
    if (null != _db) {
      return _db!;
    }

    String databasesPath = await getDatabasesPath();
    String path = join(databasesPath, this.dbFileName);

    _db = await openDatabase(path);
    return _db!;
  }

  Future<void> delDb() async {
    String databasesPath = await getDatabasesPath();
    String path = join(databasesPath, this.dbFileName);

    if (await databaseExists(path)) {
      await deleteDatabase(path);
      _db = null;
    }
  }
}

```


## sqlite query
#### query table exist
```
# SELECT name FROM sqlite_master WHERE type='table' AND name='{table_name}';

await db.query('sqlite_master', where: 'type = ? AND name = ?', whereArgs: ['table', tableName]);

```

#### query create table or drop with exist
```
# create table if not exists TableName (col1 typ1, ..., colN typN);
execute("create table if not exists $tableName (columnName1 VARCHAR(255), columnName2 VARCHAR(255));");

# drop table if exists TableName;
execute("drop table if exists $tableName;");
```
