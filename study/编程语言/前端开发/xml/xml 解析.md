```
解析方式：
	1. sax
		特点：逐行解析，只能查询
	2. dom
		特点：一次性将文档加载到内存中，形成一颗dom树.就可以对dom树curd操作
解析技术：
	JAXP：sun公司提供支持DOM和SAX开包
	JDOM：dom4j兄弟
	jsoup：一种处理HTML特定解析开发包
	dom4j：比较常用的解析开发包，hibernate底层采用
dom4j
	进行查询操作
	使用步骤：
		1. 导入 jar 包
		2. 创建一个核心对象
			SAXReader
			document doc = new SAXReader().read(文件路径)
		3. 将 xml 文档加载到内存中形成一棵树
		4. 获取根节点
			Element root = doc.getRootElement();
		5. 通过根节点获取其他节点（文本节点、属性节点、元素节点）
			获取属性节点
				String value = root.attributeValue("属性名")
			获取所有的子元素
				List<Element> list = root.element()
			获取子元素的文本节点
				String text = ele.element("子元素名称")
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79944395