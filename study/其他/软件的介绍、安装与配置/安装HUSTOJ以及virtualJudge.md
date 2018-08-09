### Ubuntu 14.04下 Apache修改网站的根目录以及默认网页

#### 修改根目录

在 `/etc/apache2/sites-available/000-default.conf` 中:

```
DocumentRoot /var/www/  # 修改成想要的目录，然后重启
```

#### 修改默认网页

在 `/etc/apache2/mods-available/dir.conf` 中

```
<IfModule mod_dir.c>
    DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm 
</IfModule>
```
