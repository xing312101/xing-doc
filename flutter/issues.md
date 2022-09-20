# Issues

## SocketException: Failed host lookup: 'url' (OS Error: No address associated with hostname, errno = 7)

at android/app/src/main/AndroidManifest.xml
```
<uses-permission android:name="android.permission.INTERNET"/>
```


## The minCompileSdk (31) specified in a dependency's AAR metadata

at android/app/build.gradle

Note: it is not work on flutter 2.2.1
```
defaultConfig{
    // add start
    configurations.all {
        resolutionStrategy {
            force 'androidx.core:core-ktx:1.6.0'
        }
    }
    // add end

    ...
    ...
    ...
}

```
