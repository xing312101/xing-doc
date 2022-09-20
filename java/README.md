# Java

## Regular Expression
> https://openhome.cc/Gossip/Regex/MatcherJava.html

### Pattern

```
var pattern = Pattern.compile("^abc");
var matcher = pattern.matcher("abcd");
matcher.find()
```

## JAR EAR

```
jar xf “file.name.jar” => 解壓
jar uf “file.name.final.jar” “file.name.class”

```


## Java 11: import javax
at pom.xml
```
    <dependency>
        <groupId>com.sun.xml.ws</groupId>
        <artifactId>jaxws-ri</artifactId>
        <version>2.3.0</version>
        <type>pom</type>
    </dependency>
```
