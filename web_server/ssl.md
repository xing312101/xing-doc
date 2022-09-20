# SSL
## openssl
```
$sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt

req：使用 X.509 Certificate Signing Request（CSR） Management 產生憑證。
-x509：建立自行簽署的憑證。
-nodes：不要使用密碼保護，因為這個憑證是 NGINX 伺服器要使用的，如果設定密碼的話，會讓伺服器每次在啟動時書需要輸入密碼。
-days 365：設定憑證的使用期限，單位是天，如果不想時常重新產生憑證，可以設長一點。
-newkey rsa:2048：同時產生新的 RSA 2048 位元的金鑰。
-keyout：設定金鑰儲存的位置。
-out：設定憑證儲存的位置。
```
## 展期 crt bundle crt chained
```
https://www.godaddy.com/help/nginx-install-a-certificate-6722?v=1
http://nginx.org/en/docs/http/configuring_https_servers.html#chains

$ cat www.example.com.crt bundle.crt > www.example.com.chained.crt
```


