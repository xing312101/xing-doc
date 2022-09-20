# Dotenv
> reference: https://www.npmjs.com/package/dotenv

## install
```
$ npm install dotenv --save

```

## Usage
```
# create file .env

先在專案根目錄建一個 .env 的檔案
裡面寫想要的環境變數
EX:
DB_HOST=localhost
DB_HOST="localhost"
```

```
程式碼
1.
先把dotenv抓進來
require('dotenv').config()
or
require('dotenv').load(); # 只用過這個

2.
使用環境變數
host = process.env.DB_HOST
```
