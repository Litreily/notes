# LNMP

## change root dir of nginx on centos-6.9

``` bash
# expect dir : /home/litreily/web/www/html

# update nginx config
$ sudo cat /etc/nginx/conf.d/default.conf
#
# The default server
#

server {
    listen       80 default_server;
    listen       [::]:80 default_server;
    server_name  127.0.0.1;

    root        /home/litreily/web/www/html;
    # Load configuration files for the default server block.
    include /etc/nginx/default.d/*.conf;

    location / {
        index index.php index.html index.htm;
    }

    error_page 404 /404.html;
        location = /40x.html {
    }

    error_page 500 502 503 504 /50x.html;
        location = /50x.html {
    }

    location ~ \.php$ {
        try_files       $uri =404;
        fastcgi_pass    127.0.0.1:9000;
        fastcgi_index   index.php;
        fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include         fastcgi_params;
        include         fastcgi.conf;
    }

}

# update php config, it's very important
$ sudo vi /etc/php-fpm.d/www/conf
user = litreily
group = litreily


# restart php server and nginx
$ sudo service php-fpm restart
$ sudo service nginx restart
```

ref: https://serverfault.com/questions/517190/nginx-1-fastcgi-sent-in-stderr-primary-script-unknown?newreg=be2687ea0ed343f6a32439c7b749a0f4
