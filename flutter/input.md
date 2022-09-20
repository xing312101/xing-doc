# Input

https://api.flutter.dev/flutter/material/DropdownButton-class.html
https://pub.dev/packages/smart_select



## TextFormField
#### multiple line
```
TextField(
    decoration: InputDecoration(
      border: new OutlineInputBorder(
        borderRadius: BorderRadius.circular(6.0)
      )
    ),
    keyboardType: TextInputType.multiline,
    maxLines: null,
),
```


#### password field
```
TextFormField(
  decoration: InputDecoration(
    focusedBorder: OutlineInputBorder(
      borderSide: BorderSide(color: Colors.red, width: 2.0),
    ),
    enabledBorder: OutlineInputBorder(
      borderSide: BorderSide(color: Colors.black, width: 2.0),
    ),
    hintText: 'Password',
  ),
  obscureText: true,
  enableSuggestions: false,
  autocorrect: false,
)
```

## button


## radio buttons
#### Radio
```
ListTile(
    title: const Text('Apple'),
    leading: Radio(
      value: 1,
      groupValue: _foodType,
      onChanged: (value) {
        setState(() {
          _foodType = value;
        });
      },
    ),
),
```

#### RadioListTile
```
RadioListTile(
  value: 1,
  groupValue: selectedRadioTile,
  title: Text("Apple"),
  subtitle: Text("Apple Subtitle"),
  onChanged: (value) {
    setState(() {
      _foodType = value;
    });
  },
  activeColor: Colors.red,
  secondary: OutlineButton(
    child: Text("Hello"),
    onPressed: () {
      print("Hello");
    },
  ),
  selected: true,
)
```


## Checkbox
> https://api.flutter.dev/flutter/material/Checkbox-class.html

> https://api.flutter.dev/flutter/material/CheckboxListTile-class.html

```
Checkbox(
    value: widget.values[index].selected,
    onChanged: (value) {
      setState(() {
        widget.values[index].selected = !widget.values[index].selected;
      });
    }),
)

```
