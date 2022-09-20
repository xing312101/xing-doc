# find
## find and exec
```
find . -mtime +200 -exec mv {} path \;
find path -name "*" -exec ln -s {} . \;
```

## find and keyword
```
find ./ | xargs grep "keyword"
find ./ -name ".bash*" | xargs grep "keyword"
```

## locate
```
$ locate filename
```
