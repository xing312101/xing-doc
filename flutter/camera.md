# Camera
> https://pub.dev/packages/camera
> https://flutter.dev/docs/cookbook/plugins/picture-using-camera


```
camera: ^0.9.4+2
```


## ISO
### Privacy
Privacy - Camera Usage Description

Privacy - Microphone Usage Description

#### ios/Runner/Info.plist
```
<key>NSCameraUsageDescription</key>
<string>Can I use the camera please?</string>
<key>NSMicrophoneUsageDescription</key>
<string>Can I use the mic please?</string>
```

## flutter

```
## before runApp
try {
    WidgetsFlutterBinding.ensureInitialized();
    cameras = await availableCameras();
} on CameraException catch (e) {
    logError(e.code, e.description);
}
```
