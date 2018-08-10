数据库连接池负责分配、管理和释放数据库连接，它允许应用程序重复使用一个现有的数据库连接，而不是再重新建立一个；释放空闲时间超过最大空闲时间的数据库连接来避免因为没有释放数据库连接而引起的数据库连接遗漏。这项技术能明显提高对数据库操作的性能。

```
必须实现 javax.sql.DataSource 接口
	获取连接：getConnection();
	归还连接：conn.close();
方法增前的方式：
	1. 继承
	2. 静态代理
	3. 动态代理
静态代理步骤：
	1. 要求装饰者和被装饰者实现同一个接口或者继承同一个类
	2. 要求装饰者要有被装饰者的引用
	3. 对需要加强的方法进行加强
	4. 对不需要加强的方法调用原来的方法
常见的连接池：
	1. DBCP
		使用步骤
			1. 导入 jar 包（两个 jar 包）
			2. 编码
				a. 硬编码
					new BasicDataSource()
				b. 配置文件
					Properties prop = new Properties()
					prop.load(is);
					new BasicDataSourceFactory().createDataSource(Properties prop);
	2. C3P0
		使用步骤
			1. 导入 jar 包（1个）
			2. 编码
				a. 配置文件
					配置文件的名称：c3p0.properties 或者c3p0-config.xml
					配置文件的位置：src 目录下
					编码中通过构造器创建
						new ComboPooledDataSource();
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79944502