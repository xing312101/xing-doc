# Dart
> https://dart.dev/get-dart

```
// Mac
 brew tap dart-lang/dart
 brew install dart
```

## libraries-and-visibility
> https://dart.dev/guides/language/language-tour#libraries-and-visibility.

對Dart而言每個app都是個libaray即使沒有用libaray directive.

用 下底線(_) 開頭的變數名稱作為 private 變數


## Map
#### check key exist
```
m.containsKey(k)
```

#### putIfAbsent
> https://api.dart.dev/stable/2.13.4/dart-core/Map/putIfAbsent.html

```
Map _instances = {}
_instances.putIfAbsent(key, () => new MyClass());

```


