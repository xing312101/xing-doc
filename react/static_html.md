# Static html
> reference:

> https://reactjs.org/docs/cdn-links.html

> https://babeljs.io/docs/en/babel-standalone

> https://reactjs.org/docs/add-react-to-a-website.html

跟Vue.js一樣，在html裡面寫code要用到babel去包code

記得head要載入react跟babel的js

```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <script src="https://unpkg.com/react@^16/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@16.13.0/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
  </head>

  <body>
    <div id="root"></div>

    <script type="text/babel">
      // React code
    </script>
  </body>
</html>
```
