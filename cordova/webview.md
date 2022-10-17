# WebView

Remove some codes at index.html
Clear index.css

## config.xml
Add <allow-navigation href="*://*.google.com/*" /> for open web in app

## index.js
```
document.addEventListener('deviceready', onDeviceReady, false);

function onDeviceReady() {
    let url = "https://www.google.com";
    goToTarget(url);
}

function goToTarget(url) {
    window.location = url;
    return;
}
```
