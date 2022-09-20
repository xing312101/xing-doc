# File
> ref: https://programmingwithswift.com/how-to-save-a-file-locally-with-flutter

> ref: https://pub.dev/packages/path

> ref: https://pub.dev/packages/open_file

> ref: https://pub.dev/packages/path_provider

## get App directory path
```
// path_provider
Directory appDir = await getApplicationDocumentsDirectory();
Directory cacheDir = await getTemporaryDirectory();

```

## File
```
File file = File(localPath);

static Future<String> fileToBase64(File file) async {
    Uint8List tmp = await file.readAsBytes();
    return base64Encode(tmp);
}

```

## join
```
import 'package:path/path.dart' as p;
p.join(dirPath, fileName);

```

## OpenFile
```
// import 'package:open_file/open_file.dart';
await OpenFile.open(filePath);
```






