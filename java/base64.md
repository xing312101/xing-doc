# Base64
> ref: https://stackoverflow.com/questions/14413169/which-java-library-provides-base64-encoding-decoding

## JAVA 8, 9
```
## encode
byte[] message = "hello world".getBytes(StandardCharsets.UTF_8);
String encoded = Base64.getEncoder().encodeToString(message);

## decode
byte[] decoded = Base64.getDecoder().decode("aGVsbG8gd29ybGQ=");

```

## JAVA 6, 7
```
## encode
byte[] message = "hello world".getBytes("UTF-8");
String encoded = DatatypeConverter.printBase64Binary(message);

## decode
byte[] decoded = DatatypeConverter.parseBase64Binary("aGVsbG8gd29ybGQ=");

```
