### Could not reliably determine the server's fully qualified domain name, using 127.0.0.1. Set the 'ServerName' directive globally to suppress this message

13.10 or newer：

```
sudo vi /etc/apache2/conf-available/servername.conf
```

在 servername.conf 中加入一行：

```
ServerName localhost
```

然后 

```
echo "ServerName localhost" | sudo tee /etc/apache2/conf-available/servername.conf
```

To activate the new configuration, you need to run:

```
service apache2 reload
```