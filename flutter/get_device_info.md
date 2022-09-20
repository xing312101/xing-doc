# get device info
> https://pub.dev/packages/device_info

> https://pub.dev/packages/package_info/install

```
Map<String, dynamic> _information = <String, dynamic>{};
try {
  // print('@@ DeviceInfoPlugin');
  DeviceInfoPlugin deviceInfoPlugin = DeviceInfoPlugin();
  if (Platform.isAndroid) {
    AndroidDeviceInfo deviceInfo = await deviceInfoPlugin.androidInfo;

    _information['version.securityPatch'] = deviceInfo.version.securityPatch;
    _information['version.sdkInt'] = deviceInfo.version.sdkInt;
    _information['version.release'] = deviceInfo.version.release;
    _information['version.previewSdkInt'] = deviceInfo.version.previewSdkInt;
    _information['version.incremental'] = deviceInfo.version.incremental;
    _information['version.codename'] = deviceInfo.version.codename;
    _information['version.baseOS'] = deviceInfo.version.baseOS;
    _information['board'] = deviceInfo.board;
    _information['bootloader'] = deviceInfo.bootloader;
    _information['brand'] = deviceInfo.brand;
    _information['device'] = deviceInfo.device;
    _information['display'] = deviceInfo.display;
    _information['fingerprint'] = deviceInfo.fingerprint;
    _information['hardware'] = deviceInfo.hardware;
    _information['host'] = deviceInfo.host;
    _information['id'] = deviceInfo.id;
    _information['manufacturer'] = deviceInfo.manufacturer;
    _information['model'] = deviceInfo.model;
    _information['product'] = deviceInfo.product;
    _information['supported32BitAbis'] = deviceInfo.supported32BitAbis;
    _information['supported64BitAbis'] = deviceInfo.supported64BitAbis;
    _information['supportedAbis'] = deviceInfo.supportedAbis;
    _information['tags'] = deviceInfo.tags;
    _information['type'] = deviceInfo.type;
    _information['isPhysicalDevice'] = deviceInfo.isPhysicalDevice;
    _information['androidId'] = deviceInfo.androidId;
    // information['systemFeatures'] = deviceInfo.systemFeatures;
  } else if (Platform.isIOS) {
    IosDeviceInfo deviceInfo = await deviceInfoPlugin.iosInfo;

    _information['name'] = deviceInfo.name;
    _information['systemName'] = deviceInfo.systemName;
    _information['systemVersion'] = deviceInfo.systemVersion;
    _information['model'] = deviceInfo.model;
    _information['localizedModel'] = deviceInfo.localizedModel;
    _information['identifierForVendor'] = deviceInfo.identifierForVendor;
    _information['isPhysicalDevice'] = deviceInfo.isPhysicalDevice;
    _information['utsname.sysname:'] = deviceInfo.utsname.sysname;
    _information['utsname.nodename:'] = deviceInfo.utsname.nodename;
    _information['utsname.release:'] = deviceInfo.utsname.release;
    _information['utsname.version:'] = deviceInfo.utsname.version;
    _information['utsname.machine:'] = deviceInfo.utsname.machine;
  }
} catch (e){
  print('$e');
}

try {
  // print('@@ PackageInfo');
  PackageInfo packageInfo = await PackageInfo.fromPlatform();

  _information['packageInfo.appName'] = packageInfo.appName;
  _information['packageInfo.packageName'] = packageInfo.packageName;
  _information['packageInfo.version'] = packageInfo.version;
  _information['packageInfo.buildNumber'] = packageInfo.buildNumber;
} catch (e) {
  print('$e');
}

return _information;

```
