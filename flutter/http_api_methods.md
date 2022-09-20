# Http api methods
> https://ithelp.ithome.com.tw/articles/10248231


|  | HttpClient | Http |Dio |
| -- | -- | -- | -- |
| application/json | O | O | O |
| application/x-www-form-urlencode | X | O | O |
| multipart/form-data | X | O | O |




## HttpClient
> Flutter dart:io內建的HttpClient

```
void loginHttpClientWWW(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    HttpClient()
        .postUrl(Uri.parse(urlString))
        .then((HttpClientRequest request) {
      request.headers.contentType = ContentType("application", "x-www-form-urlencoded");
      request.write("{\"email\":\"test@test\",\"password\":\"hello\"}");
      return request.close();

    }).then((HttpClientResponse response) {
      if (response.statusCode == 200) {
        response.transform(utf8.decoder).join().then((String string) {
          print("HttpClientWWW Success：$string");
          success();
        });
      } else {
        print("HttpClientWWW Fail：${response.statusCode}");
        fail();
      }
    });
  }

  void loginHttpClientJson(void Function() success, void Function() fail) async {

    var urlString = "http://httpbin.org/delay/1";
    HttpClient()
        .postUrl(Uri.parse(urlString))
        .then((HttpClientRequest request) {
      request.headers.contentType = ContentType("application", "json");

      Map<String,String> p = {"UserName":"test@test", "Password":"hello"};
      request.add(utf8.encode(json.encode(p)));
      return request.close();

    }).then((HttpClientResponse response) {
      if (response.statusCode == 200) {
        response.transform(utf8.decoder).join().then((String string) {
          print("HttpClientJson Success：$string");
          success();
        });
      } else {
        print("HttpClientJson Fail：${response.statusCode}");
        fail();
      }
    });
  }
```


## Http
> https://pub.dev/packages/http

```
void loginHttpWWW(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    Map<String, String> headersMap = new Map();
    headersMap["content-type"] = "application/x-www-form-urlencoded";

    Map<String, String> bodyParams = new Map();
    bodyParams["email"] = "test@test";
    bodyParams["password"] = "hello";
    http.Client()
        .post(urlString, headers: headersMap, body: bodyParams, encoding: Utf8Codec())
        .then((http.Response response) {
      if (response.statusCode == 200) {
        print("httpWWW Success：${response.body}");
        success();
      } else {
        print("httpWWW Fail：${response.statusCode}");
        fail();
      }
    }).catchError((error) {
      print("httpWWW Fail：${error.toString()}");
      fail();
    });
  }

  void loginHttpJson(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    Map<String, String> headersMap = new Map();
    headersMap["content-type"] = ContentType.json.toString();

    Map<String, String> bodyParams = new Map();
    bodyParams["email"] = "test@test";
    bodyParams["password"] = "hello";
    http.Client()
        .post(urlString, headers: headersMap, body: jsonEncode(bodyParams), encoding: Utf8Codec())
        .then((http.Response response) {
      if (response.statusCode == 200) {
        print("httpJson Success：${response.body}");
        success();
      } else {
        print("httpJson Fail：${response.statusCode}");
        fail();
      }
    }).catchError((error) {
      print("httpJson Fail：${error.toString()}");
      fail();
    });
  }

  void loginHttpForm(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    var client = new http.MultipartRequest("post", Uri.parse(urlString));
    client.fields["email"] = "test@test";
    client.fields["password"] = "hello";
    client.send().then((http.StreamedResponse response) {
      if (response.statusCode == 200) {
        response.stream.transform(utf8.decoder).join().then((String string) {
          print("httpForm Success：$string");
          success();
        });
      } else {
        print("httpForm Fail：${response.statusCode}");
        fail();
      }
    }).catchError((error) {
      print("httpForm Fail：${error.toString()}");
      fail();
    });
  }
```

## Dio
> https://pub.dev/packages/dio

```
 void loginDioWWW(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    try {
      Response response = await Dio()
        .post(urlString,
          data: {"email":"test@test", "password":"hello"},
          options: Options(contentType:Headers.formUrlEncodedContentType));
      print("DioWWW Success：${response.data}");
      success();
    } catch (error) {
      print("DioWWW Fail：${error.toString()}");
      fail();
    }
  }

  void loginDioJson(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    try {
      Response response = await Dio()
          .post(urlString,
          data: {"email":"test@test", "password":"hello"},
          options: Options(contentType:Headers.jsonContentType));
      print("DioJson Success：${response.data}");
      success();
    } catch (error) {
      print("DioJson Fail：${error.toString()}");
      fail();
    }
  }

  void loginDioForm(void Function() success, void Function() fail) async {

    var urlString = "https://xxxx.xx/login";
    try {
      Response response = await Dio()
          .post(urlString,
          data: FormData.fromMap({"email":"test@test", "password":"hello"}));
      print("DioForm Success：${response.data}");
      success();
    } catch (error) {
      print("DioForm Fail：${error.toString()}");
      fail();
    }
  }
}
```
