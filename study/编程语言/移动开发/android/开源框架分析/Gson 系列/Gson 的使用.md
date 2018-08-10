Gson 相关：

* https://github.com/google/gson
* https://sites.google.com/site/gson/

#### Gson 使用步骤

```
1. 添加依赖
	compile 'com.google.code.gson:gson:2.8.2'
	最新请访问：https://github.com/google/gson
2. 创建数据实体对象类
	确保Android studio 安装了 GsonFormat 插件
	在 我们创建的实体类中， Alt + Ins 选择 GsonFormat 粘贴JSON数据
3. 对获取到的JSON数据判空处理
4. 将JSON数据转化为实体类对象
	实体类 对象名称 = gson.fromJson(Json数据, 实体类名称.class);
	MyBooks myBooks = gson.fromJson(jsonString, MyBooks.class);
```




