# let's Encrypt
> reference: https://letsencrypt.org/

> https://xenby.com/b/101-%E6%95%99%E5%AD%B8-%E7%94%B3%E8%AB%8Blets-encrypt%E6%86%91%E8%AD%89%E8%88%87%E5%95%9F%E7%94%A8https-nginx

## Step 1. install certbot
```
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install certbot
```

## Step 2. edit nginx config
```
$ sudo vim /etc/nginx/sites/sites-available/default # or another wanted

>>>>>

location ~ /.well-known {
	allow all;
}

<<<<<

$ sudo service nginx reload

```

## Step 3. apply a certificate
```
$ sudo certbot certonly --webroot --webroot-path=/var/www/projectDir -d domain.com -d www.domain.com -d subDomainName.domain.com

next step will key email.
if would not enter email, add parameter: –register-unsafely-without-email
it will put file at /etc/letsencrypt/live/www.domain.com/fullchain.pem
```

## Step 4. create a 2048-bit Diffie-Hellman combine for getting more security
```
$ sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
it will at /etc/ssl/certs/dhparam.pem
```

## Step 5. set up ssl-domain.com.conf
```
$ sudo vim /etc/nginx/snippets/ssl-domain.com.conf

>>>>>

ssl_certificate /etc/letsencrypt/live/domain.com/fullchain.pem;
ssl_certificate_key /etc/letsencrypt/live/domain.com/privkey.pem;

<<<<<

```

## Step 6. apply diffie-hellman
```
$ sudo vim /etc/nginx/snippets/ssl-params.conf

>>>>>

ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_prefer_server_ciphers on;
ssl_ciphers "EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH";
ssl_ecdh_curve secp384r1;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off;
ssl_stapling on;
ssl_stapling_verify on;
resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 5s;
add_header X-Frame-Options DENY;
add_header X-Content-Type-Options nosniff;
ssl_dhparam /etc/ssl/certs/dhparam.pem;

<<<<<

```
其中的8.8.8.8 8.8.4.4與/etc/ssl/certs/dhparam.pem可以依據自己使用不同做設定

8.8.8.8 8.8.4.4 為Google DNS的IP 假如要使用別的DNS就改成自己使用的DNS IP

而/etc/ssl/certs/dhparam.pem是剛剛產生的2048-bit Diffie-Hellman的密碼組合位置 如果你在產生時不是放在此路徑 就修改這個選項


## Step 7. enable ssl
### method 1 using return
```
listen 443 ssl http2 default_server;
listen [::]:443 ssl http2 default_server;
include snippets/ssl-domain.com.conf;
include snippets/ssl-params.conf;

server {
    listen 80 default_server;
    listen [::]:80 default_server;
    server_name domain.com www.domain.com;
    return 301 https://$server_name$request_uri;
}

```
### method 2 using rewrite (recommend)
```
rewrite ^(.*) https://$host$1 permanent;
```


## Auto update cerfiticate
```
$ sudo crontab -e
* * */7 * * /usr/bin/certbot renew --quiet --renew-hook "/bin/systemctl reload nginx"
```


## Delete Certbot Certificate by Domain Name
```
sudo certbot delete --cert-name www.domain.com
```




