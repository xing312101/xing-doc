# code
## require module example
##### method 1:
```
# module.js

module.exports = "hello world";
```
```
# index.js

hi = require("module.js");
// log hi: "hello world"
```

##### method 2:
```
# module.js

function Hello() {
    this.world = "Xing's World";
}

module.exports = Hello;
//exports = module.exports = Hello;
```
```
# index.js

hi = require("module.js");
hello = new hi();
echo hello.world;
```
