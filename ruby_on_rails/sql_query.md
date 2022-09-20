# SQL Query
> 非Rails架構的做法，只是有時model真的太麻煩，或者model的query效率不好時，再來這樣做

```
ActiveRecord::Base.establish_connection(...)
ActiveRecord::Base.connection.execute(...)

connection = ActiveRecord::Base.connection
connection.execute("SQL query");
```
