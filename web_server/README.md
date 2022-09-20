# Web Server
## Access Control CORS
> https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS

## test web page 效能
```
測試網頁的效能跟安全性，可用下面網址
https://gtmetrix.com/
https://developers.google.com/speed/pagespeed/insights/
```

## web gzip compress
```
## apache need mod_deflate mod_filter

<IfModule mod_deflate.c>
# Insert filters
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/xml
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE application/xml
AddOutputFilterByType DEFLATE application/xhtml+xml
AddOutputFilterByType DEFLATE application/rss+xml
AddOutputFilterByType DEFLATE application/javascript
AddOutputFilterByType DEFLATE application/x-javascript
AddOutputFilterByType DEFLATE application/x-httpd-php
AddOutputFilterByType DEFLATE application/x-httpd-fastphp
AddOutputFilterByType DEFLATE image/svg+xml

# Drop problematic browsers
BrowserMatch ^Mozilla/4 gzip-only-text/html
BrowserMatch ^Mozilla/4\.0[678] no-gzip
BrowserMatch \bMSI[E] !no-gzip !gzip-only-text/html

# Make sure proxies don't deliver the wrong content
Header append Vary User-Agent env=!dont-vary
</IfModule>
```

```
<IfModule mod_deflate.c>
<IfModule mod_headers.c>
Header append Vary User-Agent env=!dont-vary
</IfModule>
AddOutputFilterByType DEFLATE text/css text/x-component application/x-javascript application/javascript text/javascript text/x-js text/html text/richtext image/svg+xml text/plain text/xsd text/xsl text/xml image/x-icon application/json
<IfModule mod_mime.c>
# DEFLATE by extension
AddOutputFilter DEFLATE js css htm html xml
</IfModule>
</IfModule>
# END W3TC Browser Cache
# BEGIN WordPress
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /wordpress_pusa/
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /wordpress_pusa/index.php [L]
</IfModule>
```
