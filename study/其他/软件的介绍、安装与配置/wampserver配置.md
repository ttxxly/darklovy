### 修改 网站默认目录

1) 修改 Apache 的 httpd.conf 文件

有两处需要修改

```
DocumentRoot "F:\projects\php"
<Directory "F:\projects\php">
```
第一步完成之后， www目录依旧指向的是默认位置。这就需要修改wamp安装目录下的 wampmanager.tpl 和 wampmanager.ini 文件。

2) 修改 wampmanager.tpl 文件

```
Type: item; Caption: "${w_wwwDirectory}"; Action: shellexecute; FileName: "F:\projects\php"; Glyph: 2
```

3) 修改 wampmanager.ini 文件

```
Type: item; Caption: "www directory"; Action: shellexecute; FileName: "F:\projects\php"; Glyph: 2
```
