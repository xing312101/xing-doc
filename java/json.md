# json

## JSON-java
> https://jar-download.com/artifacts/org.json
> https://stleary.github.io/JSON-java
> https://github.com/stleary/JSON-java

```
Map<String,Object> map = new HashMap<String,Object>();

map.put("keyName", "value123");

List<String> list = new ArrayList<String>();
list.add ....

map.put("list", list);

JSONObject json = new JSONObject(map);

```


## parsing Datetime
```
SimpleDateFormat dateParser = new SimpleDateFormat("yyyy-MM-dd'T'HH:mm:ss");
if (!dataObj.isNull("key")) {
  String tString = dataObj.get("tString").toString();
  dateParser.parse(tString);
}
```
