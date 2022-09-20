# Gitbook
## editor
> https://github.com/GitbookIO/editor-legacy/releases

## install
```
$ sudo npm install gitbook-cli -g
```

## update / show version
```
$ gitbook --version


CLI version: 2.3.2
Installing GitBook 3.2.3
GitBook version: 3.2.3
```

## update gitbook-cli
```
$ npm update gitbook-cli -g
```

## uninstall gitbook-clie
```
sudo npm uninstall gitbook-cli -g
```

## create a gitbook
建議開一個目錄進去操作
```
$ gitbook init

warn: no summary file in this book
info: create README.md
info: create SUMMARY.md
info: initialization is finished
```

## start gitbook server
```
$ gitbook serve
```

## build a static html
```
$ gitbook build
```

## hide gitbook default link
### book.json
```
{
	"styles": {
		"website": "css/gitbook.css"
	}
}
```
### css/gitbook.css
```
.gitbook-link {
	display: none !important;
}
```


