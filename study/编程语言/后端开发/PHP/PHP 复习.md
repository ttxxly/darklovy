## HTML

### 表单以及属性

### 输入框

### 按钮

* 普通按钮
* 提交按钮
* 重置按钮
* 图片按钮

### 图片

### 超级链接

### 表格 

<br >

<hr >
<img >



## PHP  

### 变量以及命令格式

### 判断相等 值相等 、 类型相等 （== 、  ===）

### 优先级 

```
$a = $a-=5; 
```

### 标记

```
<?
echo “hello,world”;
?>
```

### 运算符 

```
.
+=
=
```

### 数组

* 数组 
* 分类 range()
* 排序 (、 sort asort、 ksort array_multisort)
* 遍历 

```
list($a, $b) = range('a', 'b');
```

### 面向对象

* 特征：封装、 继承、 多态
* 封装： private、 public、 protected
* 对象属性和方法： ->

### 函数

* 自定义函数
* implode（）   、 explode（）
* 字母大小写转换： strtolow()   strtoupper()


### 会话状态

1. 启动会话（） 
2. 注册会话（ $_ssession['a'] = 'b'） 
3. 销毁会话（）
4. setcookie（） 设置过期时间


## MySQL

### 数据操作


```
mysql_comnnect()
mysql_select_db()
mysql_query()
mysql_fetch_row_object seet
mysql_close
mysql_free_restart()
```

### SQL  语句

1. 添加 
```
insert into 
```
2.删除
```
delete from
```
3. 修改
```
update
```
4. 查询

```
select from
```



### 其他

1. post 和 get 区别
2. 魔法方法
3. 验证码
4. require 和 include  -once（防止文件被多次包含）