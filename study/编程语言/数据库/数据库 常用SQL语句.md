```
SQL :
	结构化的查询语句
	作用：
		管理数据库.
SQL的分类
	DDL：数据定义语言
		操作对象：数据库和表
		关键词：create alter drop
	DML：数据操作语言
		操作对象：记录
	DQL：数据查询语言（非官方）
		
	DCL：数据控制语言
		操作对象：用户 事务 权限
		
////////////////////////////////////////////////////////////
登录数据库：
	mysql -uroot -p密码
DDL：数据定义语言
		操作对象：数据库和表
		关键词：create alter drop
	操作数据库：
		创建数据库：
			格式：
				create database 数据库名称;
		删除数据库：
			格式：
				drop database 数据库名称;
		常用的命令：
			查看所有的桑数据库：show databases;
	操作表：
		创建表
			格式：
				create table 表名(字段描述, 字段描述);
				字段描述：
					字段名称 字段类型 [约束]
				例如：
					create table user(
						id int primary key auto_increment, 
						username varchar(20)
					);
		修改表
			格式：
				alter table 表名 ...
			修改表名：
				alter table 旧表名 rename to 新表名;
			添加字段：
				alter table 表名 add [colum] 字段描述;
				例如：
					alter table user add password varchar(20);
			修改字段名：
				alter table 表名 change 字段名称 新字段描述;
				例如：
					alter table user change password pwd varchar(20);
			修改字段描述：
				alter table 表名 modify 字段名称 字段类型 [约束];
				例如：
					alter table user modify pwd int;
			删除字段
				alter table 表名 drop 字段名称;
				例如：
					alter table user drop pwd;
		删除表
			格式：
				drop table 表名;
		常用命令：
			切换或者进入数据库：use 数据库名称;
			查看当前数据库下的所有表：show tables;
			查看表结构：desc 表名;
			查看建表语句：show create table 表名;
			
///////////////////////////////////////////////////
DML: 数据操作语言
	操作对象：记录 (行)
	关键词：insert update delete
	插入：
		格式1：
			insert into 表名 values(字段值1, 字段值2....,字段值n);
			注意：
				默认插入全部字段，必须保证 values 后面的内容的类型和顺序和表结构中的一致。
				若字段类型为数字，可以省略引号。
			例如：
				insert into user values(1, 'tom');
				
		格式2：
			insert into 表名(字段名,字段名.....); values(字段值,字段值...);
			注意：
				插入指定的字段
				必须保证 values 后面的内容的类型顺序和表名后面的字段的类型和顺序保持一致。
			例如：
				insert into user (username, id) values('jack', 2);
	修改：
		格式：
			update 表名 set 字段名=字段值, 字段名=字段值..... [where 条件]；
			例如：
				update user set username='jerry' where username='jack';
	删除：
		格式：
			delete from 表名 [where 条件];
		例如：
			delete from user where id=2;
			
////////////////////////////////////////////////////
DQL: 数据查询语言
	操作对象：记录
	关键词：select
	格式：	
		select ... from 表名 where 条件 group by 分组字段 having 条件 order by 排序字段 ase|desc
		
	
	初始化环境：
	创建商品表
	create table products(
        pid int primary key auto_increment,
        pname varchar(20),
        price double,
        pnum int,
        cno int,
        pdate timestamp
	);

    insert into products values (null,'泰国大榴莲',98,12,1,null);
    insert into products values (null,'新疆大枣',38,123,1,null);
    insert into products values (null,'新疆切糕',68,50,2,null);
    insert into products values (null,'十三香',10,200,3,null);
    insert into products values (null,'老干妈',20,180,3,null);
    insert into products values (null,'豌豆黄',20,120,2,null);
    
    练习：
    简单查询:
     练习:
        1.查询所有的商品
        	select * from products;
        2.查询商品名和商品价格.	
        	查看指定的字段：
        		格式： select 字段名1,字段名2... from 表名
        	select pname,price from products;
        3.查询所有商品都有那些价格.
        	去重操作 distinct
        	格式：select distinct 字段名1,字段2 from 表名
        	select price from products;
        	select distinct price from products;
        4.将所有商品的价格+10元进行显示.(别名)
			可以在查询的结果之上进行运算，不影响数据库中的值。
			给字段取别名 
				格式：	字段名 [as] 别名
			select price+10 from products;
			select price+10 新价格 from products;
        条件查询:
        练习:
        1.查询商品名称为十三香的商品所有信息：
        	select * from products where pname='十三香';
        2.查询商品价格>60元的所有的商品信息:
        	select * from where price>60;
        3.查询商品名称中包含”新”的商品
        	模糊匹配 
        		格式：字段名称 like "匹配规则";
        		匹配规则：
        			1. 匹配个数	"_"	占个位置
        			2. 匹配内容 %
                    	"龙"				值为龙
                    	"%龙"			值以龙结尾
                    	"龙%"			值以龙开头
                    	"%龙%"			值包含龙
        	 
        4.查询价格为38,68,98的商品
        	select * from products where price=38 or price=68 or price=98;
        	select * from products where price in(38, 68, 98);
        	
        	where后的条件写法：
                * > ,<,=,>=,<=,<>, !=
                * like 使用占位符 _ 和 %  _代表一个字符 %代表任意个字符. 
                    * select * from product where pname like '%新%';
                * in在某个范围中获得值.
                    * select * from product where pid in (2,5,8);
                * between 较小值 and 较大值
                	select * from products where price between 50 and 70;
                	
                	
        排序查询:
            1.查询所有的商品，按价格进行排序.(asc-升序,desc-降序)
            	select * from products order by price;
            2.查询名称有新的商品的信息并且按价格降序排序.
				select * from products where pname like "%新%" order by price desc;

        聚合函数:
        	对一列进行计算。特点：忽略NULL值
            * sum(),avg(),max(),min(),count();
            1.获得所有商品的价格的总和：
            	select sum(price) from products;
            2.获得商品表中价格的平均数：
           		select avg(price) from products;
           		round(值,保留的小数位)
           		select round(avg(price), 2) from products;
            3.获得商品表中有多少条记录：
				select count(*) from products;
         分组：使用group by
            1.根据cno字段分组，分组后统计商品的个数.
            	select cno,count(*) from products group by cno;
            2.根据cno分组，分组统计每组商品的总数量，并且总数量> 200;
            	select cno,sum(pnum) t from products group by cno having t>200;  
               
              注意：
              	where 和 having 区别：
              		1. where 是对分组前的数据进行过滤。having 是对分组后的数据进行过滤。
              		2. where 后面不能使用 聚合函数  ，  having 可以，
```

