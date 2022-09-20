# Start Coding
> Part 1: https://flutter.dev/docs/get-started/codelab

> Part 2: https://codelabs.developers.google.com/codelabs/first-flutter-app-pt2/#0

> hello_flutter: https://github.com/xing312101/hello_flutter

> https://flutter.dev/docs/cookbook

## Use an external package
> find open-source package at https://pub.dev

## flutter entry point
Path: lib/main.dart


## debug log at console
```
inspect(object)
debug(print)
```

## debug UI
```
import 'package:flutter/rendering.dart';

void main() {
  debugPaintSizeEnabled = true;
  runApp(MyApp());
}
```

## basic widget
```
// can not change ui
StatelessWidget

// can change ui by state
StatefulWidget
// set state sample
setState(() { _myState = newValue; })
```

## Add a Stateful Widget
在Android Studio可以輸入stful來自動產生statefulWidget相關的class。

會有兩個class，一個是繼承StatefulWidget，一個是繼承State<自訂義的StatefulWidget>的class

state的class name會依照statefulWidget的class name作相對應的name，eg:
```
class Hello extends StatefulWidget {
    @override
    _HelloState createState() => _HelloState();
}

class _HelloState extend State<Hello> {
    @override
    Widget build(BuildContext context){
        return Container();
    }
}
```


## setState
> https://api.flutter.dev/flutter/widgets/State/setState.html

## layout widget
> https://flutter.dev/docs/development/ui/layout#lay-out-multiple-widgets-vertically-and-horizontally

* Row
* Column
* Stack
* Container
* Center

####  different of Row and Column
> https://flutter.dev/docs/development/ui/layout#aligning-widgets

* mainAxisAlignment
* crossAxisAlignment
* DefaultTextStyle.merge
* EdgeInsetsS

#### helpful widget for layout
* ListView
 * ListView supports app body scrolling when the app is run on a small device.
* ListTile
* Divider
* divideTiles
* GridView
* CARD

## Button
* IconButton
* RaisedButton
* GestureDetector


## image
* Icon
* Icons
* Image.asset
* Image.network

## style
* EdgeInsets
* Color
* Colors

## Responsive
> https://flutter.dev/docs/development/ui/layout/responsive

* AspectRatio
* CustomSingleChildLayout
* CustomMultiChildLayout
* FittedBox
* FractionallySizedBox
* LayoutBuilder
* MediaQuery
* MediaQueryData
* OrientationBuilder

## Layout constrain
> https://flutter.dev/docs/development/ui/layout/constraints

** Constraints go down. Sizes go up. Parent sets position. **


## It is like react component
> https://flutter.dev/docs/development/ui/widgets-intro#changing-widgets-in-response-to-input


## parent control children
> https://flutter.dev/docs/development/ui/widgets-intro#bringing-it-all-together

## Adding interactivity
### Standard widgets
* Form
* FormField

### Material Components
* Checkbox
* DropdownButton
* FlatButton
* FloatingActionButton
* IconButton
* Radio
* RaisedButton
* Slider
* Switch
* TextField


## Drawer
UserAccountsDrawerHeader


## Take a picture using the camera
> https://flutter.dev/docs/cookbook/plugins/picture-using-camera


## uncategory
* Scaffold
* AppBar
* Text


## after build
> https://medium.com/flutterworld/flutter-schedulerbinding-vs-widgetsbinding-149c71cb607f
````
WidgetsBinding.instance.addPostFrameCallback
WidgetsBinding.instance.addPersistentFrameCallback
````

vv
