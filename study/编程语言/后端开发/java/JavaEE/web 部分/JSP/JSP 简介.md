SP全称Java Server Pages，是一种动态网页开发技术。它使用JSP标签在HTML网页中插入Java代码。标签通常以<%开头以%>结束。

SP是一种Java servlet，主要用于实现Java web应用程序的用户界面部分。网页开发者们通过结合HTML代码、XHTML代码、XML元素以及嵌入JSP操作和命令来编写JSP。

JSP通过网页表单获取用户输入数据、访问数据库及其他数据源，然后动态地创建网页。

JSP标签有多种功能，比如访问数据库、记录用户选择信息、访问JavaBeans组件等，还可以在不同的网页中传递控制信息和共享信息。

#### 为什么是使用 JSP？

JSP 程序与 CGI 程序有着相似的功能， 但和 CGI 程序相比， JSP 程序有如下的优势：

* 性能更加的优越， 因为 JSP 可以直接在 HTML 网页中动态嵌入元素而不需要单独的引用 CGI 文件。
* 服务器调用的是已经编写好的 JSP 文件， 而不像 CGI/Perl 那样必须先载入解释器和目标脚本。
* JSP 基于 Java Servlet API， 因此， JSP 拥有各种强大的企业级 java API ，包括JDBC， JNDI， EJB，JAXP等。
* JSP 页面可以与处理业务逻辑的 servlet 一起使用，这种模式被 Java Servlet 模板引擎所支持。

JSP 是 JAVA EE 不可或缺的部分， 是一个完整的 企业应用平台。 这意味着 JSP 可以用简单的方式来实现最复杂的应用。



#### JSP 的优势

* 与 ASP 相比：有两大优势：
  * 动态部分用 java 编写，而不是VB 或者其他MS 专用语言，所以更加的强大和易用。
  * JSP 易于移植到非 MS 平台上。
* 与纯 Servlet 相比：JSP 可以很方便的编写和修改 HTML网页而不用面对大量的 Println 语句。
* 与 SSI(Struts2、Spring、 ibatis) 相比：SSI 无法使用表单数据，无法进行数据库连接。
* 与 JavaScript 相比：虽然 JavaScript 可以在客户端动态生成 HTML，但是很难与服务器进行交互，因此不能提供复杂的服务，比如访问数据库和图像处理等等。
* 与静态 HTML 相比：静态 HTML 不包含动态的信息