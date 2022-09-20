# EnvironmentConfig

## run with parameter
```
flutter run --dart-define=ENVIRONMENT=STAGING
```

## assets/config/server.json
```
{
  "Dev": {
    "host": "123"
  },
  "Prod": {
    "host": "456"
  }
}
```

## lib/config/environment.dart
```
enum EnvironmentMode { dev, prod }

class AppEnvironment {
  EnvironmentMode? mode; // dev, prod
  String? host;

  static final AppEnvironment _instance = AppEnvironment._internal();
  factory AppEnvironment() {
    return _instance;
  }
  AppEnvironment._internal();

  initConfig(EnvironmentMode mode) async {
    this.mode = mode;
    String target = mode.toString().split('.').last;

    final serverJson = await Util.loadJsonFile('assets/config/server.json');

    this.host = serverJson['target']['host'];
  }
}
```
