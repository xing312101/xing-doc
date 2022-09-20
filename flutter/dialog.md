# Dialog
> https://api.flutter.dev/flutter/material/AlertDialog-class.html

> https://api.flutter.dev/flutter/material/showDialog.html

> https://api.flutter.dev/flutter/cupertino/showCupertinoDialog.html

> https://api.flutter.dev/flutter/widgets/showGeneralDialog.html

> https://api.flutter.dev/flutter/cupertino/CupertinoAlertDialog-class.html



## Custom Dialog
```
class CustomDialog {
  final _borderRadiusCircularValue = 10.0;
  static CustomDialog _instance;

  factory CustomDialog() {
    if (null == _instance) {
      _instance = new CustomDialog._internal();
    }
    return _instance;
  }
  CustomDialog._internal();

  showMessage(BuildContext context, String title, message, {double height: 500}) async {
    await showDialog(
      context: context,
      builder: (BuildContext context) {
        return Dialog(
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.circular(_borderRadiusCircularValue),
          ),
          child: Container(
            // padding: EdgeInsets.only(top:10, bottom: 10),
            decoration: BoxDecoration(
              borderRadius: BorderRadius.circular(_borderRadiusCircularValue),
            ),
            height: height,
            child: Column(
              children: <Widget>[
                Container(
                  height: 50,
                  decoration: BoxDecoration(
                    boxShadow: [
                      BoxShadow(
                        color: Colors.grey.withOpacity(0.5),
                        offset: Offset(0, 3),
                      ),
                    ],
                    borderRadius: BorderRadius.only(
                        topLeft: Radius.circular(_borderRadiusCircularValue),
                        topRight: Radius.circular(_borderRadiusCircularValue)
                    ),
                    color: Theme.of(context).primaryColor,
                  ),
                  padding: EdgeInsets.only(top:10, bottom: 10),
                  child: Center(
                    child: Text(title, style: TextStyle(fontSize: 24, fontWeight: FontWeight.bold),),
                  ),
                ),
                CommonWidget().divider(),
                Expanded(
                  flex: 1,
                  child: Container(
                    alignment: Alignment.center,
                    child: Text(message),
                  ),
                ),
                CommonWidget().divider(),
                Container(
                  height: 50,
                  child: CommonButton().tabActionButton('關閉', ()=> Navigator.of(context).pop()),
                )
              ],
            ),
          )
        );
      }
    );
  }
}


```
