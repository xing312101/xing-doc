# qr_code_scanner
> https://pub.dev/packages/qr_code_scanner


## wrong version of Kotlin
> https://github.com/juliuscanute/qr_code_scanner/issues/325

```
1. In android/build.gradle bump ext.kotlin_version = '1.3.50' to ext.kotlin_version = '1.5.10'
2. In android/build.gradle bump classpath 'com.android.tools.build:gradle:3.5.0' to classpath 'com.android.tools.build:gradle:4.2.0'
3. In android/gradle/wrapper/gradle-wrapper.properties bump distributionUrl=https\://services.gradle.org/distributions/gradle-5.6.2-all.zip to distributionUrl=https\://services.gradle.org/distributions/gradle-6.9-all.zip
```


