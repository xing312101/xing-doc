# Nginx
## https ssl
```
http://nginx.org/en/docs/http/configuring_https_servers.html#chains
```

## proxy
```
upstream streamName {
# server unix:RailsPath/tmp/sockets/unicorn.sock;

server ip:port; // 127.0.0.1:8080
}


server {
	listen 80;
	server_name serverDomain; # www.google.com www.yahoo.com.tw 用空格區隔
	rewrite ^(.*) https://$host$1 permanent; # 用rewrite的方式轉成https
}


server {
	listen 443;
	server_name serverDomain;

	index index.html;
	ssl on;

	error_log /var/log/nginx/serverDomain-error.log;
	access_log /var/log/nginx/serverDomain-access.log;
	root RailsPath/public;
	ssl_protocols TLSv1.2 TLSv1.1 TLSv1;
	ssl_certificate /etc/nginx/ssl/serverDomain/gd_bundle.crt; #路徑隨意
	ssl_certificate_key /etc/nginx/ssl/serverDomain/ssl.key; #路徑隨意

	try_files $uri/index.html $uri.html $uri;

	location / {
		proxy_set_header X-Real-IP $remote_addr;
		proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
		proxy_set_header X-FORWARDED_PROTO https;
		proxy_set_header Host $http_host;
		proxy_redirect off;
		proxy_read_timeout 180;

		if ($request_uri ~* "\.(ico|css|js|gif|jpe?g|png)$") {
			expires max;
			break;
		}
		if ($request_uri ~* "\.(ico|css|js|gif|jpe?g|png)\?[0-9]+$") {
			expires max;
		break;
		}
		if (-f $request_filename) {
			break;
		}
		if (-f $request_filename/index.html) {
			rewrite (.*) $1/index.html break;
		}
		if (-f $request_filename.html) {
			rewrite (.*) $1.html break;
		}

		proxy_pass http://streamName;
	}

	error_page 500 502 503 504 /50x.html;

	location = /50x.html {
		root html;
	}
}
```

## sockjs-node proxy
> reference: https://stackoverflow.com/questions/40516288/webpack-dev-server-with-nginx-proxy-pass
```
location /sockjs-node {
    proxy_set_header X-Real-IP  $remote_addr;
    proxy_set_header X-Forwarded-For $remote_addr;
    proxy_set_header Host $host;

    proxy_pass http://node:8080;

    proxy_redirect off;

    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
}
```
