# windows offline

## Android Studio
```
prefer Android Studio 3.5.3
In order to set gradle offline mode easyily
```

## [!] Android Studio (not installed)
```
flutter config --android-studio-dir="C:\Program Files\Android\Android Studio"
```

## Environment Variable (example)

#### ANDROID_HOME:
```
C:\Android
```

#### ANDROID_SDK_ROOT:
```
C:\Android\sdk\Android
```

#### PATH:
```
C:\dart-sdk\bin
C:\flutter\bin
```

## SDK
### Android SDK
#### method 1
> https://developer.android.com/studio/command-line/sdkmanager

```
https://developer.android.com/studio#downloads

using command line tool to get sdkmanager
```


#### method 2
Download from Android Studio or another IDE

### Dart SDK
> https://dart.dev/tools/sdk/archive

### Flutter SDK
> https://flutter.dev/docs/development/tools/sdk/releases?tab=windows


## Android Studio
> https://developer.android.com/studio

### plugins
Need to check the version of plugins and android studio

#### Dart
> https://plugins.jetbrains.com/plugin/6351-dart

#### Flutter
> https://plugins.jetbrains.com/plugin/9212-flutter

## Gradle
> https://gradle.org/releases/

> offline files of Gradle  are copied from another computer which has build apk success.

```
Offline
# gradle-wrapper.properties
## flutter project: android\gradle\wrapper\gradle-wrapper.properties
distributionUrl=file:///c:/x/install/gradle-4.10.2-all.zip

# .gradle directory
## defulat path C:\Users\{{Administrator}}\.gradle
copy file to this path

## environment name
GRADLE_USER_HOME


```

## Intel Hardware Accelerated Execution Manager (HAXM)
> https://github.com/intel/haxm




# Summary
```
1. 環境變數

ANDROID_SDK_ROOT => C:\Android\sdk\Android

GRADLE_USER_HOME => C:\.gradle

PATH (add) => C:\flutter\bin

PATH (add) => C:\dart-sdk\bin



2. Gradle

unzip gradle_20210227c.7z to C:\.gradle

put gradle-4.10.2-all at global place. ex: d:\



3. Android SDK

unzip Android.7z to C:\Android



4. Dart SDK

unzip dartsdk-windows-x64-release.zip to c:\dart-sdk



5. Flutter SDK

unzip flutter.7z to C:\flutter



6. Android studio

=> "Build, Execution, Deployment" > "Build Tool > Gradle"

Set gradle is offline mode

Set gradle path is c:\.gradle



=> "Appearance & Behavior > System Settings > Android SDK"

Set SDK Path is C:\Android\sdk\Android



=> Plugins

import Dart-191.8593.zip

import flutter-intellij.zip

7. Project code
修改android\gradle\wrapper\gradle-wrapper.properties當中的distributionUrl

依照檔案位置做調整
distributionUrl=file:///c:/xxxPath/gradle-4.10.2-all.zip

```


