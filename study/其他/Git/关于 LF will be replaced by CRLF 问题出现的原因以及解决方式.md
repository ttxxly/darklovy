本文主要写了在 Hexo 博客中 出现 LF will be replaced by CRLF 的原因以及它的解决方式。

##### 出现的原因

```
1. windows中的换行符为 CRLF，而在Linux下的换行符为LF，所以在执行add . 时出现提示 
2. CRLF和LF是两种不同的换行格式，git工作区默认为CRLF来作为换行符，
    所以当我们项目文件里有用的地方使用LF作为换行符，这个时候我们再继续git add
    或者git commit的时候就会弹出警告，
    当最终push到远程仓库的时候git会统一格式全部转化为用CRLF作为换行符 
```

##### 解决方式

```
1. 这个只是一个警告，我们直接忽略就好。
2. git config –global core.autocrlf false //禁用自动转换 
```

##### 发表地址

* https://blog.csdn.net/jdliyao/article/details/81412527

##### 发表时间

```
2018年8月4日16:39:27
```

