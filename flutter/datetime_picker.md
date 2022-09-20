# DateTime Picker
> https://api.flutter.dev/flutter/material/showDatePicker.html

> https://api.flutter.dev/flutter/material/showTimePicker.html

> https://api.flutter.dev/flutter/material/showDateRangePicker.html

```

RaisedButton(
                    child: Text(
                      '修改日期',
                      style: TextStyle(fontSize: 20.0, color: Colors.blue),
                    ),
                    onPressed: () async{
                      final dateResult = await showDatePicker(
                          context: context,
                          initialDate: DateTime.now(),
                          firstDate: DateTime(2020, 01),
                          lastDate: DateTime(2100, 12));

                      debugPrint(dateResult.toString());
                    },
                  ),
                  RaisedButton(
                    child: Text(
                      '修改時間',
                      style: TextStyle(fontSize: 20.0, color: Colors.blue),
                    ),
                    onPressed: () async {
                      final timeResult = await showTimePicker(
                          context: context, initialTime: TimeOfDay.now());
                      debugPrint('$timeResult');
                    },
                  ),
```
