# setting

## update DB config
> ref: https://stackoverflow.com/questions/48215839/cannot-start-maximo-due-to-error-in-configdb

```
at maximo\tools\maximo

run configdb.bat or configdb.sh
```

## change db model class

Maximo dashborad:
1. System Configuration > Platform Configuration > Database Configuration

2. Select a table

3. change the class


## update maximo.ear
```
jar uf businessobjects.jar com
jar uf maximo.ear businessobjects.jar

```

