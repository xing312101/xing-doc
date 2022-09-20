# Oracle database

要安裝 oracle client

## gems
```
gem install ruby-oci8
gem install activerecord-oracle_enhanced-adapter
```

## database.yml
```
adapter: oracle_enhanced
database: SID
username: user_name
password: user_password
host: host
port: port

or

# use ora
adapter: oracle_enhanced
database: XXXXX_dev_tns # tnsnames.ora
username: user_name
password: user_password
```
