# intl
> https://pub.dev/packages/intl

## DateTime Format
```
import 'package:intl/intl.dart';

DateFormat('yyyy/MM/dd HH:MM').format(DateTime.now());
```

# i18n
> https://flutter.dev/docs/development/accessibility-and-localization/internationalization

> https://pub.dev/packages/intl_utils


## pubspec.yaml
```
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter
  intl: ^0.17.0

flutter:
  generate: true


```

## l10n.yaml
```
arb-dir: lib/l10n
template-arb-file: app_en.arb
output-localization-file: app_localizations.dart
```

## ${FLUTTER_PROJECT}/lib/l10n/app_en.arb
```
{
    "hello": "world",
}
```


## file of MaterialApp
```
import 'package:flutter_localizations/flutter_localizations.dart';

const MaterialApp(
  title: '...',
  localizationsDelegates: [
    S.delegate,
    GlobalMaterialLocalizations.delegate,
    GlobalWidgetsLocalizations.delegate,
    GlobalCupertinoLocalizations.delegate,
  ],
  supportedLocales: [
    Locale('en', ''), // English, no country code
    Locale('es', ''), // Spanish, no country code
  ],
  // supportedLocales: S.delegate.supportedLocales,  // Or only this line
  home: ...,
);

```


## Android Studio
### Flutter Intl

#### pubspec.yaml
```
flutter_intl:
  enabled: true
```
