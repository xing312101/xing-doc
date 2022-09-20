# Flutter
> https://dart.dev/get-dart

> https://flutter.dev

> https://book.flutterchina.club

> https://www.mdeditor.tw/pl/pUFP/zh-tw # about build version

## Notice
install dart first

## Version Control
> https://github.com/leoafarias/fvm

> https://fvm.app/

```
$ pub global activate fvm
$ fvm install v1.7.8+hotfix.4

per project
$ fvm use <version>

global
$ fvm use <version> --global

```

## Flutter's build modes
> https://flutter.dev/docs/testing/build-modes

## flutter commands

#### check dependencies
```
$ flutter doctor
```

#### build web version
> https://flutter.dev/docs/get-started/web

目前beta所以官方建議是用新的version
```
$ flutter channel beta // 切換beta
$ flutter upgrade // 取得新的version
$ flutter config --enable-web
```

#### Update package
類似 bundle install
```
$ flutter pub get
```



## Adding a launcher icon
> https://pub.dev/packages/flutter_launcher_icons

### pubspec.yaml
```
dev_dependencies:
  flutter_launcher_icons: "^0.9.2"

flutter_icons:
  android: "launcher_icon"
  ios: true
  image_path: "assets/icon/icon.png"

```
### run
```
flutter pub run flutter_launcher_icons:main
```

## Android release build
> https://docs.flutter.dev/deployment/android


### Create an upload keystore
```
On Mac/Linux, use the following command:
  keytool -genkey -v -keystore ~/upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload

On Windows, use the following command:
  keytool -genkey -v -keystore c:\Users\USER_NAME\upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

### [project]/android/key.properties
```
storePassword=<password from previous step>
keyPassword=<password from previous step>
keyAlias=upload
storeFile=<location of the key store file, such as /Users/<user name>/upload-keystore.jks>
```

### Proguard Rule
> android/app/proguard-rules.pro

```
## Flutter wrapper
-keep class io.flutter.app.** { *; }
-keep class io.flutter.plugin.**  { *; }
-keep class io.flutter.util.**  { *; }
-keep class io.flutter.view.**  { *; }
-keep class io.flutter.**  { *; }
-keep class io.flutter.plugins.**  { *; }
-dontwarn io.flutter.embedding.**
```

### Configure signing in gradle
at [project]/android/app/build.gradle

#### Add the keystore information
```
   def keystoreProperties = new Properties()
   def keystorePropertiesFile = rootProject.file('key.properties')
   if (keystorePropertiesFile.exists()) {
       keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
   }

   android {
         ...
   }

```

#### buildTypes
```
signingConfigs {
    release {
        keyAlias keystoreProperties['keyAlias']
        keyPassword keystoreProperties['keyPassword']
        storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
        storePassword keystoreProperties['storePassword']
    }
}

buildTypes {
    debug {
        signingConfig signingConfigs.debug
        minifyEnabled false
        useProguard true
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }

    release {
        signingConfig signingConfigs.release
        useProguard true
        shrinkResources true
        minifyEnabled true
        proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
    }
}
```










