---
title: Java 面试题系列篇-SpringMVC 框架
date: 2018-10-20 18:15:02
tags: Java
---

## SpringMVC 框架

### 如何在Web项目中配置Spring MVC？ 

答：要使用Spring MVC需要在Web项目配置文件中配置其前端控制器DispatcherServlet，如下所示：

<web-app>

 

​    <servlet>

​        <servlet-name>example</servlet-name>

​        <servlet-class>

​            org.springframework.web.servlet.DispatcherServlet

​        </servlet-class>

​        <load-on-startup>1</load-on-startup>

​    </servlet>

 

​    <servlet-mapping>

​        <servlet-name>example</servlet-name>

​        <url-pattern>*.html</url-pattern>

​    </servlet-mapping>

 

</web-app>

说明：上面的配置中使用了*.html的后缀映射，这样做一方面不能够通过URL推断采用了何种服务器端的技术，另一方面可以欺骗搜索引擎，因为搜索引擎不会搜索动态页面，这种做法称为伪静态化。

### Spring MVC的工作原理是怎样的？ 

答：Spring MVC的工作原理如下图所示： 
① 客户端的所有请求都交给前端控制器DispatcherServlet来处理，它会负责调用系统的其他模块来真正处理用户的请求。 
② DispatcherServlet收到请求后，将根据请求的信息（包括URL、HTTP协议方法、请求头、请求参数、Cookie等）以及HandlerMapping的配置找到处理该请求的Handler（任何一个对象都可以作为请求的Handler）。 
③在这个地方Spring会通过HandlerAdapter对该处理器进行封装。 
④ HandlerAdapter是一个适配器，它用统一的接口对各种Handler中的方法进行调用。 
⑤ Handler完成对用户请求的处理后，会返回一个ModelAndView对象给DispatcherServlet，ModelAndView顾名思义，包含了数据模型以及相应的视图的信息。 
⑥ ModelAndView的视图是逻辑视图，DispatcherServlet还要借助ViewResolver完成从逻辑视图到真实视图对象的解析工作。 
⑦ 当得到真正的视图对象后，DispatcherServlet会利用视图对象对模型数据进行渲染。 
⑧ 客户端得到响应，可能是一个普通的HTML页面，也可以是XML或JSON字符串，还可以是一张图片或者一个PDF文件。

 

### 大型网站在架构上应当考虑哪些问题？ 

答： 

- 分层：分层是处理任何复杂系统最常见的手段之一，将系统横向切分成若干个层面，每个层面只承担单一的职责，然后通过下层为上层提供的基础设施和服务以及上层对下层的调用来形成一个完整的复杂的系统。计算机网络的开放系统互联参考模型（OSI/RM）和Internet的TCP/IP模型都是分层结构，大型网站的软件系统也可以使用分层的理念将其分为持久层（提供数据存储和访问服务）、业务层（处理业务逻辑，系统中最核心的部分）和表示层（系统交互、视图展示）。需要指出的是：（1）分层是逻辑上的划分，在物理上可以位于同一设备上也可以在不同的设备上部署不同的功能模块，这样可以使用更多的计算资源来应对用户的并发访问；（2）层与层之间应当有清晰的边界，这样分层才有意义，才更利于软件的开发和维护。 
- 分割：分割是对软件的纵向切分。我们可以将大型网站的不同功能和服务分割开，形成高内聚低耦合的功能模块（单元）。在设计初期可以做一个粗粒度的分割，将网站分割为若干个功能模块，后期还可以进一步对每个模块进行细粒度的分割，这样一方面有助于软件的开发和维护，另一方面有助于分布式的部署，提供网站的并发处理能力和功能的扩展。 
- 分布式：除了上面提到的内容，网站的静态资源（JavaScript、CSS、图片等）也可以采用独立分布式部署并采用独立的域名，这样可以减轻应用服务器的负载压力，也使得浏览器对资源的加载更快。数据的存取也应该是分布式的，传统的商业级关系型数据库产品基本上都支持分布式部署，而新生的NoSQL产品几乎都是分布式的。当然，网站后台的业务处理也要使用分布式技术，例如查询索引的构建、数据分析等，这些业务计算规模庞大，可以使用Hadoop以及MapReduce分布式计算框架来处理。 
- 集群：集群使得有更多的服务器提供相同的服务，可以更好的提供对并发的支持。 
- 缓存：所谓缓存就是用空间换取时间的技术，将数据尽可能放在距离计算最近的位置。使用缓存是网站优化的第一定律。我们通常说的CDN、反向代理、热点数据都是对缓存技术的使用。 
- 异步：异步是实现软件实体之间解耦合的又一重要手段。异步架构是典型的生产者消费者模式，二者之间没有直接的调用关系，只要保持数据结构不变，彼此功能实现可以随意变化而不互相影响，这对网站的扩展非常有利。使用异步处理还可以提高系统可用性，加快网站的响应速度（用Ajax加载数据就是一种异步技术），同时还可以起到削峰作用（应对瞬时高并发）。"；能推迟处理的都要推迟处理"是网站优化的第二定律，而异步是践行网站优化第二定律的重要手段。 
- 冗余：各种服务器都要提供相应的冗余服务器以便在某台或某些服务器宕机时还能保证网站可以正常工作，同时也提供了灾难恢复的可能性。冗余是网站高可用性的重要保证。

### 你用过的网站前端优化的技术有哪些？ 

答： 
① 浏览器访问优化： 

- 减少HTTP请求数量：合并CSS、合并JavaScript、合并图片（CSS Sprite） 
- 使用浏览器缓存：通过设置HTTP响应头中的Cache-Control和Expires属性，将CSS、JavaScript、图片等在浏览器中缓存，当这些静态资源需要更新时，可以更新HTML文件中的引用来让浏览器重新请求新的资源 
- 启用压缩 
- CSS前置，JavaScript后置 
- 减少Cookie传输 
  ② CDN加速：CDN（Content Distribute Network）的本质仍然是缓存，将数据缓存在离用户最近的地方，CDN通常部署在网络运营商的机房，不仅可以提升响应速度，还可以减少应用服务器的压力。当然，CDN缓存的通常都是静态资源。 
  ③ 反向代理：反向代理相当于应用服务器的一个门面，可以保护网站的安全性，也可以实现负载均衡的功能，当然最重要的是它缓存了用户访问的热点资源，可以直接从反向代理将某些内容返回给用户浏览器。

### 你使用过的应用服务器优化技术有哪些？ 

答： 
① 分布式缓存：缓存的本质就是内存中的哈希表，如果设计一个优质的哈希函数，那么理论上哈希表读写的渐近时间复杂度为O(1)。缓存主要用来存放那些读写比很高、变化很少的数据，这样应用程序读取数据时先到缓存中读取，如果没有或者数据已经失效再去访问数据库或文件系统，并根据拟定的规则将数据写入缓存。对网站数据的访问也符合二八定律（Pareto分布，幂律分布），即80%的访问都集中在20%的数据上，如果能够将这20%的数据缓存起来，那么系统的性能将得到显著的改善。当然，使用缓存需要解决以下几个问题： 

- 频繁修改的数据； 
- 数据不一致与脏读； 
- 缓存雪崩（可以采用分布式缓存服务器集群加以解决，memcached是广泛采用的解决方案）； 
- 缓存预热； 
- 缓存穿透（恶意持续请求不存在的数据）。 
  ② 异步操作：可以使用消息队列将调用异步化，通过异步处理将短时间高并发产生的事件消息存储在消息队列中，从而起到削峰作用。电商网站在进行促销活动时，可以将用户的订单请求存入消息队列，这样可以抵御大量的并发订单请求对系统和数据库的冲击。目前，绝大多数的电商网站即便不进行促销活动，订单系统都采用了消息队列来处理。 
  ③ 使用集群。 
  ④ 代码优化： 
- 多线程：基于Java的Web开发基本上都通过多线程的方式响应用户的并发请求，使用多线程技术在编程上要解决线程安全问题，主要可以考虑以下几个方面：A. 将对象设计为无状态对象（这和面向对象的编程观点是矛盾的，在面向对象的世界中被视为不良设计），这样就不会存在并发访问时对象状态不一致的问题。B. 在方法内部创建对象，这样对象由进入方法的线程创建，不会出现多个线程访问同一对象的问题。使用ThreadLocal将对象与线程绑定也是很好的做法，这一点在前面已经探讨过了。C. 对资源进行并发访问时应当使用合理的锁机制。 
- 非阻塞I/O： 使用单线程和非阻塞I/O是目前公认的比多线程的方式更能充分发挥服务器性能的应用模式，基于Node.js构建的服务器就采用了这样的方式。Java在JDK 1.4中就引入了NIO（Non-blocking I/O）,在Servlet 3规范中又引入了异步Servlet的概念，这些都为在服务器端采用非阻塞I/O提供了必要的基础。 
- 资源复用：资源复用主要有两种方式，一是单例，二是对象池，我们使用的数据库连接池、线程池都是对象池化技术，这是典型的用空间换取时间的策略，另一方面也实现对资源的复用，从而避免了不必要的创建和释放资源所带来的开销。

### 什么是XSS攻击？什么是SQL注入攻击？什么是CSRF攻击？

 答： 

- XSS（Cross Site Script，跨站脚本攻击）是向网页中注入恶意脚本在用户浏览网页时在用户浏览器中执行恶意脚本的攻击方式。跨站脚本攻击分有两种形式：反射型攻击（诱使用户点击一个嵌入恶意脚本的链接以达到攻击的目标，目前有很多攻击者利用论坛、微博发布含有恶意脚本的URL就属于这种方式）和持久型攻击（将恶意脚本提交到被攻击网站的数据库中，用户浏览网页时，恶意脚本从数据库中被加载到页面执行，QQ邮箱的早期版本就曾经被利用作为持久型跨站脚本攻击的平台）。XSS虽然不是什么新鲜玩意，但是攻击的手法却不断翻新，防范XSS主要有两方面：消毒（对危险字符进行转义）和HttpOnly（防范XSS攻击者窃取Cookie数据）。 
- SQL注入攻击是注入攻击最常见的形式（此外还有OS注入攻击（Struts 2的高危漏洞就是通过OGNL实施OS注入攻击导致的）），当服务器使用请求参数构造SQL语句时，恶意的SQL被嵌入到SQL中交给数据库执行。SQL注入攻击需要攻击者对数据库结构有所了解才能进行，攻击者想要获得表结构有多种方式：（1）如果使用开源系统搭建网站，数据库结构也是公开的（目前有很多现成的系统可以直接搭建论坛，电商网站，虽然方便快捷但是风险是必须要认真评估的）；（2）错误回显（如果将服务器的错误信息直接显示在页面上，攻击者可以通过非法参数引发页面错误从而通过错误信息了解数据库结构，Web应用应当设置友好的错误页，一方面符合最小惊讶原则，一方面屏蔽掉可能给系统带来危险的错误回显信息）；（3）盲注。防范SQL注入攻击也可以采用消毒的方式，通过正则表达式对请求参数进行验证，此外，参数绑定也是很好的手段，这样恶意的SQL会被当做SQL的参数而不是命令被执行，JDBC中的PreparedStatement就是支持参数绑定的语句对象，从性能和安全性上都明显优于Statement。 
- CSRF攻击（Cross Site Request Forgery，跨站请求伪造）是攻击者通过跨站请求，以合法的用户身份进行非法操作（如转账或发帖等）。CSRF的原理是利用浏览器的Cookie或服务器的Session，盗取用户身份，其原理如下图所示。防范CSRF的主要手段是识别请求者的身份，主要有以下几种方式：（1）在表单中添加令牌（token）；（2）验证码；（3）检查请求头中的Referer（前面提到防图片盗链接也是用的这种方式）。令牌和验证都具有一次消费性的特征，因此在原理上一致的，但是验证码是一种糟糕的用户体验，不是必要的情况下不要轻易使用验证码，目前很多网站的做法是如果在短时间内多次提交一个表单未获得成功后才要求提供验证码，这样会获得较好的用户体验。



补充：防火墙的架设是Web安全的重要保障，ModSecurity是开源的Web防火墙中的佼佼者。企业级防火墙的架设应当有两级防火墙，Web服务器和部分应用服务器可以架设在两级防火墙之间的DMZ，而数据和资源服务器应当架设在第二级防火墙之后。

### 什么是领域模型(domain model)？贫血模型(anaemic domain model)和充血模型(rich domain model)有什么区别？ 

答：领域模型是领域内的概念类或现实世界中对象的可视化表示，又称为概念模型或分析对象模型，它专注于分析问题领域本身，发掘重要的业务领域概念，并建立业务领域概念之间的关系。贫血模型是指使用的领域对象中只有setter和getter方法（POJO），所有的业务逻辑都不包含在领域对象中而是放在业务逻辑层。有人将我们这里说的贫血模型进一步划分成失血模型（领域对象完全没有业务逻辑）和贫血模型（领域对象有少量的业务逻辑），我们这里就不对此加以区分了。充血模型将大多数业务逻辑和持久化放在领域对象中，业务逻辑（业务门面）只是完成对业务逻辑的封装、事务和权限等的处理。下面两张图分别展示了贫血模型和充血模型的分层架构。

贫血模型 

充血模型 

贫血模型下组织领域逻辑通常使用事务脚本模式，让每个过程对应用户可能要做的一个动作，每个动作由一个过程来驱动。也就是说在设计业务逻辑接口的时候，每个方法对应着用户的一个操作，这种模式有以下几个有点： 

- 它是一个大多数开发者都能够理解的简单过程模型（适合国内的绝大多数开发者）。 
- 它能够与一个使用行数据入口或表数据入口的简单数据访问层很好的协作。 
- 事务边界的显而易见，一个事务开始于脚本的开始，终止于脚本的结束，很容易通过代理（或切面）实现声明式事务。 
  然而，事务脚本模式的缺点也是很多的，随着领域逻辑复杂性的增加，系统的复杂性将迅速增加，程序结构将变得极度混乱。开源中国社区上有一篇很好的译文《贫血领域模型是如何导致糟糕的软件产生》对这个问题做了比较细致的阐述。

### 谈一谈测试驱动开发（TDD）的好处以及你的理解。 

答：TDD是指在编写真正的功能实现代码之前先写测试代码，然后根据需要重构实现代码。在JUnit的作者Kent Beck的大作《测试驱动开发：实战与模式解析》（Test-Driven Development: by Example）一书中有这么一段内容：“消除恐惧和不确定性是编写测试驱动代码的重要原因”。因为编写代码时的恐惧会让你小心试探，让你回避沟通，让你羞于得到反馈，让你变得焦躁不安，而TDD是消除恐惧、让Java开发者更加自信更加乐于沟通的重要手段。TDD会带来的好处可能不会马上呈现，但是你在某个时候一定会发现，这些好处包括： 

- 更清晰的代码 — 只写需要的代码 
- 更好的设计 
- 更出色的灵活性 — 鼓励程序员面向接口编程 
- 更快速的反馈 — 不会到系统上线时才知道bug的存在

补充：敏捷软件开发的概念已经有很多年了，而且也部分的改变了软件开发这个行业，TDD也是敏捷开发所倡导的。

TDD可以在多个层级上应用，包括单元测试（测试一个类中的代码）、集成测试（测试类之间的交互）、系统测试（测试运行的系统）和系统集成测试（测试运行的系统包括使用的第三方组件）。TDD的实施步骤是：红（失败测试）- 绿（通过测试） - 重构。关于实施TDD的详细步骤请参考另一篇文章《测试驱动开发之初窥门径》。 
在使用TDD开发时，经常会遇到需要被测对象需要依赖其他子系统的情况，但是你希望将测试代码跟依赖项隔离，以保证测试代码仅仅针对当前被测对象或方法展开，这时候你需要的是测试替身。测试替身可以分为四类： 

- 虚设替身：只传递但是不会使用到的对象，一般用于填充方法的参数列表 
- 存根替身：总是返回相同的预设响应，其中可能包括一些虚设状态 
- 伪装替身：可以取代真实版本的可用版本（比真实版本还是会差很多） 
- 模拟替身：可以表示一系列期望值的对象，并且可以提供预设响应 
  Java世界中实现模拟替身的第三方工具非常多，包括EasyMock、Mockito、jMock等。



### 什么是可变参数？

可变参数允许调用参数数量不同的方法。请看下面例子中的求和方法。此方法可以调用1个int参数，或2个int参数，或多个int参数。

 

 //int(type) followed ... (three dot's) is syntax of a variable argument. 

​    public int sum(int... numbers) {

​        //inside the method a variable argument is similar to an array.

​        //number can be treated as if it is declared as int[] numbers;

​        int sum = 0;

​        for (int number: numbers) {

​            sum += number;

​        }

​        return sum;

​    }

 

​    public static void main(String[] args) {

​        VariableArgumentExamples example = new VariableArgumentExamples();

​        //3 Arguments

​        System.out.println(example.sum(1, 4, 5));//10

​        //4 Arguments

​        System.out.println(example.sum(1, 4, 5, 20));//30

​        //0 Arguments

​        System.out.println(example.sum());//0

}

 

### 断言的用途？

断言是在Java 1.4中引入的。它能让你验证假设。如果断言失败（即返回false），就会抛出AssertionError（如果启用断言）。基本断言如下所示。

 

private int computerSimpleInterest(int principal,float interest,int years){

​    assert(principal>0);

​    return 100;

}

 

### 什么时候使用断言？

断言不应该用于验证输入数据到一个public方法或命令行参数。IllegalArgumentException会是一个更好的选择。在public方法中，只用断言来检查它们根本不应该发生的情况。

 

### 什么是初始化数据块？

 

初始化数据块——当创建对象或加载类时运行的代码。

 

有两种类型的初始化数据块：

 

静态初始化器：加载类时运行的的代码

 

实例初始化器：创建新对象时运行的代码

 

### 什么是静态初始化器？

 

请看下面的例子：static{ 和 }之间的代码被称为静态初始化器。它只有在第一次加载类时运行。只有静态变量才可以在静态初始化器中进行访问。虽然创建了三个实例，但静态初始化器只运行一次。

 

/**

- Java学习交流QQ群：589809992 我们一起学Java！

 */

public class InitializerExamples {

​    static int count;

​    int i;

 

​    static{

​        //This is a static initializers. Run only when Class is first loaded.

​        //Only static variables can be accessed

​        System.out.println("Static Initializer");

​        //i = 6;//COMPILER ERROR

​        System.out.println("Count when Static Initializer is run is " + count);

​    }

 

​    public static void main(String[] args) {

​        InitializerExamples example = new InitializerExamples();

​        InitializerExamples example2 = new InitializerExamples();

​        InitializerExamples example3 = new InitializerExamples();

​    }

}

示例输出

 

Static Initializer

Count when Static Initializer is run is 0.

 

### 什么是实例初始化块？

 

让我们来看一个例子：每次创建类的实例时，实例初始化器中的代码都会运行。

 

/**

- Java学习交流QQ群：589809992 我们一起学Java！

 */

public class InitializerExamples {

​    static int count;

​    int i;

​    {

​        //This is an instance initializers. Run every time an object is created.

​        //static and instance variables can be accessed

​        System.out.println("Instance Initializer");

​        i = 6;

​        count = count + 1;

​        System.out.println("Count when Instance Initializer is run is " + count);

​    }

 

​    public static void main(String[] args) {

​        InitializerExamples example = new InitializerExamples();

​        InitializerExamples example1 = new InitializerExamples();

​        InitializerExamples example2 = new InitializerExamples();

​    }

}

示例输出

 

Instance Initializer

​      Count when Instance Initializer is run is 1

​      Instance Initializer

​      Count when Instance Initializer is run is 2

​      Instance Initializer

​      Count when Instance Initializer is run is 3

 

### 什么是正则表达式？

 

正则表达式能让解析、扫描和分割字符串变得非常容易。Java中常用的正则表达式——Patter，Matcher和Scanner类。

 

### 什么是令牌化？

 

令牌化是指在分隔符的基础上将一个字符串分割为若干个子字符串。例如，分隔符；分割字符串ac;bd;def;e为四个子字符串ac，bd，def和e。

 

分隔符自身也可以是一个常见正则表达式。

 

String.split(regex)函数将regex作为参数。

 

### 给出令牌化的例子？

 

private static void tokenize(String string,String regex) {

​    String[] tokens = string.split(regex);

​    System.out.println(Arrays.toString(tokens));

}

 

tokenize("ac;bd;def;e",";");//[ac, bd, def, e]

 

### 如何使用扫描器类（Scanner Class）令牌化？

 

private static void tokenizeUsingScanner(String string,String regex) {

​    Scanner scanner = new Scanner(string);

​    scanner.useDelimiter(regex);

​    List<String> matches = new ArrayList<String>();

​    while(scanner.hasNext()){

​        matches.add(scanner.next());

​    }

​    System.out.println(matches);

}

 

tokenizeUsingScanner("ac;bd;def;e",";");//[ac, bd, def, e]

 

### 如何添加小时(hour)到一个日期对象（Date Objects）？

 

现在，让我们如何看看添加小时到一个date对象。所有在date上的日期操作都需要通过添加毫秒到date才能完成。例如，如果我们想增加6个小时，那么我们需要将6小时换算成毫秒。6小时= 6  60  60 * 1000毫秒。请看以下的例子。

 

Date date = new Date();

 

//Increase time by 6 hrs

date.setTime(date.getTime() + 6 * 60 * 60 * 1000);

System.out.println(date);

 

//Decrease time by 6 hrs

date = new Date();

date.setTime(date.getTime() - 6 * 60 * 60 * 1000);

System.out.println(date);

 

### 如何格式化日期对象？

 

格式化日期需要使用DateFormat类完成。让我们看几个例子。

 

//Formatting Dates

System.out.println(DateFormat.getInstance().format(

​        date));//10/16/12 5:18 AM

带有区域设置的格式化日期如下所示：

 

System.out.println(DateFormat.getDateInstance(

​        DateFormat.FULL, new Locale("it", "IT"))

​        .format(date));//marted“ 16 ottobre 2012

 

System.out.println(DateFormat.getDateInstance(

​        DateFormat.FULL, Locale.ITALIAN)

​        .format(date));//marted“ 16 ottobre 2012

 

//This uses default locale US

System.out.println(DateFormat.getDateInstance(

​        DateFormat.FULL).format(date));//Tuesday, October 16, 2012

 

System.out.println(DateFormat.getDateInstance()

​        .format(date));//Oct 16, 2012

System.out.println(DateFormat.getDateInstance(

​        DateFormat.SHORT).format(date));//10/16/12

System.out.println(DateFormat.getDateInstance(

​        DateFormat.MEDIUM).format(date));//Oct 16, 2012

 

System.out.println(DateFormat.getDateInstance(

​        DateFormat.LONG).format(date));//October 16, 2012

 

### Java中日历类（Calendar Class）的用途？

 

Calendar类在Java中用于处理日期。Calendar类提供了增加和减少天数、月数和年数的简便方法。它还提供了很多与日期有关的细节（这一年的哪一天？哪一周？等等）

 

### 如何在Java中获取日历类（Calendar Class）的实例？

 

Calendar类不能通过使用new Calendar创建。得到Calendar类实例的最好办法是在Calendar中使用getInstance() static方法。

 

//Calendar calendar = new Calendar(); //COMPILER ERROR

Calendar calendar = Calendar.getInstance();

 

### 解释一些日历类（Calendar Class）中的重要方法？

 

在Calendar对象上设置日（day），月（month）或年（year）不难。对Day，Month或Year调用恰当Constant的set方法。下一个参数就是值。

 

calendar.set(Calendar.DATE, 24);

calendar.set(Calendar.MONTH, 8);//8 - September

calendar.set(Calendar.YEAR, 2010);

calendar get方法

 

要获取一个特定日期的信息——2010年9月24日。我们可以使用calendar get方法。已被传递的参数表示我们希望从calendar中获得的值—— 天或月或年或……你可以从calendar获取的值举例如下：

 

System.out.println(calendar.get(Calendar.YEAR));//2010

System.out.println(calendar.get(Calendar.MONTH));//8

System.out.println(calendar.get(Calendar.DATE));//24

System.out.println(calendar.get(Calendar.WEEK_OF_MONTH));//4

System.out.println(calendar.get(Calendar.WEEK_OF_YEAR));//39

System.out.println(calendar.get(Calendar.DAY_OF_YEAR));//267

System.out.println(calendar.getFirstDayOfWeek());//1 -> Calendar.SUNDAY

 

### 数字格式化类（Number Format Class）的用途？

 

数字格式用于格式化数字到不同的区域和不同格式中。

 

使用默认语言环境的数字格式

 

System.out.println(NumberFormat.getInstance().format(321.24f));//321.24

使用区域设置的数字格式

 

使用荷兰语言环境格式化数字：

 

System.out.println(NumberFormat.getInstance(new Locale("nl")).format(4032.3f));//4.032,3

使用德国语言环境格式化数字：

 

System.out.println(NumberFormat.getInstance(Locale.GERMANY).format(4032.3f));//4.032,3

使用默认语言环境格式化货币

 

System.out.println(NumberFormat.getCurrencyInstance().format(40324.31f));//$40,324.31

使用区域设置格式化货币

 

使用荷兰语言环境格式化货币：

 

System.out.println(NumberFormat.getCurrencyInstance(new Locale("nl")).format(40324.31f));/

 

### 后台从前端页面获取到表单数据的方法？请具体到细节，如Servlet如何接收？SpringMVC怎么接收或Structs2？

 

### Spring 中 IOC 和 DI 的区别以及关系是什么、AOP是怎么实现的？