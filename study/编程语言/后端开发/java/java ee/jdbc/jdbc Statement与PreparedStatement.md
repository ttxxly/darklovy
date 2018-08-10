```
作用：两者都是创建对象然后通过对象调用 executeQuery() 方法执行 sql 语句

注意：
	PreparedStatement效率更高
    	主要用于解决使用Statement对象多次执行同一SQL语句的效率问题
            在数据库支持预编译的情况下预先将SQL语句编译，
            当多次执行这条SQL语句时，可以直接执行编译好的SQL语句
	PreparedStatement更加安全
		PreparedStatement将sql变量抽离出sql语句，执行更加安全
		案例：
			select * from user where username = 'user' and userpwd = '' or '1' = '1';  
			select * from user where username= '"+varname+"' and userpwd='"+varpasswd+"'";
```

#### 相关面试题

```
1. 关于PreparedStatement与Statement描述错误的是（）
    A. 一般而言，PreparedStatement比Statement执行效率更高
    B. PreparedStatement会预编译SQL语句
    C. Statement每次都会解析/编译SQL，确立并优化数据获取路径
    D. Statement执行扫描的结果集比PreparedStatement大
    解析我觉得答案是 D 我没有找到答案啊
    	SQL 语句从数据库查询中获取数据，并将数据返回到结果集，同一SQL语句结果集应该是一样的。我觉得哈
    	
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79944520