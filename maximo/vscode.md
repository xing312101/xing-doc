# vscode

## copy files
```
businessobjects.jar
commonweb.jar
maximouiweb.jar # to jar classes dir in maximoui.war
mboejb.jar
mboejbclient.jar
mbojava.jar
properties.jar
```


## project sturcture
```
project
-- src
-- lib
---- maximo.jar files
-- pom.xml

```


## pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <groupId>maximo</groupId>
  <artifactId>maximo</artifactId>
  <version>0.0.1-XING312101-VSCODE-MAXIMO</version>
  <name>maximo</name>
  <dependencies>
    <dependency>
      <groupId>businessobjects</groupId>
      <artifactId>maximo7613.businessobjects</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/businessobjects.jar</systemPath>
    </dependency>

    <dependency>
      <groupId>commonweb</groupId>
      <artifactId>maximo7613.commonweb</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/commonweb.jar</systemPath>
    </dependency>

    <dependency>
      <groupId>maximouiweb</groupId>
      <artifactId>maximo7613.maximouiweb</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/maximouiweb.jar</systemPath>
    </dependency>

    <dependency>
      <groupId>mboejb</groupId>
      <artifactId>maximo7613.mboejb</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/mboejb.jar</systemPath>
    </dependency>

    <dependency>
      <groupId>mboejbclient</groupId>
      <artifactId>maximo7613.mboejbclient</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/mboejbclient.jar</systemPath>
    </dependency>

    <dependency>
      <groupId>mbojava</groupId>
      <artifactId>maximo7613.mbojava</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/mbojava.jar</systemPath>
    </dependency>

    <dependency>
      <groupId>properties</groupId>
      <artifactId>maximo7613.properties</artifactId>
      <version>1.0</version>
      <scope>system</scope>
      <systemPath>${project.basedir}/lib/properties.jar</systemPath>
    </dependency>

  </dependencies>
  <build>
    <sourceDirectory>${basedir}/src</sourceDirectory>
    <resources>
      <resource>
        <directory>src</directory>
        <excludes>
          <exclude>**/*.java</exclude>
        </excludes>
      </resource>
    </resources>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>1.7</source>
          <target>1.7</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```
