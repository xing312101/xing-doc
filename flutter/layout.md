# layout

## avoid UIoverflow
```
#### row
Expanded(
    flex: ..... // option
    child: Row(
        children: []
    )
)

Flexable(
    child: Row(
        children: []
    )
)


#### column
SingleChildScrollView(
    child: Column(
        children: []
    )
)
```


## flex

## NestedScrollView




## table DataTableSource
> https://material.io/components/data-tables/flutter#theming-data-tables


## ListView
> https://medium.com/flutter-community/flutter-adding-separator-in-listview-c501fe568c76

```
ListView.separated(
  separatorBuilder: (context, index) => Divider(
        color: Colors.black,
      ),
  itemCount: 20,
  itemBuilder: (context, index) => Padding(
        padding: EdgeInsets.all(8.0),
        child: Center(child: Text("Index $index")),
      ),
)
```

#### fix ListView overlow
```
ListView(
   primary: false,
   shrinkWrap: true,
),
```

## Expansiable
> https://api.flutter.dev/flutter/material/ExpansionPanel-class.html

> https://api.flutter.dev/flutter/material/ExpansionPanelList-class.html


#### ExpansionTile
#### ExpansionPanelList
#### ExpansionPanel
```
```



