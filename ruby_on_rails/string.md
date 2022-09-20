# String
```
pluralize 將名詞字串轉為複數的名詞
singularize 轉為單數
camelize 轉為駝峰式的字串
underscore 將原先駝峰式的字串轉為路徑式的字串
titleize 將單字的開頭皆轉為大寫
dasherize 將字串中的底線轉為橫線
parameterize 將字串轉為適合url的方式
tableize 將單數名詞轉為複數再將駝峰式的名詞改為底線，tableize的作用主要是協助找出Model的資料表名稱
classify 則是tableize的相反，從資料表的名稱轉為Model
strip 刪除字串前後的空白 like php trim()


補到8碼
"%08d" % 123456 => "00123456"

random string
o = [('a'..'z'), ('0'..'9')].map { |i| i.to_a }.flatten
string = (1..13).map { o[rand(o.length)] }.join
```
