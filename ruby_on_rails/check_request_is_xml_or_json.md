# Check request is XML or Json
```
string = request.body.read
# if string is xml
object = Hash.from_xml(string)
# elsif string is JSON
object = ActiveSupport::JSON.decode(string)
```
