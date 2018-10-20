---
title: Java 面试题系列篇-Spring 框架
date: 2018-10-20 18:14:37
tags: Java
---

## Spring 框架

### 【Spring】使用Spring框架的好处是什么？

轻量：Spring 是轻量的，基本的版本大约2MB

 

控制反转：Spring通过控制反转实现了松散耦合，对象们给出它们的依赖，而不是创建或查找依赖的对象们

 

面向切面的编程(AOP)：Spring支持面向切面的编程，并且把应用业务逻辑和系统服务分开

 

容器：Spring 包含并管理应用中对象的生命周期和配置

 

MVC框架：Spring的WEB框架是个精心设计的框架，是Web框架的一个很好的替代品

 

事务管理：Spring 提供一个持续的事务管理接口，可以扩展到上至本地事务下至全局事务（JTA）

 

异常处理：Spring 提供方便的API把具体技术相关的异常（比如由JDBC，Hibernate or JDO抛出的）转化为一致的unchecked 异常

### 什么是IoC和DI？DI是如何实现的？ 

答：IoC叫控制反转，是Inversion of Control的缩写，DI（Dependency Injection）叫依赖注入，是对IoC更简单的诠释。控制反转是把传统上由程序代码直接操控的对象的调用权交给容器，通过容器来实现对象组件的装配和管理。所谓的"控制反转"就是对组件对象控制权的转移，从程序代码本身转移到了外部容器，由容器来创建对象并管理对象之间的依赖关系。IoC体现了好莱坞原则 - "Don’t call me, we will call you"。依赖注入的基本原则是应用组件不应该负责查找资源或者其他依赖的协作对象。配置对象的工作应该由容器负责，查找资源的逻辑应该从应用组件的代码中抽取出来，交给容器来完成。DI是对IoC更准确的描述，即组件之间的依赖关系由容器在运行期决定，形象的来说，即由容器动态的将某种依赖关系注入到组件之中。

举个例子：一个类A需要用到接口B中的方法，那么就需要为类A和接口B建立关联或依赖关系，最原始的方法是在类A中创建一个接口B的实现类C的实例，但这种方法需要开发人员自行维护二者的依赖关系，也就是说当依赖关系发生变动的时候需要修改代码并重新构建整个系统。如果通过一个容器来管理这些对象以及对象的依赖关系，则只需要在类A中定义好用于关联接口B的方法（构造器或setter方法），将类A和接口B的实现类C放入容器中，通过对容器的配置来实现二者的关联。

依赖注入可以通过setter方法注入（设值注入）、构造器注入和接口注入三种方式来实现，Spring支持setter注入和构造器注入，通常使用构造器注入来注入必须的依赖关系，对于可选的依赖关系，则setter注入是更好的选择，setter注入需要类提供无参构造器或者无参的静态工厂方法来创建对象。

### Spring中Bean的作用域有哪些？ 

答：在Spring的早期版本中，仅有两个作用域：singleton和prototype，前者表示Bean以单例的方式存在；后者表示每次从容器中调用Bean时，都会返回一个新的实例，prototype通常翻译为原型。

补充：设计模式中的创建型模式中也有一个原型模式，原型模式也是一个常用的模式，例如做一个室内设计软件，所有的素材都在工具箱中，而每次从工具箱中取出的都是素材对象的一个原型，可以通过对象克隆来实现原型模式。

Spring 2.x中针对WebApplicationContext新增了3个作用域，分别是：request（每次HTTP请求都会创建一个新的Bean）、session（同一个HttpSession共享同一个Bean，不同的HttpSession使用不同的Bean）和globalSession（同一个全局Session共享一个Bean）。

说明：单例模式和原型模式都是重要的设计模式。一般情况下，无状态或状态不可变的类适合使用单例模式。在传统开发中，由于DAO持有Connection这个非线程安全对象因而没有使用单例模式；但在Spring环境下，所有DAO类对可以采用单例模式，因为Spring利用AOP和Java API中的ThreadLocal对非线程安全的对象进行了特殊处理。

ThreadLocal为解决多线程程序的并发问题提供了一种新的思路。ThreadLocal，顾名思义是线程的一个本地化对象，当工作于多线程中的对象使用ThreadLocal维护变量时，ThreadLocal为每个使用该变量的线程分配一个独立的变量副本，所以每一个线程都可以独立的改变自己的副本，而不影响其他线程所对应的副本。从线程的角度看，这个变量就像是线程的本地变量。

ThreadLocal类非常简单好用，只有四个方法，能用上的也就是下面三个方法： 

- void set(T value)：设置当前线程的线程局部变量的值。 
- T get()：获得当前线程所对应的线程局部变量的值。 
- void remove()：删除当前线程中线程局部变量的值。

ThreadLocal是如何做到为每一个线程维护一份独立的变量副本的呢？在ThreadLocal类中有一个Map，键为线程对象，值是其线程对应的变量的副本，自己要模拟实现一个ThreadLocal类其实并不困难，代码如下所示：

import java.util.Collections;

import java.util.HashMap;

import java.util.Map;

 

public class MyThreadLocal<T> {

​    private Map<Thread, T> map = Collections.synchronizedMap(new HashMap<Thread, T>());

 

​    public void set(T newValue) {

​        map.put(Thread.currentThread(), newValue);

​    }

 

​    public T get() {

​        return map.get(Thread.currentThread());

​    }

 

​    public void remove() {

​        map.remove(Thread.currentThread());

​    }

}

### 解释一下什么叫AOP（面向切面编程）？ 

答：AOP（Aspect-Oriented Programming）指一种程序设计范型，该范型以一种称为切面（aspect）的语言构造为基础，切面是一种新的模块化机制，用来描述分散在对象、类或方法中的横切关注点（crosscutting concern）。

### 你是如何理解"横切关注"这个概念的？ 

答："横切关注"是会影响到整个应用程序的关注功能，它跟正常的业务逻辑是正交的，没有必然的联系，但是几乎所有的业务逻辑都会涉及到这些关注功能。通常，事务、日志、安全性等关注就是应用中的横切关注功能。

### 你如何理解AOP中的连接点（Joinpoint）、切点（Pointcut）、增强（Advice）、引介（Introduction）、织入（Weaving）、切面（Aspect）这些概念？ 

答： 
a. 连接点（Joinpoint）：程序执行的某个特定位置（如：某个方法调用前、调用后，方法抛出异常后）。一个类或一段程序代码拥有一些具有边界性质的特定点，这些代码中的特定点就是连接点。Spring仅支持方法的连接点。 
b. 切点（Pointcut）：如果连接点相当于数据中的记录，那么切点相当于查询条件，一个切点可以匹配多个连接点。Spring AOP的规则解析引擎负责解析切点所设定的查询条件，找到对应的连接点。 
c. 增强（Advice）：增强是织入到目标类连接点上的一段程序代码。Spring提供的增强接口都是带方位名的，如：BeforeAdvice、AfterReturningAdvice、ThrowsAdvice等。很多资料上将增强译为“通知”，这明显是个词不达意的翻译，让很多程序员困惑了许久。

说明： Advice在国内的很多书面资料中都被翻译成"通知"，但是很显然这个翻译无法表达其本质，有少量的读物上将这个词翻译为"增强"，这个翻译是对Advice较为准确的诠释，我们通过AOP将横切关注功能加到原有的业务逻辑上，这就是对原有业务逻辑的一种增强，这种增强可以是前置增强、后置增强、返回后增强、抛异常时增强和包围型增强。

d. 引介（Introduction）：引介是一种特殊的增强，它为类添加一些属性和方法。这样，即使一个业务类原本没有实现某个接口，通过引介功能，可以动态的未该业务类添加接口的实现逻辑，让业务类成为这个接口的实现类。 
e. 织入（Weaving）：织入是将增强添加到目标类具体连接点上的过程，AOP有三种织入方式：①编译期织入：需要特殊的Java编译期（例如AspectJ的ajc）；②装载期织入：要求使用特殊的类加载器，在装载类的时候对类进行增强；③运行时织入：在运行时为目标类生成代理实现增强。Spring采用了动态代理的方式实现了运行时织入，而AspectJ采用了编译期织入和装载期织入的方式。 
f. 切面（Aspect）：切面是由切点和增强（引介）组成的，它包括了对横切关注功能的定义，也包括了对连接点的定义。

补充：代理模式是GoF提出的23种设计模式中最为经典的模式之一，代理模式是对象的结构模式，它给某一个对象提供一个代理对象，并由代理对象控制对原对象的引用。简单的说，代理对象可以完成比原对象更多的职责，当需要为原对象添加横切关注功能时，就可以使用原对象的代理对象。我们在打开Office系列的Word文档时，如果文档中有插图，当文档刚加载时，文档中的插图都只是一个虚框占位符，等用户真正翻到某页要查看该图片时，才会真正加载这张图，这其实就是对代理模式的使用，代替真正图片的虚框就是一个虚拟代理；Hibernate的load方法也是返回一个虚拟代理对象，等用户真正需要访问对象的属性时，才向数据库发出SQL语句获得真实对象。

下面用一个找枪手代考的例子演示代理模式的使用：

/**

- 参考人员接口
- @author 骆昊

 *

 */

public interface Candidate {

 

​    /**

​     * 答题

​     */

​    public void answerTheQuestions();

}

/**

- 懒学生
- @author 骆昊

 *

 */

public class LazyStudent implements Candidate {

​    private String name;        // 姓名

 

​    public LazyStudent(String name) {

​        this.name = name;

​    }

 

​    @Override

​    public void answerTheQuestions() {

​        // 懒学生只能写出自己的名字不会答题

​        System.out.println("姓名: " + name);

​    }

 

}

/**

- 枪手
- @author 骆昊

 *

 */

public class Gunman implements Candidate {

​    private Candidate target;   // 被代理对象

 

​    public Gunman(Candidate target) {

​        this.target = target;

​    }

 

​    @Override

​    public void answerTheQuestions() {

​        // 枪手要写上代考的学生的姓名

​        target.answerTheQuestions();

​        // 枪手要帮助懒学生答题并交卷

​        System.out.println("奋笔疾书正确答案");

​        System.out.println("交卷");

​    }

 

}

public class ProxyTest1 {

 

​    public static void main(String[] args) {

​        Candidate c = new Gunman(new LazyStudent("王小二"));

​        c.answerTheQuestions();

​    }

}

说明：从JDK 1.3开始，Java提供了动态代理技术，允许开发者在运行时创建接口的代理实例，主要包括Proxy类和InvocationHandler接口。下面的例子使用动态代理为ArrayList编写一个代理，在添加和删除元素时，在控制台打印添加或删除的元素以及ArrayList的大小：

import java.lang.reflect.InvocationHandler;

import java.lang.reflect.Method;

import java.util.List;

 

public class ListProxy<T> implements InvocationHandler {

​    private List<T> target;

 

​    public ListProxy(List<T> target) {

​        this.target = target;

​    }

 

​    @Override

​    public Object invoke(Object proxy, Method method, Object[] args)

​            throws Throwable {

​        Object retVal = null;

​        System.out.println("[" + method.getName() + ": " + args[0] + "]");

​        retVal = method.invoke(target, args);

​        System.out.println("[size=" + target.size() + "]");

​        return retVal;

​    }

 

}

 

import java.lang.reflect.Proxy;

import java.util.ArrayList;

import java.util.List;

 

public class ProxyTest2 {

 

​    @SuppressWarnings("unchecked")

​    public static void main(String[] args) {

​        List<String> list = new ArrayList<String>();

​        Class<?> clazz = list.getClass();

​        ListProxy<String> myProxy = new ListProxy<String>(list);

​        List<String> newList = (List<String>) 

​                Proxy.newProxyInstance(clazz.getClassLoader(), 

​                clazz.getInterfaces(), myProxy);

​        newList.add("apple");

​        newList.add("banana");

​        newList.add("orange");

​        newList.remove("banana");

​    }

}

说明：使用Java的动态代理有一个局限性就是代理的类必须要实现接口，虽然面向接口编程是每个优秀的Java程序都知道的规则，但现实往往不尽如人意，对于没有实现接口的类如何为其生成代理呢？继承！继承是最经典的扩展已有代码能力的手段，虽然继承常常被初学者滥用，但继承也常常被进阶的程序员忽视。CGLib采用非常底层的字节码生成技术，通过为一个类创建子类来生成代理，它弥补了Java动态代理的不足，因此Spring中动态代理和CGLib都是创建代理的重要手段，对于实现了接口的类就用动态代理为其生成代理类，而没有实现接口的类就用CGLib通过继承的方式为其创建代理。

### Spring中自动装配的方式有哪些？

 答： 

- no：不进行自动装配，手动设置Bean的依赖关系。 
- byName：根据Bean的名字进行自动装配。 
- byType：根据Bean的类型进行自动装配。 
- constructor：类似于byType，不过是应用于构造器的参数，如果正好有一个Bean与构造器的参数类型相同则可以自动装配，否则会导致错误。 
- autodetect：如果有默认的构造器，则通过constructor的方式进行自动装配，否则使用byType的方式进行自动装配。

说明：自动装配没有自定义装配方式那么精确，而且不能自动装配简单属性（基本类型、字符串等），在使用时应注意。

### Spring中如何使用注解来配置Bean？有哪些相关的注解？ 

答：首先需要在Spring配置文件中增加如下配置：

<context:component-scan base-package="org.example"/>

然后可以用@Component、@Controller、@Service、@Repository注解来标注需要由Spring IoC容器进行对象托管的类。这几个注解没有本质区别，只不过@Controller通常用于控制器，@Service通常用于业务逻辑类，@Repository通常用于仓储类（例如我们的DAO实现类），普通的类用@Component来标注。

### Spring支持的事务管理类型有哪些？你在项目中使用哪种方式？ 

答：Spring支持编程式事务管理和声明式事务管理。许多Spring框架的用户选择声明式事务管理，因为这种方式和应用程序的关联较少，因此更加符合轻量级容器的概念。声明式事务管理要优于编程式事务管理，尽管在灵活性方面它弱于编程式事务管理，因为编程式事务允许你通过代码控制业务。

事务分为全局事务和局部事务。全局事务由应用服务器管理，需要底层服务器JTA支持（如WebLogic、WildFly等）。局部事务和底层采用的持久化方案有关，例如使用JDBC进行持久化时，需要使用Connetion对象来操作事务；而采用Hibernate进行持久化时，需要使用Session对象来操作事务。

Spring提供了如下所示的事务管理器。

| 事务管理器实现类                    | 目标对象            |
| ----------------------------------- | ------------------- |
| DataSourceTransactionManager        | 注入DataSource      |
| HibernateTransactionManager         | 注入SessionFactory  |
| JdoTransactionManager               | 管理JDO事务         |
| JtaTransactionManager               | 使用JTA管理事务     |
| PersistenceBrokerTransactionManager | 管理Apache的OJB事务 |

这些事务的父接口都是PlatformTransactionManager。Spring的事务管理机制是一种典型的策略模式，PlatformTransactionManager代表事务管理接口，该接口定义了三个方法，该接口并不知道底层如何管理事务，但是它的实现类必须提供getTransaction()方法（开启事务）、commit()方法（提交事务）、rollback()方法（回滚事务）的多态实现，这样就可以用不同的实现类代表不同的事务管理策略。使用JTA全局事务策略时，需要底层应用服务器支持，而不同的应用服务器所提供的JTA全局事务可能存在细节上的差异，因此实际配置全局事务管理器是可能需要使用JtaTransactionManager的子类，如：WebLogicJtaTransactionManager（Oracle的WebLogic服务器提供）、UowJtaTransactionManager（IBM的WebSphere服务器提供）等。

编程式事务管理如下所示。

<?xml version="1.0" encoding="UTF-8"?>

 <beans xmlns="http://www.springframework.org/schema/beans"

​     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  xmlns:p="http://www.springframework.org/schema/p"

​    xmlns:p="http://www.springframework.org/schema/context"

​     xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd

​     http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

 

​     <context:component-scan base-package="com.jackfrued"/>

 

​     <bean id="propertyConfig"

​         class="org.springframework.beans.factory.config.

  PropertyPlaceholderConfigurer">

​         <property name="location">

​             <value>jdbc.properties</value>

​         </property>

​     </bean>

 

​     <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">

​         <property name="driverClassName">

​             <value>${db.driver}</value>

​         </property>

​         <property name="url">

​             <value>${db.url}</value>

​         </property>

​         <property name="username">

​             <value>${db.username}</value>

​         </property>

​         <property name="password">

​             <value>${db.password}</value>

​         </property>

​     </bean>

 

​     <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate">

​         <property name="dataSource">

​             <ref bean="dataSource" />

​         </property>

​     </bean>

 

​     <!-- JDBC事务管理器 -->

​     <bean id="transactionManager"

​         class="org.springframework.jdbc.datasource.

​       DataSourceTransactionManager"　scope="singleton">

​         <property name="dataSource">

​             <ref bean="dataSource" />

​         </property>

​     </bean>

 

​     <!-- 声明事务模板 -->

​     <bean id="transactionTemplate"

​         class="org.springframework.transaction.support.

   TransactionTemplate">

​         <property name="transactionManager">

​             <ref bean="transactionManager" />

​         </property>

​     </bean>

 

</beans>

package com.jackfrued.dao.impl;

 

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.jdbc.core.JdbcTemplate;

 

import com.jackfrued.dao.EmpDao;

import com.jackfrued.entity.Emp;

 

@Repository

public class EmpDaoImpl implements EmpDao {

​    @Autowired

​    private JdbcTemplate jdbcTemplate;

 

​    @Override

​    public boolean save(Emp emp) {

​        String sql = "insert into emp values (?,?,?)";

​        return jdbcTemplate.update(sql, emp.getId(), emp.getName(), emp.getBirthday()) == 1;

​    }

 

}

package com.jackfrued.biz.impl;

 

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.stereotype.Service;

import org.springframework.transaction.TransactionStatus;

import org.springframework.transaction.support.TransactionCallbackWithoutResult;

import org.springframework.transaction.support.TransactionTemplate;

 

import com.jackfrued.biz.EmpService;

import com.jackfrued.dao.EmpDao;

import com.jackfrued.entity.Emp;

 

@Service

public class EmpServiceImpl implements EmpService {

​    @Autowired

​    private TransactionTemplate txTemplate;

​    @Autowired

​    private EmpDao empDao;

 

​    @Override

​    public void addEmp(final Emp emp) {

​        txTemplate.execute(new TransactionCallbackWithoutResult() {

 

​            @Override

​            protected void doInTransactionWithoutResult(TransactionStatus txStatus) {

​                empDao.save(emp);

​            }

​        });

​    }

 

 

}

声明式事务如下图所示，以Spring整合Hibernate 3为例，包括完整的DAO和业务逻辑代码。

<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"

​    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 

​    xmlns:p="http://www.springframework.org/schema/p"

​    xmlns:context="http://www.springframework.org/schema/context"

​    xmlns:aop="http://www.springframework.org/schema/aop" 

​    xmlns:tx="http://www.springframework.org/schema/tx"

​    xsi:schemaLocation="http://www.springframework.org/schema/beans

​           http://www.springframework.org/schema/beans/spring-beans-3.2.xsd

​           http://www.springframework.org/schema/context

​           http://www.springframework.org/schema/context/spring-context-3.2.xsd

​           http://www.springframework.org/schema/aop

​           http://www.springframework.org/schema/aop/spring-aop-3.2.xsd

​           http://www.springframework.org/schema/tx

​           http://www.springframework.org/schema/tx/spring-tx-3.2.xsd">

 

​    <!-- 配置由Spring IoC容器托管的对象对应的被注解的类所在的包 -->

​    <context:component-scan base-package="com.jackfrued" />

 

​    <!-- 配置通过自动生成代理实现AOP功能 -->

​    <aop:aspectj-autoproxy />

 

​    <!-- 配置数据库连接池 (DBCP) -->

​    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"

​        destroy-method="close">

​        <!-- 配置驱动程序类 -->

​        <property name="driverClassName" value="com.mysql.jdbc.Driver" />

​        <!-- 配置连接数据库的URL -->

​        <property name="url" value="jdbc:mysql://localhost:3306/myweb" />

​        <!-- 配置访问数据库的用户名 -->

​        <property name="username" value="root" />

​        <!-- 配置访问数据库的口令 -->

​        <property name="password" value="123456" />

​        <!-- 配置最大连接数 -->

​        <property name="maxActive" value="150" />

​        <!-- 配置最小空闲连接数 -->

​        <property name="minIdle" value="5" />

​        <!-- 配置最大空闲连接数 -->

​        <property name="maxIdle" value="20" />

​        <!-- 配置初始连接数 -->

​        <property name="initialSize" value="10" />

​        <!-- 配置连接被泄露时是否生成日志 -->

​        <property name="logAbandoned" value="true" />

​        <!-- 配置是否删除超时连接 -->

​        <property name="removeAbandoned" value="true" />

​        <!-- 配置删除超时连接的超时门限值(以秒为单位) -->

​        <property name="removeAbandonedTimeout" value="120" />

​        <!-- 配置超时等待时间(以毫秒为单位) -->

​        <property name="maxWait" value="5000" />

​        <!-- 配置空闲连接回收器线程运行的时间间隔(以毫秒为单位) -->

​        <property name="timeBetweenEvictionRunsMillis" value="300000" />

​        <!-- 配置连接空闲多长时间后(以毫秒为单位)被断开连接 -->

​        <property name="minEvictableIdleTimeMillis" value="60000" />

​    </bean>

 

​    <!-- 配置Spring提供的支持注解ORM映射的Hibernate会话工厂 -->

​    <bean id="sessionFactory"

​        class="org.springframework.orm.hibernate3.annotation.AnnotationSessionFactoryBean">

​        <!-- 通过setter注入数据源属性 -->

​        <property name="dataSource" ref="dataSource" />

​        <!-- 配置实体类所在的包 -->

​        <property name="packagesToScan" value="com.jackfrued.entity" />

​        <!-- 配置Hibernate的相关属性 -->

​        <property name="hibernateProperties">

​            <!-- 在项目调试完成后要删除show_sql和format_sql属性否则对性能有显著影响 -->

​            <value>

​                hibernate.dialect=org.hibernate.dialect.MySQL5Dialect

​            </value>

​        </property>

​    </bean>

 

​    <!-- 配置Spring提供的Hibernate事务管理器 -->

​    <bean id="transactionManager"

​        class="org.springframework.orm.hibernate3.HibernateTransactionManager">

​        <!-- 通过setter注入Hibernate会话工厂 -->

​        <property name="sessionFactory" ref="sessionFactory" />

​    </bean>

 

​    <!-- 配置基于注解配置声明式事务 -->

​    <tx:annotation-driven />

 

</beans>

package com.jackfrued.dao;

 

import java.io.Serializable;

import java.util.List;

 

import com.jackfrued.comm.QueryBean;

import com.jackfrued.comm.QueryResult;

 

/**

- 数据访问对象接口(以对象为单位封装CRUD操作)
- @author 骆昊

 *

- @param <E> 实体类型
- @param <K> 实体标识字段的类型

 */

public interface BaseDao <E, K extends Serializable> {

 

​    /**

​     * 新增

​     * @param entity 业务实体对象

​     * @return 增加成功返回实体对象的标识

​     */

​    public K save(E entity);

 

​    /**

​     * 删除

​     * @param entity 业务实体对象

​     */

​    public void delete(E entity);

 

​    /**

​     * 根据ID删除

​     * @param id 业务实体对象的标识

​     * @return 删除成功返回true否则返回false

​     */

​    public boolean deleteById(K id);

 

​    /**

​     * 修改

​     * @param entity 业务实体对象

​     * @return 修改成功返回true否则返回false

​     */

​    public void update(E entity);

 

​    /**

​     * 根据ID查找业务实体对象

​     * @param id 业务实体对象的标识

​     * @return 业务实体对象对象或null

​     */

​    public E findById(K id);

 

​    /**

​     * 根据ID查找业务实体对象

​     * @param id 业务实体对象的标识

​     * @param lazy 是否使用延迟加载

​     * @return 业务实体对象对象

​     */

​    public E findById(K id, boolean lazy);

 

​    /**

​     * 查找所有业务实体对象

​     * @return 装所有业务实体对象的列表容器

​     */

​    public List<E> findAll();

 

​    /**

​     * 分页查找业务实体对象

​     * @param page 页码

​     * @param size 页面大小

​     * @return 查询结果对象

​     */

​    public QueryResult<E> findByPage(int page, int size);

 

​    /**

​     * 分页查找业务实体对象

​     * @param queryBean 查询条件对象

​     * @param page 页码

​     * @param size 页面大小

​     * @return 查询结果对象

​     */

​    public QueryResult<E> findByPage(QueryBean queryBean, int page, int size);

 

}

package com.jackfrued.dao;

 

import java.io.Serializable;

import java.util.List;

 

import com.jackfrued.comm.QueryBean;

import com.jackfrued.comm.QueryResult;

 

/**

- BaseDao的缺省适配器
- @author 骆昊

 *

- @param <E> 实体类型
- @param <K> 实体标识字段的类型

 */

public abstract class BaseDaoAdapter<E, K extends Serializable> implements

​        BaseDao<E, K> {

 

​    @Override

​    public K save(E entity) {

​        return null;

​    }

 

​    @Override

​    public void delete(E entity) {

​    }

 

​    @Override

​    public boolean deleteById(K id) {

​        E entity = findById(id);

​        if(entity != null) {

​            delete(entity);

​            return true;

​        }

​        return false;

​    }

 

​    @Override

​    public void update(E entity) {

​    }

 

​    @Override

​    public E findById(K id) {

​        return null;

​    }

 

​    @Override

​    public E findById(K id, boolean lazy) {

​        return null;

​    }

 

​    @Override

​    public List<E> findAll() {

​        return null;

​    }

 

​    @Override

​    public QueryResult<E> findByPage(int page, int size) {

​        return null;

​    }

 

​    @Override

​    public QueryResult<E> findByPage(QueryBean queryBean, int page, int size) {

​        return null;

​    }

 

}

package com.jackfrued.dao;

 

import java.io.Serializable;

import java.lang.reflect.ParameterizedType;

import java.util.ArrayList;

import java.util.Collections;

import java.util.List;

 

import org.hibernate.Query;

import org.hibernate.Session;

import org.hibernate.SessionFactory;

import org.springframework.beans.factory.annotation.Autowired;

 

import com.jackfrued.comm.HQLQueryBean;

import com.jackfrued.comm.QueryBean;

import com.jackfrued.comm.QueryResult;

 

/**

- 基于Hibernate的BaseDao实现类
- @author 骆昊

 *

- @param <E> 实体类型
- @param <K> 主键类型

 */

@SuppressWarnings(value = {"unchecked"})

public abstract class BaseDaoHibernateImpl<E, K extends Serializable> extends BaseDaoAdapter<E, K> {

​    @Autowired

​    protected SessionFactory sessionFactory;

 

​    private Class<?> entityClass;       // 业务实体的类对象

​    private String entityName;          // 业务实体的名字

 

​    public BaseDaoHibernateImpl() {

​        ParameterizedType pt = (ParameterizedType) this.getClass().getGenericSuperclass();

​        entityClass = (Class<?>) pt.getActualTypeArguments()[0];

​        entityName = entityClass.getSimpleName();

​    }

 

​    @Override

​    public K save(E entity) {

​        return (K) sessionFactory.getCurrentSession().save(entity);

​    }

 

​    @Override

​    public void delete(E entity) {

​        sessionFactory.getCurrentSession().delete(entity);

​    }

 

​    @Override

​    public void update(E entity) {

​        sessionFactory.getCurrentSession().update(entity);

​    }

 

​    @Override

​    public E findById(K id) {

​        return findById(id, false);

​    }

 

​    @Override

​    public E findById(K id, boolean lazy) {

​        Session session = sessionFactory.getCurrentSession();

​        return (E) (lazy? session.load(entityClass, id) : session.get(entityClass, id));

​    }

 

​    @Override

​    public List<E> findAll() {

​        return sessionFactory.getCurrentSession().createCriteria(entityClass).list();

​    }

 

​    @Override

​    public QueryResult<E> findByPage(int page, int size) {

​        return new QueryResult<E>(

​            findByHQLAndPage("from " + entityName , page, size),

​            getCountByHQL("select count(*) from " + entityName)

​        );

​    }

 

​    @Override

​    public QueryResult<E> findByPage(QueryBean queryBean, int page, int size) {

​        if(queryBean instanceof HQLQueryBean) {

​            HQLQueryBean hqlQueryBean = (HQLQueryBean) queryBean;

​            return new QueryResult<E>(

​                findByHQLAndPage(hqlQueryBean.getQueryString(), page, size, hqlQueryBean.getParameters()),

​                getCountByHQL(hqlQueryBean.getCountString(), hqlQueryBean.getParameters())

​            );

​        }

​        return null;

​    }

 

​    /**

​     * 根据HQL和可变参数列表进行查询

​     * @param hql 基于HQL的查询语句

​     * @param params 可变参数列表

​     * @return 持有查询结果的列表容器或空列表容器

​     */

​    protected List<E> findByHQL(String hql, Object... params) {

​        return this.findByHQL(hql, getParamList(params));

​    }

 

​    /**

​     * 根据HQL和参数列表进行查询

​     * @param hql 基于HQL的查询语句

​     * @param params 查询参数列表

​     * @return 持有查询结果的列表容器或空列表容器

​     */

​    protected List<E> findByHQL(String hql, List<Object> params) {

​        List<E> list = createQuery(hql, params).list();

​        return list != null && list.size() > 0 ? list : Collections.EMPTY_LIST;

​    }

 

​    /**

​     * 根据HQL和参数列表进行分页查询

​     * @param hql 基于HQL的查询语句

​     * @page 页码

​     * @size 页面大小

​     * @param params 可变参数列表

​     * @return 持有查询结果的列表容器或空列表容器

​     */

​    protected List<E> findByHQLAndPage(String hql, int page, int size, Object... params) {

​        return this.findByHQLAndPage(hql, page, size, getParamList(params));

​    }

 

​    /**

​     * 根据HQL和参数列表进行分页查询

​     * @param hql 基于HQL的查询语句

​     * @page 页码

​     * @size 页面大小

​     * @param params 查询参数列表

​     * @return 持有查询结果的列表容器或空列表容器

​     */

​    protected List<E> findByHQLAndPage(String hql, int page, int size, List<Object> params) {

​        List<E> list = createQuery(hql, params)

​                .setFirstResult((page - 1) * size)

​                .setMaxResults(size)

​                .list();

​        return list != null && list.size() > 0 ? list : Collections.EMPTY_LIST;

​    }

 

​    /**

​     * 查询满足条件的记录数

​     * @param hql 基于HQL的查询语句

​     * @param params 可变参数列表

​     * @return 满足查询条件的总记录数

​     */

​    protected long getCountByHQL(String hql, Object... params) {

​        return this.getCountByHQL(hql, getParamList(params));

​    }

 

​    /**

​     * 查询满足条件的记录数

​     * @param hql 基于HQL的查询语句

​     * @param params 参数列表容器

​     * @return 满足查询条件的总记录数

​     */

​    protected long getCountByHQL(String hql, List<Object> params) {

​        return (Long) createQuery(hql, params).uniqueResult();

​    }

 

​    // 创建Hibernate查询对象(Query)

​    private Query createQuery(String hql, List<Object> params) {

​        Query query = sessionFactory.getCurrentSession().createQuery(hql);

​        for(int i = 0; i < params.size(); i++) {

​            query.setParameter(i, params.get(i));

​        }

​        return query;

​    }

 

​    // 将可变参数列表组装成列表容器

​    private List<Object> getParamList(Object... params) {

​        List<Object> paramList = new ArrayList<>();

​        if(params != null) {

​            for(int i = 0; i < params.length; i++) {

​                paramList.add(params[i]);

​            }

​        }

​        return paramList.size() == 0? Collections.EMPTY_LIST : paramList;

​    }

 

}

package com.jackfrued.comm;

 

import java.util.List;

 

/**

- 查询条件的接口
- @author 骆昊

 *

 */

public interface QueryBean {

 

​    /**

​     * 添加排序字段

​     * @param fieldName 用于排序的字段

​     * @param asc 升序还是降序

​     * @return 查询条件对象自身(方便级联编程)

​     */

​    public QueryBean addOrder(String fieldName, boolean asc);

 

​    /**

​     * 添加排序字段

​     * @param available 是否添加此排序字段

​     * @param fieldName 用于排序的字段

​     * @param asc 升序还是降序

​     * @return 查询条件对象自身(方便级联编程)

​     */

​    public QueryBean addOrder(boolean available, String fieldName, boolean asc);

 

​    /**

​     * 添加查询条件

​     * @param condition 条件

​     * @param params 替换掉条件中参数占位符的参数

​     * @return 查询条件对象自身(方便级联编程)

​     */

​    public QueryBean addCondition(String condition, Object... params);

 

​    /**

​     * 添加查询条件

​     * @param available 是否需要添加此条件

​     * @param condition 条件

​     * @param params 替换掉条件中参数占位符的参数

​     * @return 查询条件对象自身(方便级联编程)

​     */

​    public QueryBean addCondition(boolean available, String condition, Object... params);

 

​    /**

​     * 获得查询语句

​     * @return 查询语句

​     */

​    public String getQueryString();

 

​    /**

​     * 获取查询记录数的查询语句

​     * @return 查询记录数的查询语句

​     */

​    public String getCountString();

 

​    /**

​     * 获得查询参数

​     * @return 查询参数的列表容器

​     */

​    public List<Object> getParameters();

}

package com.jackfrued.comm;

 

import java.util.List;

 

/**

- 查询结果
- @author 骆昊

 *

- @param <T> 泛型参数

 */

public class QueryResult<T> {

​    private List<T> result;     // 持有查询结果的列表容器

​    private long totalRecords;  // 查询到的总记录数

 

​    /**

​     * 构造器

​     */

​    public QueryResult() {

​    }

 

​    /**

​     * 构造器

​     * @param result 持有查询结果的列表容器

​     * @param totalRecords 查询到的总记录数

​     */

​    public QueryResult(List<T> result, long totalRecords) {

​        this.result = result;

​        this.totalRecords = totalRecords;

​    }

 

​    public List<T> getResult() {

​        return result;

​    }

 

​    public void setResult(List<T> result) {

​        this.result = result;

​    }

 

​    public long getTotalRecords() {

​        return totalRecords;

​    }

 

​    public void setTotalRecords(long totalRecords) {

​        this.totalRecords = totalRecords;

​    }

}

package com.jackfrued.dao;

 

import com.jackfrued.comm.QueryResult;

import com.jackfrued.entity.Dept;

 

/**

- 部门数据访问对象接口
- @author 骆昊

 *

 */

public interface DeptDao extends BaseDao<Dept, Integer> {

 

​    /**

​     * 分页查询顶级部门

​     * @param page 页码

​     * @param size 页码大小

​     * @return 查询结果对象

​     */

​    public QueryResult<Dept> findTopDeptByPage(int page, int size);

 

}

package com.jackfrued.dao.impl;

 

import java.util.List;

 

import org.springframework.stereotype.Repository;

 

import com.jackfrued.comm.QueryResult;

import com.jackfrued.dao.BaseDaoHibernateImpl;

import com.jackfrued.dao.DeptDao;

import com.jackfrued.entity.Dept;

 

@Repository

public class DeptDaoImpl extends BaseDaoHibernateImpl<Dept, Integer> implements DeptDao {

​    private static final String HQL_FIND_TOP_DEPT = " from Dept as d where d.superiorDept is null ";

 

​    @Override

​    public QueryResult<Dept> findTopDeptByPage(int page, int size) {

​        List<Dept> list = findByHQLAndPage(HQL_FIND_TOP_DEPT, page, size);

​        long totalRecords = getCountByHQL(" select count(*) " + HQL_FIND_TOP_DEPT);

​        return new QueryResult<>(list, totalRecords);

​    }

 

}

package com.jackfrued.comm;

 

import java.util.List;

 

/**

- 分页器
- @author 骆昊

 *

- @param <T> 分页数据对象的类型

 */

public class PageBean<T> {

​    private static final int DEFAUL_INIT_PAGE = 1;

​    private static final int DEFAULT_PAGE_SIZE = 10;

​    private static final int DEFAULT_PAGE_COUNT = 5;

 

​    private List<T> data;           // 分页数据

​    private PageRange pageRange;    // 页码范围

​    private int totalPage;          // 总页数

​    private int size;               // 页面大小

​    private int currentPage;        // 当前页码

​    private int pageCount;          // 页码数量

 

​    /**

​     * 构造器

​     * @param currentPage 当前页码

​     * @param size 页码大小

​     * @param pageCount 页码数量

​     */

​    public PageBean(int currentPage, int size, int pageCount) {

​        this.currentPage = currentPage > 0 ? currentPage : 1;

​        this.size = size > 0 ? size : DEFAULT_PAGE_SIZE;

​        this.pageCount = pageCount > 0 ? size : DEFAULT_PAGE_COUNT;

​    }

 

​    /**

​     * 构造器

​     * @param currentPage 当前页码

​     * @param size 页码大小

​     */

​    public PageBean(int currentPage, int size) {

​        this(currentPage, size, DEFAULT_PAGE_COUNT);

​    }

 

​    /**

​     * 构造器

​     * @param currentPage 当前页码

​     */

​    public PageBean(int currentPage) {

​        this(currentPage, DEFAULT_PAGE_SIZE, DEFAULT_PAGE_COUNT);

​    }

 

​    /**

​     * 构造器

​     */

​    public PageBean() {

​        this(DEFAUL_INIT_PAGE, DEFAULT_PAGE_SIZE, DEFAULT_PAGE_COUNT);

​    }

 

​    public List<T> getData() {

​        return data;

​    }

 

​    public int getStartPage() {

​        return pageRange != null ? pageRange.getStartPage() : 1;

​    }

 

​    public int getEndPage() {

​        return pageRange != null ? pageRange.getEndPage() : 1;

​    }

 

​    public long getTotalPage() {

​        return totalPage;

​    }

 

​    public int getSize() {

​        return size;

​    }

 

​    public int getCurrentPage() {

​        return currentPage;

​    }

 

​    /**

​     * 将查询结果转换为分页数据

​     * @param queryResult 查询结果对象

​     */

​    public void transferQueryResult(QueryResult<T> queryResult) {

​        long totalRecords = queryResult.getTotalRecords();

 

​        data = queryResult.getResult();

​        totalPage = (int) ((totalRecords + size - 1) / size); 

​        totalPage = totalPage >= 0 ? totalPage : Integer.MAX_VALUE;

​        this.pageRange = new PageRange(pageCount, currentPage, totalPage);

​    }

 

}

package com.jackfrued.comm;

 

/**

- 页码范围
- @author 骆昊

 *

 */

public class PageRange {

​    private int startPage;  // 起始页码

​    private int endPage;    // 终止页码

 

​    /**

​     * 构造器

​     * @param pageCount 总共显示几个页码

​     * @param currentPage 当前页码

​     * @param totalPage 总页数

​     */

​    public PageRange(int pageCount, int currentPage, int totalPage) {

​        startPage = currentPage - (pageCount - 1) / 2;

​        endPage = currentPage + pageCount / 2;

​        if(startPage < 1) {

​            startPage = 1;

​            endPage = totalPage > pageCount ? pageCount : totalPage;

​        }

​        if (endPage > totalPage) {

​            endPage = totalPage;

​            startPage = (endPage - pageCount > 0) ? endPage - pageCount + 1 : 1;

​        }

​    }

 

​    /**

​     * 获得起始页页码

​     * @return 起始页页码

​     */

​    public int getStartPage() {

​        return startPage;

​    }

 

​    /**

​     * 获得终止页页码

​     * @return 终止页页码

​     */

​    public int getEndPage() {

​        return endPage;

​    }

 

}

package com.jackfrued.biz;

 

import com.jackfrued.comm.PageBean;

import com.jackfrued.entity.Dept;

 

/**

- 部门业务逻辑接口
- @author 骆昊

 *

 */

public interface DeptService {

 

​    /**

​     * 创建新的部门

​     * @param department 部门对象

​     * @return 创建成功返回true否则返回false

​     */

​    public boolean createNewDepartment(Dept department);

 

​    /**

​     * 删除指定部门

​     * @param id 要删除的部门的编号

​     * @return 删除成功返回true否则返回false

​     */

​    public boolean deleteDepartment(Integer id);

 

​    /**

​     * 分页获取顶级部门

​     * @param page 页码

​     * @param size 页码大小

​     * @return 部门对象的分页器对象

​     */

​    public PageBean<Dept> getTopDeptByPage(int page, int size);

 

}

package com.jackfrued.biz.impl;

 

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.stereotype.Service;

import org.springframework.transaction.annotation.Transactional;

 

import com.jackfrued.biz.DeptService;

import com.jackfrued.comm.PageBean;

import com.jackfrued.comm.QueryResult;

import com.jackfrued.dao.DeptDao;

import com.jackfrued.entity.Dept;

 

@Service

@Transactional  // 声明式事务的注解

public class DeptServiceImpl implements DeptService {

​    @Autowired

​    private DeptDao deptDao;

 

​    @Override

​    public boolean createNewDepartment(Dept department) {

​        return deptDao.save(department) != null;

​    }

 

​    @Override

​    public boolean deleteDepartment(Integer id) {

​        return deptDao.deleteById(id);

​    }

 

​    @Override

​    public PageBean<Dept> getTopDeptByPage(int page, int size) {

​        QueryResult<Dept> queryResult = deptDao.findTopDeptByPage(page, size);

​        PageBean<Dept> pageBean = new PageBean<>(page, size);

​        pageBean.transferQueryResult(queryResult);

​        return pageBean;

​    }

 

}

 

### 如何在Web项目中配置Spring的IoC容器？

 答：如果需要在Web项目中使用Spring的IoC容器，可以在Web项目配置文件web.xml中做出如下配置：

<context-param>

​    <param-name>contextConfigLocation</param-name>

​    <param-value>classpath:applicationContext.xml</param-value>

</context-param>

 

<listener>

​    <listener-class>

​        org.springframework.web.context.ContextLoaderListener

​    </listener-class>

</listener>

 

### 如何在Spring IoC容器中配置数据源？ 

答： 
DBCP配置：

<bean id="dataSource"

​        class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">

​    <property name="driverClassName" value="${jdbc.driverClassName}"/>

​    <property name="url" value="${jdbc.url}"/>

​    <property name="username" value="${jdbc.username}"/>

​    <property name="password" value="${jdbc.password}"/>

</bean>

 

<context:property-placeholder location="jdbc.properties"/>

C3P0配置：

<bean id="dataSource"

​        class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">

​    <property name="driverClass" value="${jdbc.driverClassName}"/>

​    <property name="jdbcUrl" value="${jdbc.url}"/>

​    <property name="user" value="${jdbc.username}"/>

​    <property name="password" value="${jdbc.password}"/>

</bean>

 

<context:property-placeholder location="jdbc.properties"/>

提示： DBCP的详细配置在第153题中已经完整的展示过了。

### 如何配置配置事务增强？ 

答：

<?xml version="1.0" encoding="UTF-8"?>

<beans xmlns="http://www.springframework.org/schema/beans"

​     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

​     xmlns:aop="http://www.springframework.org/schema/aop"

​     xmlns:tx="http://www.springframework.org/schema/tx"

​     xsi:schemaLocation="

​     http://www.springframework.org/schema/beans

​     http://www.springframework.org/schema/beans/spring-beans.xsd

​     http://www.springframework.org/schema/tx

​     http://www.springframework.org/schema/tx/spring-tx.xsd

​     http://www.springframework.org/schema/aop

​     http://www.springframework.org/schema/aop/spring-aop.xsd">

 

  <!-- this is the service object that we want to make transactional -->

  <bean id="fooService" class="x.y.service.DefaultFooService"/>

 

  <!-- the transactional advice -->

  <tx:advice id="txAdvice" transaction-manager="txManager">

  <!-- the transactional semantics... -->

  tx:attributes

​    <!-- all methods starting with 'get' are read-only -->

​    <tx:method name="get*" read-only="true"/>

​    <!-- other methods use the default transaction settings (see below) -->

​    <tx:method name="*"/>

  /tx:attributes

  /tx:advice

 

  <!-- ensure that the above transactional advice runs for any execution

​    of an operation defined by the FooService interface -->

  aop:config

  <aop:pointcut id="fooServiceOperation" 

​    expression="execution(* x.y.service.FooService.*(..))"/>

  <aop:advisor advice-ref="txAdvice" pointcut-ref="fooServiceOperation"/>

  /aop:config

 

  <!-- don't forget the DataSource -->

  <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" 

​    destroy-method="close">

  <property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"/>

  <property name="url" value="jdbc:oracle:thin:@localhost:1521:orcl"/>

  <property name="username" value="scott"/>

  <property name="password" value="tiger"/>

  </bean>

 

  <!-- similarly, don't forget the PlatformTransactionManager -->

  <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">

  <property name="dataSource" ref="dataSource"/>

  </bean>

 

  <!-- other <bean/> definitions here -->

 

</beans>

### 选择使用Spring框架的原因（Spring框架为企业级开发带来的好处有哪些）？ 

答：可以从以下几个方面作答： 

- 非侵入式：支持基于POJO的编程模式，不强制性的要求实现Spring框架中的接口或继承Spring框架中的类。 
- IoC容器：IoC容器帮助应用程序管理对象以及对象之间的依赖关系，对象之间的依赖关系如果发生了改变只需要修改配置文件而不是修改代码，因为代码的修改可能意味着项目的重新构建和完整的回归测试。有了IoC容器，程序员再也不需要自己编写工厂、单例，这一点特别符合Spring的精神"不要重复的发明轮子"。 
- AOP（面向切面编程）：将所有的横切关注功能封装到切面（aspect）中，通过配置的方式将横切关注功能动态添加到目标代码上，进一步实现了业务逻辑和系统服务之间的分离。另一方面，有了AOP程序员可以省去很多自己写代理类的工作。 
- MVC：Spring的MVC框架是非常优秀的，从各个方面都可以甩Struts 2几条街，为Web表示层提供了更好的解决方案。 
- 事务管理：Spring以宽广的胸怀接纳多种持久层技术，并且为其提供了声明式的事务管理，在不需要任何一行代码的情况下就能够完成事务管理。 
- 其他：选择Spring框架的原因还远不止于此，Spring为Java企业级开发提供了一站式选择，你可以在需要的时候使用它的部分和全部，更重要的是，你甚至可以在感觉不到Spring存在的情况下，在你的项目中使用Spring提供的各种优秀的功能。

### Spring IoC容器配置Bean的方式？ 

答： 

- 基于XML文件进行配置。 
- 基于注解进行配置。 
- 基于Java程序进行配置（Spring 3+）

package com.jackfrued.bean;

 

import org.springframework.beans.factory.annotation.Autowired;

import org.springframework.stereotype.Component;

 

@Component

public class Person {

​    private String name;

​    private int age;

​    @Autowired

​    private Car car;

 

​    public Person(String name, int age) {

​        this.name = name;

​        this.age = age;

​    }

 

​    public void setCar(Car car) {

​        this.car = car;

​    }

 

​    @Override

​    public String toString() {

​        return "Person [name=" + name + ", age=" + age + ", car=" + car + "]";

​    }

 

}

package com.jackfrued.bean;

 

import org.springframework.stereotype.Component;

 

@Component

public class Car {

​    private String brand;

​    private int maxSpeed;

 

​    public Car(String brand, int maxSpeed) {

​        this.brand = brand;

​        this.maxSpeed = maxSpeed;

​    }

 

​    @Override

​    public String toString() {

​        return "Car [brand=" + brand + ", maxSpeed=" + maxSpeed + "]";

​    }

 

}

package com.jackfrued.config;

 

import org.springframework.context.annotation.Bean;

import org.springframework.context.annotation.Configuration;

 

import com.jackfrued.bean.Car;

import com.jackfrued.bean.Person;

 

@Configuration

public class AppConfig {

 

​    @Bean

​    public Car car() {

​        return new Car("Benz", 320);

​    }

 

​    @Bean

​    public Person person() {

​        return new Person("骆昊", 34);

​    }

}

package com.jackfrued.test;

 

import org.springframework.context.ConfigurableApplicationContext;

import org.springframework.context.annotation.AnnotationConfigApplicationContext;

 

import com.jackfrued.bean.Person;

import com.jackfrued.config.AppConfig;

 

class Test {

 

​    public static void main(String[] args) {

​        // TWR (Java 7+)

​        try(ConfigurableApplicationContext factory = new AnnotationConfigApplicationContext(AppConfig.class)) {

​            Person person = factory.getBean(Person.class);

​            System.out.println(person);

​        }

​    }

}

### 阐述Spring框架中Bean的生命周期？ 

答： 
① Spring IoC容器找到关于Bean的定义并实例化该Bean。 
② Spring IoC容器对Bean进行依赖注入。 
③ 如果Bean实现了BeanNameAware接口，则将该Bean的id传给setBeanName方法。 
④ 如果Bean实现了BeanFactoryAware接口，则将BeanFactory对象传给setBeanFactory方法。 
⑤ 如果Bean实现了BeanPostProcessor接口，则调用其postProcessBeforeInitialization方法。 
⑥ 如果Bean实现了InitializingBean接口，则调用其afterPropertySet方法。 
⑦ 如果有和Bean关联的BeanPostProcessors对象，则这些对象的postProcessAfterInitialization方法被调用。 
⑧ 当销毁Bean实例时，如果Bean实现了DisposableBean接口，则调用其destroy方法。

### 依赖注入时如何注入集合属性？ 

答：可以在定义Bean属性时，通过<list> / <set> / <map> / <props>分别为其注入列表、集合、映射和键值都是字符串的映射属性。

### Spring中的自动装配有哪些限制？

 答： 

- 如果使用了构造器注入或者setter注入，那么将覆盖自动装配的依赖关系。 
- 基本数据类型的值、字符串字面量、类字面量无法使用自动装配来注入。 
- 优先考虑使用显式的装配来进行更精确的依赖注入而不是使用自动装配。

### 在Web项目中如何获得Spring的IoC容器？ 

答：

WebApplicationContext ctx = 

WebApplicationContextUtils.getWebApplicationContext(servletContext);

 

### Spring由哪些模块组成？

以下是Spring 框架的基本模块：

 

Core module

 

Bean module

 

Context module

 

Expression Language module

 

JDBC module

 

ORM module

 

OXM module

 

Java Messaging Service(JMS) module

 

Transaction module

 

Web module

 

Web-Servlet module

 

Web-Struts module

 

Web-Portlet module

 

### 【Spring】**什么是Spring IOC 容器？**

Spring IOC 负责创建对象，管理对象（通过依赖注入（DI），装配对象，配置对象，并且管理这些对象的整个生命周期。

 

### 【Spring】**IOC的优点是什么？**

IOC 或 依赖注入把应用的代码量降到最低。它使应用容易测试，单元测试不再需要单例和JNDI查找机制。最小的代价和最小的侵入性使松散耦合得以实现。IOC容器支持加载服务时的饿汉式初始化和懒加载。

 

### 【Spring】**ApplicationContext通常的实现是什么？**

FileSystemXmlApplicationContext ：此容器从一个XML文件中加载beans的定义，XML Bean 配置文件的全路径名必须提供给它的构造函数。

 

ClassPathXmlApplicationContext：此容器也从一个XML文件中加载beans的定义，这里，你需要正确设置classpath因为这个容器将在classpath里找bean配置。

 

WebXmlApplicationContext：此容器加载一个XML文件，此文件定义了一个WEB应用的所有bean。

### 【Spring】**Bean 工厂和 Application contexts  有什么区别？**

Application contexts提供一种方法处理文本消息，一个通常的做法是加载文件资源（比如镜像），它们可以向注册为监听器的bean发布事件。另外，在容器或容器内的对象上执行的那些不得不由bean工厂以程序化方式处理的操作，可以在Application contexts中以声明的方式处理。Application contexts实现了MessageSource接口，该接口的实现以可插拔的方式提供获取本地化消息的方法。

 

### 【Spring】**什么是Spring的依赖注入？**

依赖注入，是IOC的一个方面，是个通常的概念，它有多种解释。这概念是说你不用创建对象，而只需要描述它如何被创建。你不在代码里直接组装你的组件和服务，但是要在配置文件里描述哪些组件需要哪些服务，之后一个容器（IOC容器）负责把他们组装起来。

### 【Spring】**有哪些不同类型的IOC（依赖注入）方式？**

构造器依赖注入：构造器依赖注入通过容器触发一个类的构造器来实现的，该类有一系列参数，每个参数代表一个对其他类的依赖。

 

Setter方法注入：Setter方法注入是容器通过调用无参构造器或无参static工厂 方法实例化bean之后，调用该bean的setter方法，即实现了基于setter的依赖注入。

 

### 【Spring】**哪种依赖注入方式你建议使用，构造器注入，还是 Setter方法注入？**

你两种依赖方式都可以使用，构造器注入和Setter方法注入。最好的解决方案是用构造器参数实现强制依赖，setter方法实现可选依赖。

 

### 【Spring】**什么是Spring beans？**

 

Spring beans 是那些形成Spring应用的主干的java对象。它们被Spring IOC容器初始化，装配，和管理。这些beans通过容器中配置的元数据创建。比如，以XML文件中<bean/> 的形式定义。

 

Spring 框架定义的beans都是单件beans。在bean tag中有个属性”singleton”，如果它被赋为TRUE，bean 就是单件，否则就是一个 prototype bean。默认是TRUE，所以所有在Spring框架中的beans 缺省都是单件。

### 【Spring】**一个 Spring Bean 定义 包含什么？**

一个Spring Bean 的定义包含容器必知的所有配置元数据，包括如何创建一个bean，它的生命周期详情及它的依赖。

 

 

### 【Spring】**如何给Spring 容器提供配置元数据？**

 

这里有三种重要的方法给Spring 容器提供配置元数据。

 

XML配置文件。

 

基于注解的配置。

 

基于java的配置。

 

### 【Spring】**解释Spring支持的几种bean的作用域**

 

Spring框架支持以下五种bean的作用域：

 

singleton : bean在每个Spring ioc 容器中只有一个实例。

 

prototype：一个bean的定义可以有多个实例。

 

request：每次http请求都会创建一个bean，该作用域仅在基于web的Spring ApplicationContext情形下有效。

 

session：在一个HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。

 

global-session：在一个全局的HTTP Session中，一个bean定义对应一个实例。该作用域仅在基于web的Spring ApplicationContext情形下有效。

 

缺省的Spring bean 的作用域是Singleton。

 

### 【Spring】**Spring框架中的单例bean是线程安全的吗？**

不，Spring框架中的单例bean不是线程安全的。

### 【Spring】**解释Spring框架中bean的生命周期**

Spring容器 从XML 文件中读取bean的定义，并实例化bean。

 

Spring根据bean的定义填充所有的属性。

 

如果bean实现了BeanNameAware 接口，Spring 传递bean 的ID 到 setBeanName方法。

 

如果Bean 实现了 BeanFactoryAware 接口， Spring传递beanfactory 给setBeanFactory 方法。

 

如果有任何与bean相关联的BeanPostProcessors，Spring会在postProcesserBeforeInitialization()方法内调用它们。

 

如果bean实现IntializingBean了，调用它的afterPropertySet方法，如果bean声明了初始化方法，调用此初始化方法。

 

如果有BeanPostProcessors 和bean 关联，这些bean的postProcessAfterInitialization() 方法将被调用。

 

如果bean实现了 DisposableBean，它将调用destroy()方法。

 

### 【Spring】**哪些是重要的bean生命周期方法？ 你能重载它们吗？**

有两个重要的bean 生命周期方法，第一个是setup ， 它是在容器加载bean的时候被调用。第二个方法是 teardown  它是在容器卸载类的时候被调用。

 

The bean 标签有两个重要的属性（init-method和destroy-method）。用它们你可以自己定制初始化和注销方法。它们也有相应的注解（@PostConstruct和@PreDestroy）。

### 【Spring】**在 Spring中如何注入一个java集合？**

 

Spring提供以下几种集合的配置元素：

 

<list>类型用于注入一列值，允许有相同的值。

 

<set> 类型用于注入一组值，不允许有相同的值。

 

<map> 类型用于注入一组键值对，键和值都可以为任意类型。



<props>类型用于注入一组键值对，键和值都只能为String类型。

 

### 【Spring】**什么是bean装配？**

装配，或bean 装配是指在Spring 容器中把bean组装到一起，前提是容器需要知道bean的依赖关系，如何通过依赖注入来把它们装配到一起。

### 【Spring】**什么是bean的自动装配？**

Spring 容器能够自动装配相互合作的bean，这意味着容器不需要<constructor-arg>和<property>配置，能通过Bean工厂自动处理bean之间的协作。

### 【Spring】**解释不同方式的自动装配**

有五种自动装配的方式，可以用来指导Spring容器用自动装配方式来进行依赖注入

 

no：默认的方式是不进行自动装配，通过显式设置ref 属性来进行装配。

 

byName：通过参数名 自动装配，Spring容器在配置文件中发现bean的autowire属性被设置成byname，之后容器试图匹配、装配和该bean的属性具有相同名字的bean。

 

byType：通过参数类型自动装配，Spring容器在配置文件中发现bean的autowire属性被设置成byType，之后容器试图匹配、装配和该bean的属性具有相同类型的bean。如果有多个bean符合条件，则抛出错误。

 

constructor：这个方式类似于byType， 但是要提供给构造器参数，如果没有确定的带参数的构造器参数类型，将会抛出异常。

 

autodetect：首先尝试使用constructor来自动装配，如果无法工作，则使用byType方式。

### 【Spring】**自动装配有哪些局限性？**

自动装配的局限性是：

 

重写：你仍需用 <constructor-arg>和 <property> 配置来定义依赖，意味着总要重写自动装配。

 

基本数据类型：你不能自动装配简单的属性，如基本数据类型，String字符串，和类。

 

模糊特性：自动装配不如显式装配精确，如果有可能，建议使用显式装配。

### 【Spring】**你可以在Spring中注入一个null 和一个空字符串吗？**

可以

### 【Spring】**什么是基于Java的Spring注解配置? 给一些注解的例子**

基于Java的配置，允许你在少量的Java注解的帮助下，进行你的大部分Spring配置而非通过XML文件。

 

以@Configuration 注解为例，它用来标记类可以当做一个bean的定义，被Spring IOC容器使用。另一个例子是@Bean注解，它表示此方法将要返回一个对象，作为一个bean注册进Spring应用上下文。点击这里学习JAVA几大元注解。

 

### 【Spring】**什么是基于注解的容器配置？**

 

相对于XML文件，注解型的配置依赖于通过字节码元数据装配组件，而非尖括号的声明。

 

开发者通过在相应的类，方法或属性上使用注解的方式，直接组件类中进行配置，而不是使用xml表述bean的装配关系。

### 【Spring】**怎样开启注解装配？**

注解装配在默认情况下是不开启的，为了使用注解装配，我们必须在Spring配置文件中配置 context:annotation-config/元素。

 

 

 

### 【Spring】**@Required  注解**

这个注解表明bean的属性必须在配置的时候设置，通过一个bean定义的显式的属性值或通过自动装配，若@Required注解的bean属性未被设置，容器将抛出BeanInitializationException。

 

### 【Spring】**@Autowired 注解**

 

 

 

@Autowired 注解提供了更细粒度的控制，包括在何处以及如何完成自动装配。它的用法和@Required一样，修饰setter方法、构造器、属性或者具有任意名称和/或多个参数的PN方法。

 

 

 

### 【Spring】**@Qualifier 注解**

当有多个相同类型的bean却只有一个需要自动装配时，将@Qualifier 注解和@Autowire 注解结合使用以消除这种混淆，指定需要装配的确切的bean。

### 【Spring】**在Spring框架中如何更有效地使用JDBC？**

使用SpringJDBC 框架，资源管理和错误处理的代价都会被减轻。所以开发者只需写statements 和 queries从数据存取数据，JDBC也可以在Spring框架提供的模板类的帮助下更有效地被使用，这个模板叫JdbcTemplate （例子见这里here）

### 【Spring】 JdbcTemplate

JdbcTemplate 类提供了很多便利的方法解决诸如把数据库数据转变成基本数据类型或对象，执行写好的或可调用的数据库操作语句，提供自定义的数据错误处理。

 

 

 

### 【Spring】**Spring对DAO的支持**

 

 

 

Spring对数据访问对象（DAO）的支持旨在简化它和数据访问技术如JDBC，Hibernate or JDO 结合使用。这使我们可以方便切换持久层。编码时也不用担心会捕获每种技术特有的异常。

 

 

 

### 【Spring】**使用Spring通过什么方式访问Hibernate？**

 

 

 

在Spring中有两种方式访问Hibernate：

 

控制反转  Hibernate Template和 Callback

 

继承 HibernateDAOSupport提供一个AOP 拦截器

 

 

 

### 【Spring】**Spring支持的ORM**

 

 

 

Spring支持以下ORM：

 

Hibernate

 

iBatis

 

JPA (Java Persistence API)

 

TopLink

 

JDO (Java Data Objects)

 

OJB

 

 

 

### 【Spring】**如何通过HibernateDaoSupport将Spring和Hibernate结合起来？**

 

 

 

用Spring的 SessionFactory 调用 LocalSessionFactory。集成过程分三步：

 

配置the Hibernate SessionFactory

 

继承HibernateDaoSupport实现一个DAO

 

在AOP支持的事务中装配

 

 

 

### 【Spring】**Spring支持的事务管理类型**

 

 

 

Spring支持两种类型的事务管理：

 

编程式事务管理：这意味你通过编程的方式管理事务，给你带来极大的灵活性，但是难维护。

 

声明式事务管理：这意味着你可以将业务代码和事务管理分离，你只需用注解和XML配置来管理事务。

 

 

 

### 【Spring】**Spring框架的事务管理有哪些优点？**

 

 

 

它为不同的事务API  如 JTA，JDBC，Hibernate，JPA 和JDO，提供一个不变的编程模式。

 

它为编程式事务管理提供了一套简单的API而不是一些复杂的事务API如

 

它支持声明式事务管理。

 

它和Spring各种数据访问抽象层很好得集成。

 

 

### 【Spring】**你更倾向用那种事务管理类型？**

 

 

 

大多数Spring框架的用户选择声明式事务管理，因为它对应用代码的影响最小，因此更符合一个无侵入的轻量级容器的思想。声明式事务管理要优于编程式事务管理，虽然比编程式事务管理（这种方式允许你通过代码控制事务）少了一点灵活性。

### 【Spring】 解释AOP

 

 

 

面向切面的编程，或AOP， 是一种编程技术，允许程序模块化横向切割关注点，或横切典型的责任划分，如日志和事务管理。

 

 

 

### 【Spring】**Aspect 切面**

 

 

 

AOP核心就是切面，它将多个类的通用行为封装成可重用的模块，该模块含有一组API提供横切功能。比如，一个日志模块可以被称作日志的AOP切面。根据需求的不同，一个应用程序可以有若干切面。在Spring AOP中，切面通过带有@Aspect注解的类实现。

 

 

 

### 【Spring】**在Spring AOP 中，关注点和横切关注的区别是什么？**

 

 

 

关注点是应用中一个模块的行为，一个关注点可能会被定义成一个我们想实现的一个功能。

 

 

 

横切关注点是一个关注点，此关注点是整个应用都会使用的功能，并影响整个应用，比如日志，安全和数据传输，几乎应用的每个模块都需要的功能。因此这些都属于横切关注点。

 

 

### 【Spring】**连接点**

 

 

 

连接点代表一个应用程序的某个位置，在这个位置我们可以插入一个AOP切面，它实际上是个应用程序执行Spring AOP的位置。

 

 

### 【Spring】**通知**

 

 

 

通知是个在方法执行前或执行后要做的动作，实际上是程序执行时要通过SpringAOP框架触发的代码段。

 

 

 

Spring切面可以应用五种类型的通知：

 

before：前置通知，在一个方法执行前被调用

 

after：在方法执行之后调用的通知，无论方法执行是否成功

 

after-returning：仅当方法成功完成后执行的通知

 

after-throwing：在方法抛出异常退出时执行的通知

 

around：在方法执行之前和之后调用的通知

 

 

### 【Spring】**切点**

 

 

 

切入点是一个或一组连接点，通知将在这些位置执行。可以通过表达式或匹配的方式指明切入点。

 

 

 

### 【Spring】**什么是引入？**

 

 

 

引入允许我们在已存在的类中增加新的方法和属性。

 

 

### 【Spring】**什么是目标对象？**

 

 

 

被一个或者多个切面所通知的对象。它通常是一个代理对象。也指被通知（advised）对象。

 

 

### 【Spring】**什么是代理？**

 

 

 

代理是通知目标对象后创建的对象。从客户端的角度看，代理对象和目标对象是一样的。

 

 

### 【Spring】**有几种不同类型的自动代理？**

 

 

 

BeanNameAutoProxyCreator

 

DefaultAdvisorAutoProxyCreator

 

Metadata autoproxying

 

 

### 【Spring】**什么是织入。什么是织入应用的不同点？**

 

 

 

织入是将切面和到其他应用类型或对象连接或创建一个被通知对象的过程。

 

织入可以在编译时，加载时，或运行时完成。

 

 

### 【Spring】**解释基于XML Schema方式的切面实现**

 

 

 

在这种情况下，切面由常规类以及基于XML的配置实现。

 

 

 

### 【Spring】**解释基于注解的切面实现**

 

 

 

在这种情况下(基于@AspectJ的实现)，涉及到的切面声明的风格与带有java5标注的普通java类一致。

 

 

 

### 【Spring】**什么是Spring的MVC框架？**

 

 

 

Spring 配备构建Web 应用的全功能MVC框架。Spring可以很便捷地和其他MVC框架集成，如Struts，Spring 的MVC框架用控制反转把业务对象和控制逻辑清晰地隔离。它也允许以声明的方式把请求参数和业务对象绑定。

 

 

### 【Spring】**DispatcherServlet**

 

 

 

Spring的MVC框架是围绕DispatcherServlet来设计的，它用来处理所有的HTTP请求和响应。

 

 

### 【Spring】**WebApplicationContext**

 

 

 

WebApplicationContext 继承了ApplicationContext  并增加了一些WEB应用必备的特有功能，它不同于一般的ApplicationContext ，因为它能处理主题，并找到被关联的servlet。

 

 

### 【Spring】**什么是Spring MVC框架的控制器？**

 

 

 

控制器提供一个访问应用程序的行为，此行为通常通过服务接口实现。控制器解析用户输入并将其转换为一个由视图呈现给用户的模型。Spring用一个非常抽象的方式实现了一个控制层，允许用户创建多种用途的控制器。

 

 

### 【Spring】**@Controller 注解**

 

 

 

该注解表明该类扮演控制器的角色，Spring不需要你继承任何其他控制器基类或引用Servlet API。

 

 

### 【Spring】**@RequestMapping 注解**

 

 

 

该注解是用来映射一个URL到一个类或一个特定的方处理法上。