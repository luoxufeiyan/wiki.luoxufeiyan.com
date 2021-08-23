# Apache设置反向代理

例如将8080端口运行的程序代理到本机80端口上。

首先加载Apache模块。

```
a2enmod proxy proxy_balancer proxy_http
```

加载完之后重启一下Apache。

在`sites_available`文件夹下创建新的站点文件`project.luoxufeiyan.com.conf`：

```
<VirtualHost *:80>
    #配置站点的域名
    ServerName project.luoxufeiyan.com
    #配置站点的管理员信息
    ServerAdmin xxx@gmail.com

    #off表示开启反向代理，on表示开启正向代理
    ProxyRequests Off
    ProxyMaxForwards 100
    ProxyPreserveHost On
    
    #这里表示要将现在这个虚拟主机跳转到本机的8080端口
    ProxyPass / http://127.0.0.1:8080/
    ProxyPassReverse / http://127.0.0.1:8080/

    <Proxy *>
        Order Deny,Allow
        Allow from all
    </Proxy>
</VirtualHost>
```

随后通过 `a2ensite project.luoxufeiyan.com.conf`启动站点，重启一下Apache服务器，完毕。

例如ZeroNet的反代：
```
<IfModule mod_ssl.c>
<VirtualHost *:443>
	ServerName 010.fledding.com
	ServerAdmin webmaster@localhost
	DocumentRoot /var/www/010.fledding.com
        SSLEngine On

	# Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
	# error, crit, alert, emerg.
	# It is also possible to configure the loglevel for particular
	# modules, e.g.
	#LogLevel info ssl:warn

        RewriteEngine On
        RewriteCond %{HTTP:Upgrade} =websocket [NC]
        RewriteRule /(.*)           ws://localhost:43110/$1 [P,L]
        RewriteCond %{HTTP:Upgrade} !=websocket [NC]
	RewriteCond %{REQUEST_FILENAME} !-f
	RewriteCond %{REQUEST_FILENAME} !-d
        #RewriteRule /(.*)           http://localhost:43110/$1 [P,L]

	ProxyRequests Off
        ProxyMaxForwards 100
        ProxyPreserveHost On
        ProxyPass /  http://127.0.0.1:43110/
        ProxyPassReverse /  http://127.0.0.1:43110/

	#AllowEncodedSlashes On

        <Proxy *>
            Order Deny,Allow
            Allow from all
        </Proxy>


	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined

	SSLCertificateFile /etc/letsencrypt/live/010.fledding.com/fullchain.pem
	SSLCertificateKeyFile /etc/letsencrypt/live/010.fledding.com/privkey.pem
	Include /etc/letsencrypt/options-ssl-apache.conf

</VirtualHost>
</IfModule>
```