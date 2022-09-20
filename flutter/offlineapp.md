# OfflineApp

## plugin
```
sqflite: https://pub.dev/packages/sqflite

path_provider: https://pub.dev/packages/path_provider

path: https://pub.dev/packages/path
```


## SQLite
### 自己寫的基本helper
```
import 'package:path/path.dart';
import 'package:sqflite/sqflite.dart';

class DbHelper {
  late Database _db;

  Database get db => this._db;

  static DbHelper _instance = DbHelper._internal();
  factory DbHelper() {
    return _instance;
  }
  DbHelper._internal();

  open() async {
    String databasesPath = await getDatabasesPath();
    String path = join(databasesPath, 'inspection.db');

    _db = await openDatabase(path);
  }

  // migrate_db() {
  // TODO: migrate db by config file
  // }

  void checkDbSchema() {}
}

```

## NoSQL
> https://pub.dev/packages/couchbase_lite
```
todo
```
