# JAVASE

## 关键字instanceof的使用

instanceof只能使用在object对象上面，比如如下代码：

~~~java
@Test
public void getClassType() {
    //注意i不能为其他类型,只能为Object类型
    Object i = "sdfsd";
    if(i instanceof String) {
        System.out.println("为String类型");
    }
}
~~~

## java字符串操作



## 集合

### 1.Map

寻找特定值：

```java
//寻找value值所在
boolean b = map.containsValue("aaa");
//寻找key值是否所在
boolean b = map.containsKey(1);
```

## 反射

### 1. 调方法：

使用反射调用指定方法-->

~~~java
package com.yt.test;

import java.lang.reflect.Method;

public abstract class AoTeMan {
    public AoTeMan(){
        try {
            //在类原型上面就有getMethod api供使用时调方法
            Method show = this.getClass().getMethod("show");
            show.invoke(this);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
~~~

子类中创建一个方法:这样实现了通过反射调用一个方法

```java
package com.yt.test;

public class 动态代理济成 extends AoTeMan{
    public void show(){
        System.out.println("你是猪");
    }

    public static void main(String[] args) {
        AoTeMan aoTeMan = new 动态代理济成();
    }
}
```

### 2. 调用属性:

通过反射调用一个属性--->`set方法和get方法使用步骤一毛一样`	

~~~java
//name属性获取值get()方法,需要注入一个对象,否则无法调用gei方法
Field name = BuTonLei.class.getField("name");

//通过反射获取一个对象首先需要实例化他的构造器,然后调用 newInstance 对构造器的值进行注入操作
Constructor<BuTonLei> constructor = BuTonLei.class.getConstructor(String.class);
BuTonLei lei = constructor.newInstance("你不是猪");
System.out.println(name.get(lei));
~~~

### 3. 调用对象:

~~~java
//通过反射获取一个对象首先需要实例化他的构造器,然后调用 newInstance 对构造器的值进行注入操作
Constructor<BuTonLei> constructor = BuTonLei.class.getConstructor(String.class);
BuTonLei lei = constructor.newInstance("你不是猪");
~~~

**实例：**使用只有一个值的构造函数调用对象

~~~java
//	获取构造函数为一个值的对象
Constructor<Chapter> constructor = Chapter.class.getConstructor(int.class);
Chapter chapter1 = constructor.newInstance(1);
System.out.println(chapter1);
~~~

使用多个构造函数的值调用对象：

~~~java
Constructor<Chapter> constructor2 = Chapter.class.getConstructor(Integer.class,String.class,String.class,Integer.class,String.class);
Chapter chapter2 = constructor2.newInstance(2,"奥特曼之歌","帝皇奥特曼",20,"2020年1月2号");
System.out.println(chapter2);
~~~

![image-20220105083118481](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20220105083118481.png)



### 4. 调用私有属性和方法:

~~~java
 BuTonLei.class.getDeclaredField()
 BuTonLei.class.getDeclaredMethod()
~~~

### 5. 获取类的实例对象:

~~~java
Class<?> aClass = Class.forName();
~~~

### ￥ 案例

#### 1. 通过javaBean获取数据库数据案例：

核心java代码

~~~java
//获取数据,使用反射获取对应的数据
@SuppressWarnings("unchecked")
public <T> List<T> getData(Class<T> clazz) throws Exception {
    String sql = "SELECT * FROM "+clazz.getSimpleName();
    List<T> list = new ArrayList<T>();

    Connection connection = BaseConnection.getConnection();
    PreparedStatement statement = connection.prepareStatement(sql);
    ResultSet query = statement.executeQuery();

    //获取数据库里面的数据行数
    int count = query.getMetaData().getColumnCount();

    //将指针下移
    while(query.next()) {
        Class<?>[] countTypeArr =new Class[count];
        Object[] countDataArr= new Object[count];
        for(int i = 1;i<=count;i++) {
            //获取数据库里面的数据
            Object countData = query.getObject(i);
            //这个是获取数据库里面的数据数据类型
            Class<? extends Object> class1 = countData.getClass();
            countTypeArr[i-1] = countData.getClass();
            //将获取的数据库数据放入该数组里面
            countDataArr[i-1] = countData;
        }
        //利用反射对该类进行实例化
        Constructor<T> constructor =clazz.getConstructor(countTypeArr);
        T tNewInstance = constructor.newInstance(countDataArr);
        list.add(tNewInstance);
    }
    BaseConnection.setColseConnection();
    return list;
}
~~~

jdbc:

~~~java
package com.yangteng.dao;

import java.io.Console;
import java.sql.Connection;
import java.sql.DriverManager;

public class BaseConnection {
    private static Connection connection;
    //获取数据库连接
    public static Connection getConnection() throws Exception {
        if(connection==null) {			
            connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/cyh_database?serverTimezone=UTC","root","root");
        }
        return connection;
    }

    //关闭数据库连接
    public static void setColseConnection() throws Exception {
        if(connection!=null) {
            //connection.commit();
            connection.close();
        }
    }

}

~~~



实体类：构造函数就够了，没那么需要get、set函数

~~~java
package com.yangteng.entity;

public class Chapter {
	private int id;
	private String name;
	private String context;
	private Integer  words;
	private String date;
public Chapter(Integer id, String name, String context, Integer words, String date) {
        super();
        this.id = id;
        this.name = name;
        this.context = context;
        this.words = words;
        this.date = date;
    }
}
~~~

表：

![image-20220105083632939](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20220105083632939.png)

测试：

~~~java
@Test
public void getData() throws Exception {
    //	获取构造函数为一个值的对象
    Constructor<Chapter> constructor = Chapter.class.getConstructor(Integer.class);
    Chapter chapter1 = constructor.newInstance(1);
    System.out.println(chapter1);

    Constructor<Chapter> constructor2 = Chapter.class.getConstructor(Integer.class,String.class,String.class,Integer.class,String.class);
    Chapter chapter2 = constructor2.newInstance(2,"奥特曼之歌","帝皇奥特曼",20,"2020年1月2号");
    System.out.println(chapter2);

    //获取数据库里面的数据
    BaseMapper baseMapper = new BaseMapper();
    List<Chapter> data = baseMapper.getData(Chapter.class);
    for(Chapter chapter : data) {
        System.out.println(chapter);
    }
}
~~~



## jdbc的使用

### 1. 数据库连接:

~~~java
package com.yangteng.dao;

import java.io.Console;
import java.sql.Connection;
import java.sql.DriverManager;

public class BaseConnection {
	private static Connection connection;
	//获取数据库连接
	public static Connection getConnection() throws Exception {
		if(connection==null) {			
			connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/cyh_database?serverTimezone=UTC","root","root");
		}
		return connection;
	}
	
	//关闭数据库连接
	public static void setColseConnection() throws Exception {
		if(connection!=null) {
//			connection.commit();
			connection.close();
		}
	}
	
}

~~~

### 2. 使用数据库增删改

~~~java
//数据库的增删改
public boolean setSql(String sql,Object... args) throws Exception {
    Connection connection = BaseConnection.getConnection();
    PreparedStatement prepareStatement = connection.prepareStatement(sql);
    for (int i = 1; i <= args.length; i++) {
        prepareStatement.setObject(i, args[i-1]);
    }
    boolean execute = prepareStatement.execute();
    BaseConnection.setColseConnection();
    return execute;
}
~~~

测试:

~~~java
@Test
public void setSql() throws Exception {
    BaseMapper baseMapper = new BaseMapper();
    boolean setSql = baseMapper.setSql("INSERT INTO chapter(`name`,content,words,date) VALUES(?,?,?,?)","第八百十八章","上天带来了奥特曼谢谢",20,"2020年12月22日");
    if(!setSql) {
        System.out.println("插入数据成功!");
    }else {
        System.out.println("插入数据失败!");
    }
}
~~~

### 3. 使用数据库查询

~~~java
//获取数据,使用反射获取对应的数据
@SuppressWarnings("unchecked")
public <T> List<T> getData(Class<T> clazz,String sqlQuery,Object... args) throws Exception {
    String sql;
    List<T> list = new ArrayList<T>();
    if(sqlQuery.trim() != null&&!sqlQuery.trim().equals("")) {
        sql = sqlQuery;
    }else {
        sql = "SELECT * FROM "+clazz.getSimpleName();
    }
    Connection connection = BaseConnection.getConnection();
    PreparedStatement statement = connection.prepareStatement(sql);
    if(args.length>0) {
        for (int i = 0; i < args.length; i++) {
            statement.setObject(i+1, args[i]);
        }
    }
    ResultSet query = statement.executeQuery();

    //获取数据库里面的数据行数
    int count = query.getMetaData().getColumnCount();

    //将指针下移
    while(query.next()) {
        Class<?>[] countTypeArr =new Class[count];
        Object[] countDataArr= new Object[count];
        for(int i = 1;i<=count;i++) {
            //获取数据库里面的数据
            Object countData = query.getObject(i);
            //这个是获取数据库里面的数据数据类型
            Class<? extends Object> class1 = countData.getClass();
            countTypeArr[i-1] = countData.getClass();
            //将获取的数据库数据放入该数组里面
            countDataArr[i-1] = countData;
        }
        //利用反射对该类进行实例化
        Constructor<T> constructor =clazz.getConstructor(countTypeArr);
        T tNewInstance = constructor.newInstance(countDataArr);
        list.add(tNewInstance);
    }
    BaseConnection.setColseConnection();
    return list;
}
~~~

## 注解

## java操作cmd命令行

代码：注意这个是直接调用系统文件的——就是环境变量那些文件，所以不打开cmd.exe运行个鬼文件

~~~java
Runtime rt = Runtime.getRuntime();
p = rt.exec("cmd.exe /c start C:/Users/有天道/Desktop/auto/java_dev/PokemmoMaxXY/脚本/go.bat");
~~~

打开cmd进行命令：

~~~java
ckage com.yangteng.dev.entity;

import java.io.IOException;

public class 脚本 {
    public static void main(String[] args) {
        Runtime rt = Runtime.getRuntime();
        Process p = null;
        try {
            String property = System.getProperty("user.dir");
            p = rt.exec("cmd.exe /c start\t"+property+"\\src\\main\\resources\\脚本\\go.bat");
        } catch (IOException e) {
            System.err.println("IO流异常");
            e.printStackTrace();
        }
    }
}
~~~



## 文件操作

获取当前项目根源目录:

~~~java
String property = System.getProperty("user.dir");
~~~

~~~java
String url = "...."
URL resource = getClass().getClassLoader().getResource(url);//注意如果有中文路径会乱码的
~~~

## MVVM监听值的变化



# JAVAWEB

## 1.第一个javaWeb程序

**servlet内置对象:**

1.servlet的配置对象ServletConfig类,使用方法:

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211125082831439.png" alt="image-20211125082831439" style="zoom:50%;" />

## 2. 解决tomcat乱码问题

找到：

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/20200312124030665.png)

将java.util.logging.ConsoleHandler.encoding = UTF-8 改成 java.util.logging.ConsoleHandler.encoding = GBK

# Spring

### 1.javaSpring-Mevan项目导入Spring

- 概述：**Spring相当于一个been的容器**，Spring所有封装对象包过SpringBoot最底层都是 `@Component`，在Mevan项目中导入Spring需要导入两个组件包spring-webmvc和spring-jdbc
- **Spring里面IOC和AOP是重点**，IOC说白了就是将JavaBeen交给Spring管理

```xml
<dependency>  
    <groupId>org.springframework</groupId>  
    <artifactId>spring-webmvc</artifactId>  
    <version>5.2.0.RELEASE</version>  
</dependency>  
<dependency>  
    <groupId>org.springframework</groupId>  
    <artifactId>spring-jdbc</artifactId>  
    <version>5.2.0.RELEASE</version>  
</dependency> 
```

+ **IOC-SpringXMLC和P的注入依赖**

```xml
导入约束 : xmlns:p="http://www.springframework.org/schema/p"  
<!--P(属性: properties)命名空间 , 属性依然要设置set方法-->  
<bean id="user" class="com.kuang.pojo.User" p:name="狂神" p:age="18"/>  
```

### 2.spring的第一个程序

```java
@Test
public void test(){
    //解析beans.xml文件 , 生成管理相应的Bean对象
    ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
    //getBean : 参数即为spring配置文件中bean的id .
    Hello hello = (Hello) context.getBean("hello");
    hello.show();
}
```

### 3.IOC-Spring的自动装配

- **使用xml进行Spring的自动装配**：需要加入 `autowire="byName"`属性，其中byName是自动扫描上下文，而使用 `autowire="byType"`则去扫描上文相关类。

```xml
xmlns:context="http://www.springframework.org/schema/context"  
http://www.springframework.org/schema/context  
http://www.springframework.org/schema/context/spring-context.xsd 
<context:annotation-config/>  

<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
       xmlns:context="http://www.springframework.org/schema/context"  
       xsi:schemaLocation="http://www.springframework.org/schema/beans  
                           http://www.springframework.org/schema/beans/spring-beans.xsd  
                           http://www.springframework.org/schema/context  
                           http://www.springframework.org/schema/context/spring-context.xsd">  
</beans>  

<!-- autowire="byName"   -->
<bean id="user" class="com.kuang.pojo.User" autowire="byName">
    <property name="str" value="qinjiang"/>
</bean>

<!-- autowire="byType"   -->
<bean id="dog" class="com.kuang.pojo.Dog"/>
<bean id="cat" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>
<bean id="user" class="com.kuang.pojo.User" autowire="byType">
    <property name="str" value="qinjiang"/>
</bean>
```

- **使用注解对javaSpring自动装配**：jdk1.5开始支持注解，spring2.5开始全面支持注解，利用注解的方式注入属性，在spring配置文件中引入context文件头。

  1.@Autowired能进行自动匹配：[@Autowired](https://github.com/Autowired)(required=false) 说明： false，对象可以为null；true，对象必须存对象，不能为null。

```xml
xmlns:context="http://www.springframework.org/schema/context"
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context.xsd
<!-- 开启注解支持   -->
<context:annotation-config/>
```

[@Qualifier](https://github.com/Qualifier) ，[@Autowired](https://github.com/Autowired)是根据类型自动装配的，加上[@Qualifier](https://github.com/Qualifier)则可以根据byName的方式自动装配[@Qualifier](https://github.com/Qualifier)不能单独使用，以解决配置文件跟类名不一致的问题

```xml
<bean id="dog1" class="com.kuang.pojo.Dog"/>
<bean id="dog2" class="com.kuang.pojo.Dog"/>
<bean id="cat1" class="com.kuang.pojo.Cat"/>
<bean id="cat2" class="com.kuang.pojo.Cat"/>
```

```java
@Autowired
@Qualifier(value = "cat2")
private Cat cat;
@Autowired
@Qualifier(value = "dog2")
private Dog dog;
```

###4.IOC-Spring用纯java的方式写Spring的配置文件

```java
@Configuration  //代表这是一个配置类
public class MyConfig {
    @Bean //通过方法注册一个bean，这里的返回值就Bean的类型，方法名就是bean的id！
    public Dog dog(){
        return new Dog();
    }
}
```

### 5.Aop1-代理模式

+ **代理模式本质**上是社会分工，同一个工业品交给一个人干，效率是极低的，但把他们拆成一个一个方法，使得彼此之间分工，生产商品的效率就提高了。
+ 代理模式分为**静态代理**和**动态代理**

  - **静态代理**：在原有的基础上再包装一个类，在原有基础上增加一个方法就行了

    ```java
    package com.wordtree.test;
    
    public class 静态代理 implements 真实角色{
        private UserBao userBao;
    
        public void setUserBao(UserBao userBao) {
            this.userBao = userBao;
        }
    
        @Override
        public void 增加() {
            userBao.增加();
        }
    
        @Override
        public void 删除() {
            userBao.删除();
        }
    
        @Override
        public void 修改() {
            userBao.修改();
        }
    }
    
    ```
  - **动态代理**：动态代理的本质通过反射实现方法

    ```java
    package com.wordtree.test;
    
    import java.lang.reflect.InvocationHandler;
    import java.lang.reflect.Method;
    import java.lang.reflect.Proxy;
    
    public class ProxyInvocationHandler implements InvocationHandler {
        private Object target;
    
        public void setRent(Object target) {
            this.target = target;
        }
    
        public Object getProxy(){
            return Proxy.newProxyInstance(this.getClass().getClassLoader(), target.getClass().getInterfaces(),this);
        }
        @Override
        public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
            Object result = method.invoke(target, args);
            return result;
        }
    
        public static void main(String[] args) {
            动态代理 动态 = new 动态代理();
            ProxyInvocationHandler proxy = new ProxyInvocationHandler();
            proxy.setRent(动态);
            真实角色 proxy1 = (真实角色)proxy.getProxy();
            proxy1.增加();
        }
    }
    ```
+ **SpringAop导入依赖包，以及实现代理**

```xml
<!-- https://mvnrepository.com/artifact/org.aspectj/aspectjweaver -->
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.4</version>
</dependency>
```

```java
public class Log implements MethodBeforeAdvice {
    //method : 要执行的目标对象的方法
    //objects : 被调用的方法的参数
    //Object : 目标对象
    @Override
    public void before(Method method, Object[] objects, Object o) throws Throwable {
        System.out.println( o.getClass().getName() + "的" + method.getName() + "方法被执行了");
    }
}

public class AfterLog implements AfterReturningAdvice {
    //returnValue 返回值
    //method被调用的方法
    //args 被调用的方法的对象的参数
    //target 被调用的目标对象
    @Override
    public void afterReturning(Object returnValue, Method method, Object[] args, Object target) throws Throwable {
        System.out.println("执行了" + target.getClass().getName()
        +"的"+method.getName()+"方法,"
        +"返回值："+returnValue);
    }
}
```

**xml代码方面**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:aop="http://www.springframework.org/schema/aop"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">
    <!--注册bean-->
    <bean id="userService" class="com.kuang.service.UserServiceImpl"/>
    <bean id="log" class="com.kuang.log.Log"/>
    <bean id="afterLog" class="com.kuang.log.AfterLog"/>
    <!--aop的配置-->
    <aop:config>
        <!--切入点  expression:表达式匹配要执行的方法-->
        <aop:pointcut id="pointcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
        <!--执行环绕; advice-ref执行方法 . pointcut-ref切入点-->
        <aop:advisor advice-ref="log" pointcut-ref="pointcut"/>
        <aop:advisor advice-ref="afterLog" pointcut-ref="pointcut"/>
    </aop:config>
</beans>
```

测试方法

```java
public class MyTest {
    @Test
    public void test(){
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        UserService userService = (UserService) context.getBean("userService");
        userService.search();
    }
}
```

Aop的重要性 : 很重要 . 一定要理解其中的思路 , 主要是思想的理解这一块 .

Spring的Aop就是将公共的业务 (日志 , 安全等) 和领域业务结合起来 , 当执行领域业务时 , 将会把公共业务加进来 . 实现公共业务的重复利用 . 领域业务更纯粹 , 程序猿专注领域业务 , 其本质还是动态代理 .

#### 第二种方式

**自定义类来实现Aop**

目标业务类不变依旧是userServiceImpl

第一步 : 写我们自己的一个切入类

```java
public class DiyPointcut {
    public void before(){
        System.out.println("---------方法执行前---------");
    }
    public void after(){
        System.out.println("---------方法执行后---------");
    }
}
```

去spring中配置

```xml
<!--第二种方式自定义实现-->
<!--注册bean-->
<bean id="diy" class="com.kuang.config.DiyPointcut"/>
<!--aop的配置-->
<aop:config>
    <!--第二种方式：使用AOP的标签实现-->
    <aop:aspect ref="diy">
        <aop:pointcut id="diyPonitcut" expression="execution(* com.kuang.service.UserServiceImpl.*(..))"/>
        <aop:before pointcut-ref="diyPonitcut" method="before"/>
        <aop:after pointcut-ref="diyPonitcut" method="after"/>
    </aop:aspect>
</aop:config>
```

测试

```java
public class MyTest {
    @Test
    public void test(){
        ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
        UserService userService = (UserService) context.getBean("userService");
        userService.add();
    }
}
```

#### 第三种方式

**使用注解实现**

第一步：编写一个注解实现的增强类

```java
package com.kuang.config;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
@Aspect
public class AnnotationPointcut {
    @Before("execution(* com.kuang.service.UserServiceImpl.*(..))")
    public void before(){
        System.out.println("---------方法执行前---------");
    }
    @After("execution(* com.kuang.service.UserServiceImpl.*(..))")
    public void after(){
        System.out.println("---------方法执行后---------");
    }
    @Around("execution(* com.kuang.service.UserServiceImpl.*(..))")
    public void around(ProceedingJoinPoint jp) throws Throwable {
        System.out.println("环绕前");
        System.out.println("签名:"+jp.getSignature());
        //执行目标方法proceed
        Object proceed = jp.proceed();
        System.out.println("环绕后");
        System.out.println(proceed);
    }
}
```

第二步：在Spring配置文件中，注册bean，并增加支持注解的配置

```xml
<!--第三种方式:注解实现-->
<bean id="annotationPointcut" class="com.kuang.config.AnnotationPointcut"/>
<aop:aspectj-autoproxy/>
```

aop:aspectj-autoproxy：说明

```xml
通过aop命名空间的<aop:aspectj-autoproxy />声明自动为spring容器中那些配置@aspectJ切面的bean创建代理，织入切面。当然，spring 在内部依旧采用AnnotationAwareAspectJAutoProxyCreator进行自动代理的创建工作，但具体实现的细节已经被<aop:aspectj-autoproxy />隐藏起来了 
<aop:aspectj-autoproxy />有一个proxy-target-class属性，默认为false，表示使用jdk动态代理织入增强，当配为<aop:aspectj-autoproxy  poxy-target-class="true"/>时，表示使用CGLib动态代理技术织入增强。不过即使proxy-target-class设置为false，如果目标类没有声明接口，则spring将自动使用CGLib动态代理。。
```

#### 使用纯java代码实现AOP

java配置类

~~~java
package com.study.good.config;

import com.study.good.entity.Person2;
import com.study.good.service.HelloService;
import com.study.good.service.HelloServiceImpl;
import com.study.good.test.MainXianQieMain;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.EnableAspectJAutoProxy;

@Configuration
@EnableAspectJAutoProxy //注意使用注解实现AOP必须要使用自动代理,也就是必须要加这个注解
public class SpringConfigContext {
    @Bean
    public Person2 Person2(){
        return new Person2(1,"你是猪","yt20020609");
    }

    @Bean
    public MainXianQieMain mainXianQieMain(){
        return new MainXianQieMain();
    }

    @Bean //注册该AOP方法实例
    public HelloService helloService(){
        return new HelloServiceImpl();
    }
}
~~~

AOP执行的方法

~~~java
package com.study.good.test;

import org.aspectj.lang.annotation.After;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class MainXianQieMain  {

    @Before("execution(* com.study.good.service.HelloServiceImpl.*(..))")
    public void before(){
        System.out.println("在指定接口执行前使用该方法");
    }
    @After("execution(* com.study.good.service.HelloServiceImpl.*(..))")
    public void hour(){
        System.out.println("在指定接口执行后使用该方法");
    }
}
~~~



# Mybatis

## 一.基本信息

[狂神SSM教程- 专栏 -KuangStudy](https://www.kuangstudy.com/zl/ssm#1377532368339955713)

- MyBatis 是一款优秀的**持久层框架**
- MyBatis 避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集的过程
- MyBatis 可以使用简单的 XML 或注解来配置和映射原生信息，将接口和 Java 的 实体类 【Plain Old Java Objects,普通的 Java对象】映射成数据库中的记录。
- MyBatis 本是apache的一个开源项目ibatis, 2010年这个项目由apache 迁移到了google code，并且改名为MyBatis 。
- 2013年11月迁移到**Github** .
- Mybatis官方文档 : http://www.mybatis.org/mybatis-3/zh/index.html
- GitHub : https://github.com/mybatis/mybatis-3



## 二.在idea中进行环境配置

1. maven导入依赖(java1.8版本)

   ```xml
   <dependencies>
       <!-- 导入依赖 -->
       <dependency>
           <groupId>mysql</groupId>
           <artifactId>mysql-connector-java</artifactId>
           <version>5.1.46</version>
       </dependency>
       <!--导入mybatis依赖-->
       <dependency>
           <groupId>org.mybatis</groupId>
           <artifactId>mybatis</artifactId>
           <version>3.5.6</version>
       </dependency>
       <!--导入测试类-->
       <dependency>
           <groupId>junit</groupId>
           <artifactId>junit</artifactId>
           <version>4.12</version>
       </dependency>
   </dependencies>
   ```

## 三：第一个Mybatis程序

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211112085641029.png" alt="image-20211112085641029" style="zoom:50%;" />

```xml
<!--处理用户业务逻辑-->
<mappers>
    <mapper resource="com/yangteng/study/dao/UserMapper.xml"/>
</mappers>
```

在配置文件里面添加上面的xml说明,下面是Mapper文件

**UserDao实体接口:**

```java
package com.yangteng.study.dao;

import com.yangteng.study.pjo.User;

import java.util.List;

public interface UserDao {
    //查询所有用户数据
    List<User> getAllUsers();
    //根据id查询用户数据
    User getUser(int id);
}
```

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.yangteng.study.dao.UserDao">
    <select id="getAllUsers" resultType="com.yangteng.study.pjo.User">
        select * from user_table
    </select>
    <select id="getUser" resultType="com.yangteng.study.pjo.User" parameterType="int">
        select * from user_table where id = #{id}
    </select>
</mapper>
```

**解决Maven过载问题:**

```xml
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
        <resource>
            <directory>src/main/resources</directory>
            <includes>
                <include>**/*.properties</include>
                <include>**/*.xml</include>
            </includes>
            <filtering>false</filtering>
        </resource>
    </resources>
</build>
```

## 四.增删改查

**注意**:增删改操作要写提交语句

javaDao：

```java
package com.yangteng.study.dao;

import com.yangteng.study.pjo.User;

import java.util.List;

public interface UserMapper {
    //查询所有用户数据
    List<User> getAllUsers();
    //根据id查询用户数据
    User getUser(int id);
    /**
     * 添加一个用户
     */
    int addUser(User user);
    /**
     * 删除一个用户
     */
    int delUser(int id);
    /**
     * 修改一个用户
     */
    int upDateUser(User user);
}

```

Mapper.xml层：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.yangteng.study.dao.UserMapper">
    <!--实际开发中往往遇到数据库名字与java中类的名字不一致的问题，除了可以在sql语句上修改之外，MyBatis还提供了一种特别的方案-->
    <resultMap id="aoteman" type="user">
        <result column="id" property="id"/>
        <result column="name" property="name"/>
        <result column="pwd" property="password"/>
    </resultMap>
    <!--查询所有数据-->
    <select id="getAllUsers" resultType="user" resultMap="aoteman">
        select * from user_table
    </select>
    <!--查询一条数据-->
    <select id="getUser" resultType="user" parameterType="int">
        select * from user_table where id = #{id}
    </select>
    <!--添加一个用户-->
    <insert id="addUser" parameterType="user">
        insert into user_table(id,name,password) value (#{id},#{name},#{password})
    </insert>
    <!--修改一个用户-->
    <update id="upDateUser" parameterType="user">
        update user_table
        set name = #{name},password = #{password}
        where id = #{id};
    </update>
    <!--删除一个用户-->
    <delete id="delUser" parameterType="int">
        delete
        from user_table
        where id = #{id};
    </delete>
</mapper>
```

Myba默认配置文件：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <!--使用外部资源绑定数据库-->
    <properties resource="Jdbc.properties">
        <!--这个的意思是在配置文件中添加下面的属性,当然一切以配置文件优先-->
        <property name="username" value="root"/>
    </properties>
    <settings>
        <setting name="logImpl" value="LOG4J"/>
    </settings>
    <!--添加类的别名-->
    <typeAliases>
    <!--这个是添加一个包下所有的别名，默认为改单词首字母小写-->
    <!--<package name="com.yangteng.study.pjo"/>-->
        <!--指定添加位置-->
        <typeAlias type="com.yangteng.study.pjo.User" alias="user"/>
    </typeAliases>
    <!--环境配置，连接的数据库，这里使用的是MySQL-->
    <environments default="mysql">
        <environment id="mysql">
            <!--指定事务管理的类型，这里简单使用Java的JDBC的提交和回滚设置-->
            <transactionManager type="JDBC"/>
            <!--dataSource 指连接源配置，POOLED是JDBC连接对象的数据源连接池的实现-->
            <dataSource type="POOLED">
                <property name="driver" value="${driverClassName}"/>
                <property name="url" value="${url}"/>
                <property name="username" value="${username}"/>
                <property name="password" value="${password}"/>
            </dataSource>
        </environment>
    </environments>
    <!--处理用户业务逻辑-->
    <mappers>
<!--        <mapper resource="com/yangteng/study/dao/UserMapper.xml"/>-->
        <package name="com.yangteng.study.dao"/>
    </mappers>

</configuration>
```

添加类的别名（有添加类和包两种方式）

```xml
    <!--添加类的别名-->
    <typeAliases>
    <!--这个是添加一个包下所有的别名，默认为改单词首字母小写-->
    <!--<package name="com.yangteng.study.pjo"/>-->
        <!--指定添加位置-->
        <typeAlias type="com.yangteng.study.pjo.User" alias="user"/>
    </typeAliases>
```

添加对于包的映射（注意这个要使dao接口与mapper.xml同名）：

```xml
    <!--处理用户业务逻辑-->
    <mappers>
<!--        <mapper resource="com/yangteng/study/dao/UserMapper.xml"/>-->
        <package name="com.yangteng.study.dao"/>
    </mappers>
```

## 五. log4j

使用log4j:(Myba配置文件)

```xml
    <settings>
        <setting name="logImpl" value="LOG4J"/>
    </settings>
```

log4j的资源文件:

```properties
# priority  :debug<info<warn<error
#you cannot specify every priority with different file for log4j
log4j.rootLogger=debug,stdout,info,debug,warn,error 

#console
log4j.appender.stdout=org.apache.log4j.ConsoleAppender 
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout 
log4j.appender.stdout.layout.ConversionPattern= [%d{yyyy-MM-dd HH:mm:ss a}]:%p %l%m%n
#info log
log4j.logger.info=info
log4j.appender.info=org.apache.log4j.DailyRollingFileAppender 
log4j.appender.info.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.info.File=./src/com/hp/log/info.log
log4j.appender.info.Append=true
log4j.appender.info.Threshold=INFO
log4j.appender.info.layout=org.apache.log4j.PatternLayout 
log4j.appender.info.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
#debug log
log4j.logger.debug=debug
log4j.appender.debug=org.apache.log4j.DailyRollingFileAppender 
log4j.appender.debug.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.debug.File=./src/com/hp/log/debug.log
log4j.appender.debug.Append=true
log4j.appender.debug.Threshold=DEBUG
log4j.appender.debug.layout=org.apache.log4j.PatternLayout 
log4j.appender.debug.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
#warn log
log4j.logger.warn=warn
log4j.appender.warn=org.apache.log4j.DailyRollingFileAppender 
log4j.appender.warn.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.warn.File=./src/com/hp/log/warn.log
log4j.appender.warn.Append=true
log4j.appender.warn.Threshold=WARN
log4j.appender.warn.layout=org.apache.log4j.PatternLayout 
log4j.appender.warn.layout.ConversionPattern=%d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
#error
log4j.logger.error=error
log4j.appender.error = org.apache.log4j.DailyRollingFileAppender
log4j.appender.error.DatePattern='_'yyyy-MM-dd'.log'
log4j.appender.error.File = ./src/com/hp/log/error.log 
log4j.appender.error.Append = true
log4j.appender.error.Threshold = ERROR 
log4j.appender.error.layout = org.apache.log4j.PatternLayout
log4j.appender.error.layout.ConversionPattern = %d{yyyy-MM-dd HH:mm:ss a} [Thread: %t][ Class:%c >> Method: %l ]%n%p:%m%n
```

接下来获取类输出就行了。

# Mybatis-plus

1. 准备相关依赖：`<font color='red'>`注意引入mybatis-plus以后就不用引入mybatis了`</font>`

```xml
<!--引入mybatis-plus-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus</artifactId>
    <version>3.4.2</version>
</dependency>
<!--引入mybatis-plus 在springboot里面注意他后面的启动类-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.0.5</version>
</dependency>
```

2. 使用mybatis-plus

```
使用mybatis-puls只需要实现相关接口就可以了,不需要写mapper资源文件。
```


3. plus能帮你自动生成id,利用雪花算法生成全球唯一的id

配置tableid也非常简单:只需要在该表对应的实体类里面加入tableId注解就行了

```java
    @TableId(type = IdType.AUTO)
    private int id;
	//下面是IdType的一些基本参数
	/**
     * 数据库ID自增
     */
    AUTO(0),
    /**
     * 该类型为未设置主键类型
     */
    NONE(1),
    /**
     * 用户输入ID
     * 该类型可以通过自己注册自动填充插件进行填充
     */
    INPUT(2),

    /* 以下3种类型、只有当插入对象ID 为空，才自动填充。 */
    /**
     * 全局唯一ID (idWorker)
     */
    ID_WORKER(3),
    /**
     * 全局唯一ID (UUID)
     */
    UUID(4),
    /**
     * 字符串全局唯一ID (idWorker 的字符串表示)
     */
    ID_WORKER_STR(5);
```

# SpringMVC

## 1.准备开发环境（这里直接使用注解开发）

1. 导入springmvc依赖（使用maven进行导入）

```xml
<!--这是springmvc的依赖-->
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>5.2.0.RELEASE</version>
</dependency>
<!--不能直接使用springmvc因为跟Tomcat里面的一个东西有冲突，需要导入下面这个包-->
<dependency>
    <groupId>javax</groupId>
    <artifactId>javaee-api</artifactId>
    <version>7.0</version>
    <scope>provided</scope>
</dependency>
```

2. 撰写web.xml的配置

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">
    <!--1.注册servlet-->
    <servlet>
        <servlet-name>SpringMVC</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!--通过初始化参数指定SpringMVC配置文件的位置，进行关联-->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:springmvc-servlet.xml</param-value>
        </init-param>
        <!-- 启动顺序，数字越小，启动越早 -->
        <load-on-startup>1</load-on-startup>
    </servlet>
    <!--所有请求都会被springmvc拦截 -->
    <servlet-mapping>
        <servlet-name>SpringMVC</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
</web-app>
```

3. 按照约定我们来写springmvc-servlet.xml的配置在资源目录下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 自动扫描包，让指定包下的注解生效,由IOC容器统一管理 -->
    <context:component-scan base-package="com.yangteng.controller"/>
    <!-- 让Spring MVC不处理静态资源 -->
    <mvc:default-servlet-handler />
    <!--
    支持mvc注解驱动
        在spring中一般采用@RequestMapping注解来完成映射关系
        要想使@RequestMapping注解生效
        必须向上下文中注册DefaultAnnotationHandlerMapping
        和一个AnnotationMethodHandlerAdapter实例
        这两个实例分别在类级别和方法级别处理。
        而annotation-driven配置帮助我们自动完成上述两个实例的注入。
     -->
    <mvc:annotation-driven />
    <!-- 视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
          id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/win/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
    </bean>
</beans>
```

## 2.第一个程序

1. 准备好开发环境,我们就可以写第一个程序了
2. web层:使用了两个注解Controller这个代表注册了控制器,RequestMapping这个指定路径,`return "hello"`表示要前往的文件名。

```java
package com.yangteng.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class Hello {
    @RequestMapping("/hello")
    public String helloWorld(Model model){
        model.addAttribute("msg","Hello World!");
        return "hello";
    }
}
```

## 3.常用注解

### 1.通过不同的注解限制请求

Spring MVC 的 [@RequestMapping](https://github.com/RequestMapping) 注解能够处理 HTTP 请求的方法, 比如 GET, PUT, POST, DELETE 以及 PATCH。

+ 我们可以通过不同的注解，限制服务器的请求

```java
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
@PatchMapping
```

### 2.请求转发与重定向

#### + 第一种是视图解释器

```xml
<!-- 视图解析器 -->
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver"
      id="internalResourceViewResolver">
    <!-- 前缀 -->
    <property name="prefix" value="/WEB-INF/jsp/" />
    <!-- 后缀 -->
    <property name="suffix" value=".jsp" />
</bean>
```

#### + 第二种是直接在控制器里面写返回值

`forward`这个参数为视图转发，`redirect`这个为请求重定向

```java
@Controller
public class ResultSpringMVC {
    @RequestMapping("/rsm/t1")
    public String test1(){
        //转发
        return "/index.jsp";
    }
    @RequestMapping("/rsm/t2")
    public String test2(){
        //转发二
        return "forward:/index.jsp";
    }
    @RequestMapping("/rsm/t3")
    public String test3(){
        //重定向
        return "redirect:/index.jsp";
    }
}
```

## 4.拦截器

**概念：**SpringMVC的处理器拦截器类似于Servlet开发中的过滤器Filter,用于对处理器进行预处理和后处理。开发者可以自己定义一些拦截器来实现特定的功能。拦截器是AOP思想的具体应用。

- 拦截器是SpringMVC框架自己的，只有使用了SpringMVC框架的工程才能使用
- 拦截器只会拦截访问的控制器方法， 如果访问的是jsp/html/css/image/js是不会进行拦截的

**编写一个拦截器：**

~~~java
package com.kuang.interceptor;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
public class MyInterceptor implements HandlerInterceptor {
    //在请求处理的方法之前执行
    //如果返回true执行下一个拦截器
    //如果返回false就不执行下一个拦截器
    public boolean preHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o) throws Exception {
        System.out.println("------------处理前------------");
        return true;
    }
    //在请求处理方法执行之后执行
    public void postHandle(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, ModelAndView modelAndView) throws Exception {
        System.out.println("------------处理后------------");
    }
    //在dispatcherServlet处理后执行,做清理工作.
    public void afterCompletion(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse, Object o, Exception e) throws Exception {
        System.out.println("------------清理------------");
    }
}
~~~

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/964016-20210107184637204-1018372234.png)

**在springmvc的配置文件中配置拦截器**

~~~xml
<!--关于拦截器的配置-->
<mvc:interceptors>
    <mvc:interceptor>
        <!--/** 包括路径及其子路径-->
        <!--/admin/* 拦截的是/admin/add等等这种 , /admin/add/user不会被拦截-->
        <!--/admin/** 拦截的是/admin/下的所有-->
        <mvc:mapping path="/**"/>
        <!--bean配置的就是拦截器-->
        <bean class="com.kuang.interceptor.MyInterceptor"/>
    </mvc:interceptor>
</mvc:interceptors>
~~~





## 文件上传与下载



# 整合SSM框架

## 一.问题以及解决方案

### 1.数据库连接失败问题：

这个不能放在配置文件里面，最好直接写在代码里面，不然就会报错，具体原因没有找到，还有请用德鲁伊的数据库连接池

下面是spring-dao.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">
    <!-- 配置整合mybatis -->
    <!-- 1.关联数据库文件 -->
    <context:property-placeholder location="classpath:database.properties"/>
    <!-- 2.数据库连接池 -->
    <!--数据库连接池
        dbcp  半自动化操作  不能自动连接
        c3p0  自动化操作（自动的加载配置文件 并且设置到对象里面）
    -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/cyh_database?serverTimezone=UTC"/>
        <property name="username" value="root"/>
        <property name="password" value="root"/>
    </bean>
    <!-- 3.配置SqlSessionFactory对象 -->
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
        <!-- 注入数据库连接池 -->
        <property name="dataSource" ref="dataSource"/>
        <!-- 配置MyBaties全局配置文件:mybatis-config.xml -->
        <property name="configLocation" value="classpath:mybatis-config.xml"/>
    </bean>
    <!-- 4.配置扫描Dao接口包，动态实现Dao接口注入到spring容器中 -->
    <!--解释 ： https://www.cnblogs.com/jpfss/p/7799806.html-->
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
        <!-- 注入sqlSessionFactory -->
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/>
        <!-- 给出需要扫描Dao接口包 -->
        <property name="basePackage" value="com.yangteng.dao"/>
    </bean>
</beans>
```

### 2.中文乱码问题

1. 除了配置过滤器一直,还要修改 `spring-mvc的默认编码`:在web.xml里面配置过滤器

```xml
 <!--配置全局过滤filter-->
<filter>
    <filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

2. 修改默认编码:(在spring-mvc.xml配置文件里面)

```xml
<!--自定义消息转换器的编码,解决后台传输json回前台时，中文乱码问题 -->
<bean id="stringHttpMessageConverter"
      class="org.springframework.http.converter.StringHttpMessageConverter">
    <constructor-arg value="UTF-8" />
</bean>
<mvc:annotation-driven>
    <mvc:message-converters>
        <ref bean="stringHttpMessageConverter" />
    </mvc:message-converters>
</mvc:annotation-driven>
```

### 3.out里面没有src文件的问题

1. `<font color="red">`问题:`</font>`

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211120191918985.png" alt="image-20211120191918985" style="zoom:50%;" />

2. 问题来源:是因为maven本身编译的问题,**不要在maven项目里面直接添加web框架,不然它会把这些文件视为同一等级进行编译**
3. 解决方案:重新创建一个javaEE项目,依次引入文件

### 4.如果下面的消息显示没有过滤器

就直接把所有过滤器都删了

### 5.JSON解析

请优先使用阿里的

```xml
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.60</version>
</dependency>
```

不行就物理导入

## 二.配置文件

### spring-dao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/mvc
    https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 配置SpringMVC -->
    <!-- 1.开启SpringMVC注解驱动 -->
    <mvc:annotation-driven />
    <!-- 2.静态资源默认servlet配置-->
    <mvc:default-servlet-handler/>
    <!-- 3.配置jsp 显示ViewResolver视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
        <property name="prefix" value="/viwe/jsp/" />
        <property name="suffix" value=".jsp" />
    </bean>
    <!-- 4.扫描web相关的bean -->
    <context:component-scan base-package="com.yangteng.controller" />

    <!-- ========================================分隔线========================================= -->
    <!--自定义消息转换器的编码,解决后台传输json回前台时，中文乱码问题 -->
    <bean id="stringHttpMessageConverter"
          class="org.springframework.http.converter.StringHttpMessageConverter">
        <constructor-arg value="UTF-8" />
    </bean>
    <mvc:annotation-driven>
        <mvc:message-converters>
            <ref bean="stringHttpMessageConverter" />
        </mvc:message-converters>
    </mvc:annotation-driven>
</beans>
```

### spring-mvc.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/mvc
    https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 配置SpringMVC -->
    <!-- 1.开启SpringMVC注解驱动 -->
    <mvc:annotation-driven />
    <!-- 2.静态资源默认servlet配置-->
    <mvc:default-servlet-handler/>
    <!-- 3.配置jsp 显示ViewResolver视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
        <property name="prefix" value="/viwe/jsp/" />
        <property name="suffix" value=".jsp" />
    </bean>
    <!-- 4.扫描web相关的bean -->
    <context:component-scan base-package="com.yangteng.controller" />

    <!-- ========================================分隔线========================================= -->
    <!--自定义消息转换器的编码,解决后台传输json回前台时，中文乱码问题 -->
    <bean id="stringHttpMessageConverter"
          class="org.springframework.http.converter.StringHttpMessageConverter">
        <constructor-arg value="UTF-8" />
    </bean>
    <mvc:annotation-driven>
        <mvc:message-converters>
            <ref bean="stringHttpMessageConverter" />
        </mvc:message-converters>
    </mvc:annotation-driven>
</beans>
```

### spring-service.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:mvc="http://www.springframework.org/schema/mvc"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd
    http://www.springframework.org/schema/context
    http://www.springframework.org/schema/context/spring-context.xsd
    http://www.springframework.org/schema/mvc
    https://www.springframework.org/schema/mvc/spring-mvc.xsd">
    <!-- 配置SpringMVC -->
    <!-- 1.开启SpringMVC注解驱动 -->
    <mvc:annotation-driven />
    <!-- 2.静态资源默认servlet配置-->
    <mvc:default-servlet-handler/>
    <!-- 3.配置jsp 显示ViewResolver视图解析器 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="viewClass" value="org.springframework.web.servlet.view.JstlView" />
        <property name="prefix" value="/viwe/jsp/" />
        <property name="suffix" value=".jsp" />
    </bean>
    <!-- 4.扫描web相关的bean -->
    <context:component-scan base-package="com.yangteng.controller" />

    <!-- ========================================分隔线========================================= -->
    <!--自定义消息转换器的编码,解决后台传输json回前台时，中文乱码问题 -->
    <bean id="stringHttpMessageConverter"
          class="org.springframework.http.converter.StringHttpMessageConverter">
        <constructor-arg value="UTF-8" />
    </bean>
    <mvc:annotation-driven>
        <mvc:message-converters>
            <ref bean="stringHttpMessageConverter" />
        </mvc:message-converters>
    </mvc:annotation-driven>
</beans>
```

### mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
<!--    别名-->
    <typeAliases>
        <package name="com.yangteng.pjo"/>
    </typeAliases>
<!--    mappers资源自动读取-->
    <mappers>
        <mapper resource="com/yangteng/dao/ChapterMapper.xml"/>
    </mappers>
</configuration>

```

### applicationContext.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <import resource="spring-dao.xml"/>
    <import resource="spring-service.xml"/>
    <import resource="spring-mvc.xml"/>
</beans>
```

### web.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

    <!--DispatcherServlet-->
    <servlet>
        <servlet-name>DispatcherServlet</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <!--一定要注意:我们这里加载的是总的配置文件，之前被这里坑了！-->
            <param-value>classpath:applicationContext.xml</param-value>
        </init-param>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>DispatcherServlet</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>
    <!--配置全局过滤filter-->
    <filter>
        <filter-name>CharacterEncodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>CharacterEncodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>

</web-app>
```

### database.properties

```properties
username=root
password=root
url=jdbc:mysql://localhost:3306/cyh_database?serverTimezone=UTC
driverClassName=com.mysql.cj.jdbc.Driver
initialSize=5
maxActive=10
```

### 依赖包

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.yangteng</groupId>
    <artifactId>demo2</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>demo2</name>
    <packaging>war</packaging>

    <properties>
        <maven.compiler.target>1.8</maven.compiler.target>
        <maven.compiler.source>1.8</maven.compiler.source>
        <junit.version>5.7.1</junit.version>
    </properties>

    <dependencies>
        <!--Junit-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
        </dependency>
        <!--数据库驱动-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.25</version>
        </dependency>
        <!-- 数据库连接池 -->
        <dependency>
            <groupId>com.mchange</groupId>
            <artifactId>c3p0</artifactId>
            <version>0.9.5.2</version>
        </dependency>
        <!--Servlet - JSP -->
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>servlet-api</artifactId>
            <version>2.5</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet.jsp</groupId>
            <artifactId>jsp-api</artifactId>
            <version>2.2</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>jstl</artifactId>
            <version>1.2</version>
        </dependency>
        <!--Mybatis-->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.2</version>
        </dependency>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis-spring</artifactId>
            <version>2.0.2</version>
        </dependency>
        <!--Spring-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>5.1.9.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-jdbc</artifactId>
            <version>5.1.9.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>RELEASE</version>
            <scope>compile</scope>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.60</version>
        </dependency>
    </dependencies>
    <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.3.1</version>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>9</source>
                    <target>9</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```

### 测试类

```java
package com.yangteng.controller;

import com.alibaba.fastjson.JSON;
import com.yangteng.pjo.Chapter;
import com.yangteng.service.ChapterService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import java.util.List;

@Controller
public class AoTeManController {

    @Autowired
    @Qualifier("ChapterServiceImpl")
    private ChapterService bookService;

    @RequestMapping("/bianshen")
    @ResponseBody
    public String bianshen(){
        System.out.println("访问了ssm后台");
        List<Chapter> allChapter = bookService.getAllChapter();
        String s = JSON.toJSONString(allChapter);
        System.out.println(s);
        return s;
    }

    @RequestMapping("/chaojie")
    public String chaojie(String yt,Model model){
        model.addAttribute("yt",yt);
        return "hehe";
    }
}

```

### 大神过滤

```java
package com.yangteng.filter;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletRequestWrapper;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.util.Map;
/**
 * 解决get和post请求 全部乱码的过滤器
 */
public class GenericEncodingFilter implements Filter {
    @Override
    public void destroy() {
    }
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        //处理response的字符编码
        HttpServletResponse myResponse=(HttpServletResponse) response;
        myResponse.setContentType("text/html;charset=UTF-8");
        // 转型为与协议相关对象
        HttpServletRequest httpServletRequest = (HttpServletRequest) request;
        // 对request包装增强
        HttpServletRequest myrequest = new MyRequest(httpServletRequest);
        chain.doFilter(myrequest, response);
    }
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }
}
//自定义request对象，HttpServletRequest的包装类
class MyRequest extends HttpServletRequestWrapper {
    private HttpServletRequest request;
    //是否编码的标记
    private boolean hasEncode;
    //定义一个可以传入HttpServletRequest对象的构造函数，以便对其进行装饰
    public MyRequest(HttpServletRequest request) {
        super(request);// super必须写
        this.request = request;
    }
    // 对需要增强方法 进行覆盖
    @Override
    public Map getParameterMap() {
        // 先获得请求方式
        String method = request.getMethod();
        if (method.equalsIgnoreCase("post")) {
            // post请求
            try {
                // 处理post乱码
                request.setCharacterEncoding("utf-8");
                return request.getParameterMap();
            } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
            }
        } else if (method.equalsIgnoreCase("get")) {
            // get请求
            Map<String, String[]> parameterMap = request.getParameterMap();
            if (!hasEncode) { // 确保get手动编码逻辑只运行一次
                for (String parameterName : parameterMap.keySet()) {
                    String[] values = parameterMap.get(parameterName);
                    if (values != null) {
                        for (int i = 0; i < values.length; i++) {
                            try {
                                // 处理get乱码
                                values[i] = new String(values[i]
                                                       .getBytes("ISO-8859-1"), "utf-8");
                            } catch (UnsupportedEncodingException e) {
                                e.printStackTrace();
                            }
                        }
                    }
                }
                hasEncode = true;
            }
            return parameterMap;
        }
        return super.getParameterMap();
    }
    //取一个值
    @Override
    public String getParameter(String name) {
        Map<String, String[]> parameterMap = getParameterMap();
        String[] values = parameterMap.get(name);
        if (values == null) {
            return null;
        }
        return values[0]; // 取回参数的第一个值
    }
    //取所有值
    @Override
    public String[] getParameterValues(String name) {
        Map<String, String[]> parameterMap = getParameterMap();
        String[] values = parameterMap.get(name);
        return values;
    }
}
```

# SpringBoot

## 1.一些错误

### # 测试类无法启动的原因：

![image-20211202093349635](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211202093349635.png)

spring在初始化的时候会把所有用到注解的地方，需要实例化的对象给实例化，所以有的时候使用一些注解就无法成功

![image-20211202093507316](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211202093507316.png)

## 2.yaml文件的语法，与向javaBean中赋值

## 3.303校验

```java
@Validated //这个表示开启数据校验
```

在对应的属性位置加注释就行了其中，还可以这样写：message会告诉你报错的信息

```java
@Email(message = "邮箱不正确") //开启邮箱验证
```

下面是一些基本操作，注意最后一个，为正则表达式

![img](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/3145530-8ae74d19e6c65b4c)

## 4.多环境配置

1. 在多环境配置配置中采用yaml进行,在核心yaml中可以切换不同的yaml文件
2. 代码:切换文件代码（active这个词语的意思大致有现代的意思）

```yaml
#设置端口号为8082
server:
  port: 8082

#这个可以切换默认的配置文件
spring:
  profiles:
    active: dev #直接写文件名就行了,比如这样application-x.yaml,写x就行了
    include: email,xmyb
#你还可以这样写https://www.webjars.org/
#spring.profiles.active=y
#设置一个叫做person的对象
person:
  name:
  age:
#使用分割线可以重新划分不同的配置
---
server:
  port: 8077
spring:
  profiles: dev #这个表示文件名称
```

>  ![image-20211207220638582](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211207220638582.png)

3. 注意给yaml对象赋值的时候,千万:后面要加空格,yaml对空格有严格的要求

## 5.配置开发环境

1. 引入jar包需要到webJars上面去找

> [WebJars - Web Libraries in Jars](https://www.webjars.org/)

2. 在springBoot,我们可以使用以下方式处理静态资源,这些目录下的文件可以直接访问

+ `webjars`
+ `public,static,/**/resource`

如果在同一级目录下的同名文件

resource>static>public

## 6.项目实战

**热部署:**

```xml
<parent>
<!--springboot启动类-->
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.0.1.RELEASE</version>
</parent>
<dependencies>
<!--嵌套了tomcat的web应用-->
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-web</artifactId>
	</dependency>
	<!--热部署-->
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-devtools</artifactId>
	</dependency>
</dependencies>

```

## 7.模板引擎*Thymeleaf*

**坑点:**

放在Thymeleaf下面他会给你报一个灰色的线

> <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211122174101868.png" alt="image-20211122174101868" style="zoom:50%;" />

**基本信息:**
使用maven引入thymeleaf(百里香)

```xml
<!--thymeleaf-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

<font color="#40a9ff">`||模板引擎`</font>

> 前端交给我们的页面，是html页面。如果是我们以前开发，我们需要把他们转成jsp页面，jsp好处就是当我们查出一些数据转发到JSP页面以后，我们可以用jsp轻松实现数据的显示，及交互等。
>
> jsp支持非常强大的功能，包括能写Java代码，但是呢，我们现在的这种情况，SpringBoot这个项目首先是以jar的方式，不是war，像第二，我们用的还是嵌入式的Tomcat，所以呢，**他现在默认是不支持jsp的**。
>
> 那不支持jsp，如果我们直接用纯静态页面的方式，那给我们开发会带来非常大的麻烦，那怎么办呢？
>
> **SpringBoot推荐你可以来使用模板引擎：**
>
> 模板引擎，我们其实大家听到很多，其实jsp就是一个模板引擎，还有用的比较多的freemarker，包括SpringBoot给我们推荐的Thymeleaf，模板引擎有非常多，但再多的模板引擎，他们的思想都是一样的，什么样一个思想呢我们来看一下这张图：

**基本语法：**详细见javaStudy目录下面的官方文档

## 8.基本工具类的使用

### 1. 拦截器

实现HandlerInterceptor接口即可

~~~java
public class MyInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {

        return HandlerInterceptor.super.preHandle(request, response, handler);
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

        HandlerInterceptor.super.postHandle(request, response, handler, modelAndView);
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

        HandlerInterceptor.super.afterCompletion(request, response, handler, ex);
    }
}
~~~

### 2.在服务端解决跨域问题

1. 一种是加`@CrossOrigin`注解

~~~java
@CrossOrigin(origins = {"*"},maxAge = -1)//允许服务器跨域访问，origins属性表示允许那一个服务器访问，默认是*就是所有的服务器
~~~

2. 一种是配置全局对象类

~~~java
package com.yangteng.demo.controller;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class TestController {
    @RequestMapping("/test")
    public String getTest(){

        return "Hello World!";
    }
}

~~~



# 雷神说SpringBoot

## 一.入门基础

### 1. springBoot开发文档

+ 中文文档： [四、Spring Boot 特性 · Spring Boot 中文文档 (felord.cn)](https://felord.cn/_doc/_springboot/2.1.5.RELEASE/_book/pages/spring-boot-features.html#boot-features-external-config-application-property-files)

+ 雷神的笔记文档： [03、了解自动配置原理 · 语雀 (yuque.com)](https://www.yuque.com/atguigu/springboot/qb7hy2#7DTGl)
+ 狂神的笔记文档：https://mp.weixin.qq.com/mp/homepage?__biz=Mzg2NTAzMTExNg==&hid=1&sn=3247dca1433a891523d9e4176c90c499
+ spring配置文件参考：https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html#common-application-properties

### 2. SpringBoot 自动装配原理

最重要的是这样一个注解:

> ![image.png](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/1602835786727-28b6f936-62f5-4fd6-a6c5-ae690bd1e31d.png)

+ 这个注解表示要是为导入相关依赖,就执行或者不执行下面的操作。

+ 在springboot底层源码中帮我们做了大量的工作，这些工作中约定大于配置，要是用户在相关约定处配置了SpringBoot依赖的配置则以用户的配置优先
+ 比如说该图就是用户自定义的配置：![image-20211207213213639](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211207213213639.png)

![image-20211207213444957](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211207213444957.png)

![image-20211207213620411](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211207213620411.png)

## 二. 常用注解

| 名称                                       | 参数           | 作用                                 |
| ------------------------------------------ | -------------- | ------------------------------------ |
| @SpringBootConfiguration @Configuration    |                | 代表当前是一个配置类                 |
| @ComponentScan                             | 填包的名称     | 指定扫描哪些，Spring注解；           |
| @ConfigurationProperties(prefix = "mycar") | 绑定对象的名称 | 到配置文件中去绑定一个指定名称的对象 |

~~~xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
~~~

~~~java
@PathVariable //这个注解用于书写路径相关
@RequestHeader、
@ModelAttribute、
@RequestParam、//这个注解很常见了,用于表达不清楚的传参或者指定默认参数
@MatrixVariable、
@CookieValue、
@RequestBody
~~~

### 传参注解

#### @PathVariable 

**介绍**:这个注解用于书写路径相关

~~~java
    //对一些常用注解的简单使用,对路径变量的使用
    @RequestMapping("/testZhuJie/name/{name}/age/{age}")
    public HashMap<String,Object> testZhuJie(@PathVariable("name") String name,        @PathVariable("age")String age,@PathVariable Map map){
        HashMap<String, Object> hashMap = new HashMap<String,Object>();
        hashMap.put("age", age);
        hashMap.put("name", name);
        hashMap.put("map", map);

        return hashMap;
    }
~~~

#### @RequestParam

**介绍:**这个注解很常见了,用于表达不清楚的传参或者指定默认参数

~~~java
    @RequestMapping("/selectCollectAll")
    @AuthCheck
    public String getCollectProductAll(@RequestParam(name = "page",defaultValue = "0") int page,
                                       @RequestParam(name = "size",defaultValue = "10") int size,
                                       String type){
        QueryWrapper<StoreProductRelation> queryWrapper = new QueryWrapper<>();
        queryWrapper.eq("uid", LocalUser.getUser().getUid())
                .eq("type",type);
        Page<StoreProductRelation> selectPage = stm.selectPage(new Page<StoreProductRelation>(page, size), queryWrapper);
        ArrayList<Map<String, Object>> maps = new ArrayList<>();
        for (StoreProductRelation record : selectPage.getRecords()) {
            StoreProduct storeProduct = st.selectById(record.getProductId());
            HashMap<String, Object> map = new HashMap<>();
            map.put("obj",storeProduct);
            map.put("rid",record.getId());
            maps.add(map);
        }
        return JSON.toJSONString(maps);
    }
~~~



### 万能的map集合

map集合加上RequestParam注解之后可以当做js里面的匿名对象使用

![image-20211212152917251](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211212152917251.png)

~~~java
    @RequestMapping("/testER2")
    public Map<String,Object> testER2(@RequestParam Map map){
        HashMap<String, Object> hashMap = new HashMap<String,Object>();
        hashMap.put("map", map);
        return hashMap;
    }
~~~

接受之前所有参数：

![image-20211212152943050](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211212152943050.png)

## 三.关于传参的一些问题

### 1. 首先,关于前端post请求data:

+ **注意：**在java中接受来自post请求data 的参数只能将参数加上@RequestBody注解才能使用,无论是变量还是对象还是数组,都要加上@RequestBody注解。

前端代码:

~~~javascript
    let i = [1,2,3,4,5,6]
    req({
      url:'/postArr',
      method:'post',
      data:{
        ids:i,
        type:"多谢",
        name:"乐天"
      }
    })
~~~

后端运行结果,注意map是不能接受这个对象的,甚至map什么都不能接受

> ![image-20211215170332002](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211215170332002.png)

+ **注意：**当前端post请求data传递的是一个对象的时候，后端接受可以使用对象，也可以使用map去接受该参数，但是顺序不能出错，切必须要加上**@RequestBody**

这里正是请求的接受出错了:

> ![image-20211215171011887](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211215171011887.png)

使用map去接受前端的参数：

> ![image-20211215171429101](C:\Users\有天道\AppData\Roaming\Typora\typora-user-images\image-20211215171429101.png)

+ **注意：**数组不能直接用get请求传参，最好用post请求进行传参



# javafx

## 基本操作列表

- 官方链接地址[Overview (JavaFX 17) (openjfx.cn)](https://openjfx.cn/javadoc/17/)
- javafx第一个程序—>推荐用kotlin编写javafx,以下笔记都会有kotlin来编写代码
	```Kotlin
	/**
	 * 写一个笔记本的代码哦
	 */
	class Notebook : Application() {
	    override fun start(stage: Stage) {
	        val box = VBox()
	        //这个是javafx里面的文字链接
	        val like = Hyperlink()
	        like.text = "www.baidu.com"
	        like.setOnAction {
	            this.hostServices.showDocument(like.text)
	        }
	        box.children.setAll(like)
	        stage.scene = Scene(box)
	        stage.width = 800.0
	        stage.height = 700.0
	        stage.show()
	    }
	}
	
	//这个是java代码调用kotlin
	public class Main {
	    public static void main(String[] args) {
	        Application.launch(Notebook.class,args);
	    }
	}
	
	```
	
- 打开文字链接，跳转到浏览器：
	```Kotlin
	/**
	 * 写一个笔记本的代码哦
	 */
	class Notebook : Application() {
	    override fun start(stage: Stage) {
	        val box = VBox()
	        //这个是javafx里面的文字链接
	        val like = Hyperlink()
	        like.text = "www.baidu.com"
	        like.setOnAction {
	            this.hostServices.showDocument(like.text)
	        }
	        box.children.setAll(like)
	        stage.scene = Scene(box)
	        stage.width = 800.0
	        stage.height = 700.0
	        stage.show()
	    }
	}
	```
	
- 布局方式
	- VBox()—垂直方向的布局管理,HBox—水平方向的布局管理
		```Kotlin
		//常用方法
		//添加组件
		box.add()
		box.addAll()
		//设置组件之间的间距
		box.spacing = 10
		//设置组件之间的位置
		box.alignment = Pos.BOTTOM_RIGHT
		//所有组件设置本身的位置都一样,相对于父组件来说
		box.layoutY
		box.layoutX
		box.padding = Insets(0.0, 100.0, 0.0, 0.0)
		
		```
		
		![](C:\Users\有天道\Desktop\seed\javaStudy\image\image.png "")
		
	- AnchorPane绝对布局
		默认将组件全部放置在左上角,用于管理子组件,当用这个类去管理子组件时,默认的设置组件的位置就不有效了
		```Kotlin
		        val button = Button("这个是用于测试的按钮")
		        val pane = AnchorPane()
		        AnchorPane.setBottomAnchor(button,10.0)
		        AnchorPane.setLeftAnchor(button,10.0)
		        AnchorPane.setRightAnchor(button,10.0)
		        AnchorPane.setTopAnchor(button,10.0)
		        pane.children.add(button)
		```
		
		![](C:\Users\有天道\Desktop\seed\javaStudy\image\image_1.png "")
		~~最后的效果~~
	- Group 这个是捆绑的容器,就是用来放置组件的,没有什么用处
	- **BorderPane**(这个是方位布局)
		![](C:\Users\有天道\Desktop\seed\javaStudy\image\image_2.png "")
- 设置组件的背景
	- 这个是设置背景图片
	```Kotlin
	        //这下面是box的操作
	        box.children.setAll(button1,button2,button3,button4)
	        box.background = Background(BackgroundImage(Image(FileToolYt.获取_根源目录()+"img/hutao.jpg"),null,null,null,null))
	
	```
	
	- 设置背景图片大小自适应并且不重复
	```Kotlin
	 //这个是拿来用的,要理解请自己看源代码去
	 //设置背景不重复,BackgroundRepeat.NO_REPEAT
	 //设置背景自适应,Image(FileToolYt.获取_根源目录()+"img/hutao.jpg",stage.width,stage.height,true,true),可以去看一下Image的官方文档,文档里面说得很详细
	 box.background = Background(BackgroundImage(Image(FileToolYt.获取_根源目录()+"img/hutao.jpg",stage.width,stage.height,true,true),BackgroundRepeat.NO_REPEAT,BackgroundRepeat.NO_REPEAT,null,null))
	
	```
	
	- 下面这个是设置颜色背景`Color.valueOf("#ff7875") ` 颜色的话一般用这个吧,看源码我是吐了
	```Kotlin
	        box.children.setAll(button1,button2,button3,button4)
	        box.background = Background(BackgroundFill(Color.rgb(255, 120, 117),null,null))
	```
	
- 树状图组件TreeView
	- 官方文档位置:
		[TreeView (JavaFX 17) (openjfx.cn)](https://openjfx.cn/javadoc/17/javafx.controls/javafx/scene/control/TreeView.html)
		[TreeItem (JavaFX 17) (openjfx.cn)](https://openjfx.cn/javadoc/17/javafx.controls/javafx/scene/control/TreeItem.html)
		[JavaFX视频教程第101课，TreeView的基本使用_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1pb41127k7/?spm_id_from=pageDriver)
	- 基本方法
		```Kotlin
		//TreeItem方法:
		//设置默认展开
		treeImage.isExpanded = true
		treeImage.value = "是色图哦"
		treeImage.isLeaf //返回false表示下面有子节点,反之相反
		//TreeView方法:
		//如果面积不够,则滚动到多少
		treeView.scrollTo(13)
		//设置单元格的尺寸
		treeView.fixedCellSize = 20.0
		//这里表示是否显示根节点,我这里设置不显示根节点
		treeView.isShowRoot = false
		
		```
		
	- 下面是一个小项目(一个简单的相册)
		```Kotlin
		        //定义头部公共部分
		        val rootPane = BorderPane()
		        val treeItem = TreeItem<String>()
		        val label = VBox()
		
		        //这个是左界面的编写
		        val file = File("${FileToolYt.获取_根源目录()}img")
		        val fileList = file.listFiles()//获取这个目录里面的图片
		        for (file in fileList) {
		            val item = TreeItem(file.name)
		            item.addEventHandler(MouseEvent.MOUSE_CLICKED) {
		                println(file.path)
		            }
		            treeItem.children.add(item)
		        }
		
		        val treeView = TreeView(treeItem)
		        rootPane.left = treeView
		
		        //这个是右界面的编写
		        rootPane.center = label
		        stage.scene = Scene(rootPane)
		        stage.width = 1000.0
		        stage.height = 800.0
		        stage.icons.add(Image("${FileToolYt.获取_根源目录()}img/icon.png"))
		        stage.show()
		```
		
		![](C:\Users\有天道\Desktop\seed\javaStudy\image\image_3.png "")
	
- 打包
	复制这段代码进去，点击package就可以打包成功了，嘻嘻
	```XML
	<build>
	        <finalName>untitled.0.1</finalName><!-- 导出jar的名字 -->
	        <plugins>
	            <plugin>
	                <groupId>org.apache.maven.plugins</groupId>
	                <artifactId>maven-shade-plugin</artifactId>
	                <version>3.2.0</version>
	                <executions>
	                    <execution>
	                        <phase>package</phase>
	                        <goals>
	                            <goal>shade</goal>
	                        </goals>
	                        <configuration>
	                            <transformers>
	                                <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
	                                    <mainClass>com.yangteng.Run</mainClass>
	                                    <!-- 主类的位置，例如上图文件，主类配置应为： -->
	                                    <!-- <mainClass>{top.nihilwater.App}</mainClass> -->
	                                </transformer>
	                            </transformers>
	                        </configuration>
	                    </execution>
	                </executions>
	            </plugin>
	        </plugins>
	    </build>
	```
	
	![](C:\Users\有天道\Desktop\seed\javaStudy\image\image_4.png "")
- 项目实现(这都是一些小项目)
	- 计算器项目
		```Kotlin
		//计算器
		class AppComputer() : Stage() {
		    private var x = 0
		    private var y = 0
		    private var moshi = true
		    private val  text = Text()
		    private val  jisuan = Text()
		    private val  text2 = Text()
		    private var result = Text()
		    private var  sum = 0.0
		    init {
		        println("这个是构造函数")
		        val gridPane = GridPane()
		        val box = VBox()
		        text.text = x.toString()
		        text2.text = ""
		        gridPane.vgap = 5.0
		        gridPane.hgap = 5.0
		
		        //设置计算机的按钮
		        val button1 = Button("1")
		        val button2 = Button("2")
		        val button3 = Button("3")
		        val button4 = Button("4")
		        val button5 = Button("5")
		        val button6 = Button("6")
		        val button7 = Button("7")
		        val button8 = Button("8")
		        val button9 = Button("9")
		        val button0 = Button("0")
		
		        val butJia = Button("+")
		        butJia.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "+"
		        }
		        val butJian = Button("-")
		        butJian.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "-"
		        }
		        val butChen = Button("*")
		        butChen.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "*"
		        }
		        val butChu = Button("/")
		        butChu.setOnMouseClicked {
		            moshi = false
		            jisuan.text = "/"
		        }
		        val butGui = Button("归零")
		        butGui.setOnMouseClicked {
		            x = 0
		            y = 0
		            moshi = true
		            jisuan.text = ""
		            text2.text = ""
		            text.text = ""
		            sum = 0.0
		            result.text = ""
		        }
		        val butX = Button("<-")
		        butX.setOnMouseClicked {
		            if(moshi){
		                if(text.text.length>0){
		                    text.text = jianText(text.text).trim()
		                    x = if (text.text.isNotEmpty()) text.text.toInt() else 0
		                }else{
		                    moshi = false
		                }
		            }else{
		                if(text2.text.length>0){
		                    text2.text = jianText(text2.text).trim()
		                    y = if (text2.text.isNotEmpty()) text2.text.toInt() else 0
		                }else{
		                    jisuan.text = jianText(jisuan.text)
		                    moshi = true
		                }
		            }
		            jisuanResult()
		        }
		        val butDenyu = Button("=")
		        butDenyu.setOnMouseClicked {
		            jisuanResult()
		        }
		        gridPane.addColumn(0,button1,button2,button3,button4,button5)
		        gridPane.addColumn(1,button6,button7,button8,button9,button0)
		        for (child in gridPane.children) {
		            child.setOnMouseClicked {
		                inputText(child as Button,text,text2)
		            }
		        }
		        gridPane.addColumn(2,butJia,butJian,butChen,butChu,butGui)
		        gridPane.addColumn(3,butX,butDenyu)
		        //设置背景图片
		        try {
		            box.background = Background(BackgroundImage(Image("${FileToolYt.获取_根源目录()}img/img.png"),null,null,null,null))
		        }catch (e:IllegalArgumentException){
		            println("没有找到资源！")
		        }
		        val hBox = HBox()
		        hBox.children.addAll(text,jisuan,text2,result)
		        hBox.alignment = Pos.CENTER
		        box.children.addAll(hBox,gridPane)
		        //设置组件居中显示
		        box.alignment = Pos.CENTER
		        box.spacing = 10.0
		        gridPane.alignment = Pos.CENTER
		        val scene = Scene(box)
		        this.scene = scene
		        width = 400.0
		        height = 600.0
		    }
		    private fun inputText(button:Button,text1:Text,text2:Text){
		        if(moshi){
		            x = (x.toString() + button.text).toInt()
		            text.text = x.toString()
		        }else{
		            y = (y.toString() + button.text).toInt()
		            text2.text = y.toString()
		        }
		    }
		    private fun jianText(s:String):String{
		        var newS = ""
		        val split = s.split("")
		        var mou = 0
		        if(split.size - 1>0){
		            mou = split.size - 2
		            val subList = split.subList(0,mou)
		            for (ss in subList) {
		                newS += ss
		            }
		            return newS
		        }else{
		            return newS
		        }
		    }
		    private fun jisuanResult(){
		        when(jisuan.text){
		            "+"->sum = (x+y).toDouble();
		            "*"->sum = (x*y).toDouble();
		            "/"->sum = (x/y).toDouble();
		            "-"->sum = (x-y).toDouble();
		            else->sum = (x+y).toDouble()
		        }
		        result.text = "= ${sum}"
		    }
		}
		```
		
	- 图片显示器
		```Kotlin
		//这个是图片查看器
		class totalPage : Application() {
		    //定义头部公共部分
		    private val rootPane = BorderPane()
		    private val treeRoot = TreeItem<String>()
		    private val label = VBox()
		    private val treeImage = TreeItem<String>("图片")
		    private val file = File("${FileToolYt.获取_根源目录()}img")
		    private val fileList = file.listFiles()
		
		    override fun start(stage: Stage) {
		        val computer = AppComputer()
		        treeRoot.value = "工作区"//这个用于设定和更改所在节点的名称
		        treeRoot.isExpanded = true //设置默认展开
		        //这个是左界面的编写
		        navigation()
		        val treeView = TreeView(treeRoot)
		        //设置左侧选择事件
		        treeView.selectionModel.selectedItemProperty().addListener(
		            ChangeListener<TreeItem<String>>(
		                fun(
		                    observable: ObservableValue<out TreeItem<String>>?,
		                    oldValue: TreeItem<String>?,
		                    newValue: TreeItem<String>?
		                ) {
		                    when(newValue?.value){
		                        "计算机"-> computer.show()
		                    }
		                    for (file in fileList) {
		                        if(file.name == newValue?.value){
		                            bgImage(label,file.path,stage)
		                        }
		                    }
		                })
		        )
		
		        //最下面是一些基本设置
		        treeView.isShowRoot = false //这里表示是否显示根节点,我这里设置不显示根节点
		        treeView.scrollTo(13)//如果面积不够,则滚动到多少
		
		        //这个是右界面的编写
		        rootPane.center = label
		        rootPane.left = treeView
		        stage.scene = Scene(rootPane)
		        stage.width = 1000.0
		        stage.height = 800.0
		        stage.icons.add(Image("${FileToolYt.获取_根源目录()}img/icon.png"))
		        stage.show()
		    }
		
		    fun bgImage(label: Pane, src: String, stage: Stage) {
		        label.background =
		            Background(
		                BackgroundImage(
		                    Image(src, stage.width * 0.7, stage.height, true, true),
		                    BackgroundRepeat.NO_REPEAT,
		                    BackgroundRepeat.NO_REPEAT,
		                    null,
		                    null
		                )
		            )
		    }
		    fun navigation(){
		        for (file in fileList) {
		            val item = TreeItem(file.name)
		            treeImage.children.add(item)
		        }
		        val itemJ = TreeItem("计算机")
		        val itemT = TreeItem("坦克")
		        treeRoot.children.addAll(treeImage,itemJ,itemT)
		    }
		}
		```
	
- javafx组件的一些基本操作
	```Kotlin
	isMouseTransparent //设置鼠标无法操作该组件
	textFill//设置组件字体颜色
	-fx-opacity: 0.4;//设置组件透明,最好不要用style属性,这个会覆盖之前设置的属性
	 children.opacity = 0.6 //设置透明度
	
	```
