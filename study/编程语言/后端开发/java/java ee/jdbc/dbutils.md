```
apache 组织提供的一个工具类，jdbc框架
dbutils的使用步骤
	1. 导入 jar 包
	2. 创建 QueryRunner
	3. 编写 SQL
	4. 执行 SQL
核心的类或者接口
	QueryRunner：类 操作SQL
		构造
			new QueryRunner(DataSource ds)
		常用的方法
			query(..) 查询
			update(...)	增删改
	DbUtils:类 释放资源和控制事务
	ResultSetHandler: 接口 封装结果集
		BeanHandler: 将查询的第一条结果封装成指定的Bean对象
		BeanListHandler:将查询的每一条结果封装成执行的bean对象，将所有的对象放入list中返回
		MaplistHandler:将查询的每一条结果封装成map,key是字段名，value是值，将所有的map放入list中返回
		ScalarHandler:针对于聚合函数
```

发表于：

* https://www.jianshu.com/p/65a346399ff5