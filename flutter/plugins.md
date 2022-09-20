# plugins
> https://pub.dev

> https://kknews.cc/zh-tw/tech/j29jv8p.html keyword: flutter好用的輪子推薦

## add the package
> find open-source package at https://pub.dev

Add package at path: project/pubspec.yaml

"english_words" as sample
```
dependencies:
    flutter:
        sdk: flutter
    cupertino_icons: ^0.1.2
    english_words: ^3.1.5

```
** update packages **
```
$ flutter pub get
```

** import package to code **
```
import 'package:english_words/english_words.dart';

final wordPair = WordPair.random();

child: Text(wordPair.asPascalCase);

```

# simple_animations
> https://pub.dev/packages/simple_animations


# crypto
> https://pub.dev/packages/crypto

crypto library is the main heart of our app. It holds the HMAC algorithm.

# path_provider
> https://pub.dev/packages/path_provider

path_provider will help use to write a file in external storage.

# simple_permissions
> https://pub.dev/packages/simple_permissions

simple_permissions will help to deal with the runtime permissions.







