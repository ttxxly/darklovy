## 方法一

我们首先需要知道的是在安全模式下以 root 账户启动 mysql 是不需要密码的。

### 停止 MySQL 服务

```shell
sudo service mysql stop  
```

### 以安全模式启动 MySQL

```shell
sudo mysqld_safe --skip-grant-tables --skip-networking &  
```

*注意：`--skip-networking`，避免远程无密码登录 MySQL。*

### 登录 root 账户重设密码

```shell
mysql -u root
mysql> use mysql;  
mysql> update user set password=PASSWORD("mynewpassword") where User='root';  
mysql> flush privileges;  
mysql > quit  
```

### 重启 MySQL

```shell
sudo service mysql restart  
```

## 方法二

如果你的数据库是为 wordpress 提供服务， 那么在 wp-config.php 配置文件中，会保存有密码。


