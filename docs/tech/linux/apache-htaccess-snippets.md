# Apache Htaccess Snippets

```
# HTTP to HTTPS redirect
RewriteEngine On
RewriteCond %{HTTP:X-Forwarded-Proto} !https [NC]
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [R=301,L]
# redirect end
```