# flutter_secure_storage
> https://pub.dev/packages/flutter_secure_storage

## in pubspec.yml
```
dependencies:
  flutter_secure_storage: 3.3.1+1
```

## use
```
final storage = FlutterSecureStorage();

await storage.write(key: 'keyName', value: newToken);
final value = await storage.read(key: 'keyName');

debugPrint("val:" + value);

```
