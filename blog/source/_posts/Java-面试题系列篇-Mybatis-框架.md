---
title: Java 面试题系列篇-Mybatis 框架
date: 2018-10-20 18:14:27
tags: Java
---

## Mybatis 框架

### 【MyBatis】MyBatis中使用#和$书写占位符有什么区别？ 

答：#将传入的数据都当成一个字符串，会对传入的数据自动加上引号；将传入的数据直接显示生成在SQL中。注意：使用​占位符可能会导致SQL注射攻击，能用#的地方就不要使用，写order by子句的时候应该用​而不是#。

{}是预编译处理，${}是字符串替换。

Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；

Mybatis在处理{}时，就是把​{}替换成变量的值。

使用#{}可以有效的防止SQL注入，提高系统安全性。

 

### 【MyBatis】解释一下MyBatis中命名空间（namespace）的作用。 

答：在大型项目中，可能存在大量的SQL语句，这时候为每个SQL语句起一个唯一的标识（ID）就变得并不容易了。为了解决这个问题，在MyBatis中，可以为每个映射文件起一个唯一的命名空间，这样定义在这个映射文件中的每个SQL语句就成了定义在这个命名空间中的一个ID。只要我们能够保证每个命名空间中这个ID是唯一的，即使在不同映射文件中的语句ID相同，也不会再产生冲突了。

### 【MyBatis】动态SQL是什么意思？ 

答：对于一些复杂的查询，我们可能会指定多个查询条件，但是这些条件可能存在也可能不存在，例如在58同城上面找房子，我们可能会指定面积、楼层和所在位置来查找房源，也可能会指定面积、价格、户型和所在位置来查找房源，此时就需要根据用户指定的条件动态生成SQL语句。如果不使用持久层框架我们可能需要自己拼装SQL语句，还好MyBatis提供了动态SQL的功能来解决这个问题。MyBatis中用于实现动态SQL的元素主要有： 

- if 
- choose / when / otherwise 
- trim 
- where 
- set 
- foreach

下面是映射文件的片段。

​    <select id="foo" parameterType="Blog" resultType="Blog">

​        select * from t_blog where 1 = 1

​        <if test="title != null">

​            and title = #{title}

​        </if>

​        <if test="content != null">

​            and content = #{content}

​        </if>

​        <if test="owner != null">

​            and owner = #{owner}

​        </if>

   </select>

当然也可以像下面这些书写。

​    <select id="foo" parameterType="Blog" resultType="Blog">

​        select * from t_blog where 1 = 1 

​        <choose>

​            <when test="title != null">

​                and title = #{title}

​            </when>

​            <when test="content != null">

​                and content = #{content}

​            </when>

​            <otherwise>

​                and owner = "owner1"

​            </otherwise>

​        </choose>

​    </select>

再看看下面这个例子。

​    <select id="bar" resultType="Blog">

​        select * from t_blog where id in

​        <foreach collection="array" index="index" 

​            item="item" open="(" separator="," close=")">

​            #{item}

​        </foreach>

</select>

### Mybatis当实体类中的属性名和表中的字段名不一样 ，怎么办 ？

第1种： 通过在查询的sql语句中定义字段名的别名，让字段名的别名和实体类的属性名一致 

​    <select id="selectorder" parametertype="int" resultetype="me.gacl.domain.order"> 

​       select order_id id, order_no orderno ,order_price price form orders where order_id=#{id}; 

</select> 

 

第2种： 通过<resultMap>来映射字段名和实体类属性名的一一对应的关系 

​    <select id="getOrder" parameterType="int" resultMap="orderresultmap">

​        select * from orders where order_id=#{id}

​    </select>

   <resultMap type="me.gacl.domain.order" id="orderresultmap"> 

​        <!–用id属性来映射主键字段–> 

​        <id property="id" column="order_id"> 

​        <!–用result属性来映射非主键字段，property为实体类属性名，column为数据表中的属性–> 

​        <result property = “orderno" column =”order_no"/> 

​        <result property="price" column="order_price" /> 

​    </reslutMap>

 

### Mybatis 模糊查询like语句该怎么写?

第1种：在Java代码中添加sql通配符。

​    string wildcardname = “%smi%”; 

​    list<name> names = mapper.selectlike(wildcardname);

 

​    <select id="selectlike"> 

​     select * from foo where bar like #{value} 

​    </select>

 

第2种：在sql语句中拼接通配符，会引起sql注入

​    string wildcardname = “smi”; 

​    list<name> names = mapper.selectlike(wildcardname);

 

​    <select id="selectlike"> 

​     select * from foo where bar like "%"#{value}"%"

</select>

 

### Mybatis 通常一个Xml映射文件，都会写一个Dao接口与之对应，请问，这个Dao接口的工作原理是什么？Dao接口里的方法，参数不同时，方法能重载吗？

Dao接口，就是人们常说的Mapper接口，接口的全限名，就是映射文件中的namespace的值，接口的方法名，就是映射文件中MappedStatement的id值，接口方法内的参数，就是传递给sql的参数。Mapper接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为key值，可唯一定位一个MappedStatement，举例：com.mybatis3.mappers.StudentDao.findStudentById，可以唯一找到namespace为com.mybatis3.mappers.StudentDao下面id = findStudentById的MappedStatement。在Mybatis中，每一个<select>、<insert>、<update>、<delete>标签，都会被解析为一个MappedStatement对象。

 

Dao接口里的方法，是不能重载的，因为是全限名+方法名的保存和寻找策略。

 

Dao接口的工作原理是JDK动态代理，Mybatis运行时会使用JDK动态代理为Dao接口生成代理proxy对象，代理对象proxy会拦截接口方法，转而执行MappedStatement所代表的sql，然后将sql执行结果返回。

 

### Mybatis是如何进行分页的？分页插件的原理是什么？

Mybatis使用RowBounds对象进行分页，它是针对ResultSet结果集执行的内存分页，而非物理分页，可以在sql内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。

 

分页插件的基本原理是使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，根据dialect方言，添加对应的物理分页语句和物理分页参数。

 

### Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？

答：第一种是使用<resultMap>标签，逐一定义列名和对象属性名之间的映射关系。第二种是使用sql列的别名功能，将列别名书写为对象属性名，比如T_NAME AS NAME，对象属性名一般是name，小写，但是列名不区分大小写，Mybatis会忽略列名大小写，智能找到与之对应对象属性名，你甚至可以写成T_NAME AS NaMe，Mybatis一样可以正常工作。

 

有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。

 

### Mybatis 如何执行批量插入?

首先,创建一个简单的insert语句: 

​    <insert id="insertname"> 

​     insert into names (name) values (#{value}) 

​    </insert>

然后在java代码中像下面这样执行批处理插入: 

​    list<string> names = new arraylist(); 

​    names.add(“fred”); 

​    names.add(“barney”); 

​    names.add(“betty”); 

​    names.add(“wilma”); 

 

​    // 注意这里 executortype.batch 

​    sqlsession sqlsession = sqlsessionfactory.opensession(executortype.batch); 

​    try { 

​     namemapper mapper = sqlsession.getmapper(namemapper.class); 

​     for (string name : names) { 

​     mapper.insertname(name); 

​     } 

​     sqlsession.commit(); 

​    } finally { 

​     sqlsession.close(); 

}

 

### Mybatis 如何获取自动生成的(主)键值?

insert 方法总是返回一个int值 - 这个值代表的是插入的行数。 

而自动生成的键值在 insert 方法执行完后可以被设置到传入的参数对象中。 

示例: 

​    <insert id="insertname" usegeneratedkeys="true" keyproperty="id"> 

​     insert into names (name) values (#{name}) 

​    </insert>

 

​    name name = new name(); 

​    name.setname(“fred”); 

 

​    int rows = mapper.insertname(name); 

​    // 完成后,id已经被设置到对象中 

​    system.out.println(“rows inserted = ” + rows); 

system.out.println(“generated key value = ” + name.getid());

 

### Mybatis在mapper中如何传递多个参数?

第1种：

//DAO层的函数

 

Public UserselectUser(String name,String area);  

//对应的xml,#{0}代表接收的是dao层中的第一个参数，#{1}代表dao层中第二参数，更多参数一致往后加即可。

 

<select id="selectUser"resultMap="BaseResultMap">  

​    select *  fromuser_user_t   whereuser_name = #{0} anduser_area=#{1}  

</select>  

第2种：    使用 @param 注解: 

​    import org.apache.ibatis.annotations.param; 

​        public interface usermapper { 

​         user selectuser(@param(“username”) string username, 

​         @param(“hashedpassword”) string hashedpassword); 

​        }

然后,就可以在xml像下面这样使用(推荐封装为一个map,作为单个参数传递给mapper): 

​    <select id="selectuser" resulttype="user"> 

​         select id, username, hashedpassword 

​         from some_table 

​         where username = #{username} 

​         and hashedpassword = #{hashedpassword} 

</select>

 

### Mybatis动态sql是做什么的？都有哪些动态sql？能简述一下动态sql的执行原理不？

Mybatis动态sql可以让我们在Xml映射文件内，以标签的形式编写动态sql，完成逻辑判断和动态拼接sql的功能。

Mybatis提供了9种动态sql标签：trim|where|set|foreach|if|choose|when|otherwise|bind。

其执行原理为，使用OGNL从sql参数对象中计算表达式的值，根据表达式的值动态拼接sql，以此来完成动态sql的功能。

 

### Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？

不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置namespace，那么id不能重复；毕竟namespace不是必须的，只是最佳实践而已。

 

原因就是namespace+id是作为Map<String, MappedStatement>的key使用的，如果没有namespace，就剩下id，那么，id重复会导致数据互相覆盖。有了namespace，自然id就可以重复，namespace不同，namespace+id自然也就不同。

 

### Mybatis 为什么说是半自动ORM映射工具？它与全自动的区别在哪里？

Hibernate属于全自动ORM映射工具，使用Hibernate查询关联对象或者关联集合对象时，可以根据对象关系模型直接获取，所以它是全自动的。而Mybatis在查询关联对象或关联集合对象时，需要手动编写sql来完成，所以，称之为半自动ORM映射工具。

 

### Mybatis 一对一、一对多的关联查询 ？

<mapper namespace="com.lcb.mapping.userMapper">  

​    <!--association  一对一关联查询 -->  

​    <select id="getClass" parameterType="int" resultMap="ClassesResultMap">  

​        select * from class c,teacher t where c.teacher_id=t.t_id and c.c_id=#{id}  

​    </select>  

​    <resultMap type="com.lcb.user.Classes" id="ClassesResultMap">  

​        <!-- 实体类的字段名和数据表的字段名映射 -->  

​        <id property="id" column="c_id"/>  

​        <result property="name" column="c_name"/>  

​        <association property="teacher" javaType="com.lcb.user.Teacher">  

​            <id property="id" column="t_id"/>  

​            <result property="name" column="t_name"/>  

​        </association>  

​    </resultMap>  

 

​    <!--collection  一对多关联查询 -->  

​    <select id="getClass2" parameterType="int" resultMap="ClassesResultMap2">  

​        select * from class c,teacher t,student s where c.teacher_id=t.t_id and c.c_id=s.class_id and c.c_id=#{id}  

​    </select>  

​    <resultMap type="com.lcb.user.Classes" id="ClassesResultMap2">  

​        <id property="id" column="c_id"/>  

​        <result property="name" column="c_name"/>  

​        <association property="teacher" javaType="com.lcb.user.Teacher">  

​            <id property="id" column="t_id"/>  

​            <result property="name" column="t_name"/>  

​        </association>  

​        <collection property="student" ofType="com.lcb.user.Student">  

​            <id property="id" column="s_id"/>  

​            <result property="name" column="s_name"/>  

​        </collection>  

​    </resultMap>  

 

</mapper>  