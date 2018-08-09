```
dom4j
	进行查询操作
	使用步骤：
		1. 导入 jar 包
			dom4j-1.6.1.jar
		2. 创建一个核心对象
			SAXReader reader = new SAXReader();
		3. 将 xml 文档加载到内存中形成一棵树
			Document doc = reader.read("F:\\projects\\java\\day08\\xml\\web.xml");
		4. 获取根节点
			Element root=doc.getRootElement();
		5. 通过根节点获取其他节点（文本节点、属性节点、元素节点）
            List<Element> list = root.elements();
            //遍历集合
            for (Element ele : list) {
                //获取servlet-name的标签体
                String text = ele.elementText("servlet-name");
                System.out.println(text);

                //获取url-pattern标签体
                System.out.println(ele.elementText("url-pattern"));
            }
            //获取root的version属性值
            String value = root.attributeValue("version");
            System.out.println(value);
```

#### 示例

```
1. web.xml 路径：F:\\projects\\java\\day08\\xml\\web.xml
    <?xml version="1.0" encoding="UTF-8"?>
    <web-app version="2.5">
        <servlet>
            <servlet-name>HelloMyServlet</servlet-name>
            <servlet-class>com.itheima.HelloMyServlet</servlet-class>
        </servlet>
        <servlet-mapping>
            <servlet-name>HelloMyServlet</servlet-name>
            <url-pattern>/hello</url-pattern>
        </servlet-mapping>
    </web-app>
2. Dom4jDemo.java 

    import java.util.List;

    import org.dom4j.Document;
    import org.dom4j.DocumentException;
    import org.dom4j.Element;
    import org.dom4j.io.SAXReader;

    public class Dom4jDemo {

        public static void main(String[] args) throws Exception {
            //创建核心对象
            SAXReader reader = new SAXReader();

            //获取dom树
            Document doc = reader.read("F:\\projects\\java\\day08\\xml\\web.xml");

            //获取根节点
            Element root=doc.getRootElement();

            //获取其他节点
            List<Element> list = root.elements();
            //遍历集合
            for (Element ele : list) {
                //获取servlet-name的标签体
                String text = ele.elementText("servlet-name");
                System.out.println(text);

                //获取url-pattern标签体
                System.out.println(ele.elementText("url-pattern"));
            }

            //获取root的version属性值
            String value = root.attributeValue("version");
            System.out.println(value);
        }
    }
```

发表于：

* https://blog.csdn.net/jdliyao/article/details/79944429