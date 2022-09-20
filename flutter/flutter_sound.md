# flutter_sound
> ref: https://pub.dev/packages/flutter_sound

> ref: https://pub.dev/packages/tau_sound

> ref: https://flutter-sound.canardoux.xyz/guides_codec.html


## Play Audio
```

FlutterSoundPlayer? _soundPlayer = FlutterSoundPlayer();

void initState() {
    _soundPlayer!.openAudioSession().then((value) {
      setState(() {
        _playerIsInitialed = true;
      });
    });
}

void dispose() {
    _soundPlayer!.closeAudioSession();
    _soundPlayer = null;
}

void startPlayer() {
    _soundPlayer!
        .startPlayer(
            fromURI: filePath,
            whenFinished: () {
                setState(() {});
            })
        .then((value) {
      setState(() {});
    });
}


void stopPlayer() {
    _soundPlayer!.stopPlayer().then((value) {
        setState(() {});
    });
}
```

## Record Audio
```
bool _recorderIsInitialed = false;
FlutterSoundRecorder? _soundRecorder = FlutterSoundRecorder();

void initState() {
    _openTheRecorder().then((value) {
        setState(() {});
    });
}

Future<void> _openTheRecorder() async {
    final status = await Permission.microphone.request();
    if (status != PermissionStatus.granted) {
      throw RecordingPermissionException('Microphone permission not granted');
    }

    await _soundRecorder!.openAudioSession();
    if (await _soundRecorder!.isEncoderSupported(_codec)) {
      _recorderIsInitialed = true;
    }
}

void dispose() {
    _soundRecorder!.closeAudioSession();
    _soundRecorder = null;
}


void _record() async {
    _soundRecorder!.startRecorder(
      toFile: "hello.mp4",
      codec: Codec.aacMP4,
    ).then((value) {
      setState(() {});
    });
}

void _stopRecorder() async {
    await _soundRecorder!.stopRecorder().then((filePath) {
      String fileName = basename(filePath);
    });
}



```
