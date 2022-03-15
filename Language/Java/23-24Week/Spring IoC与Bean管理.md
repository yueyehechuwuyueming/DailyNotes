# 第一节 Spring IoC与Bean管理

## 2 Spring快速入门

### IoC控制反转（Inverse of Control）

对象的控制权转移到中间角色统一调配

- 一种设计理念，宏观，现代程序设计遵循的标准
- 由代理人来创建与管理对象，消费者通过代理人来获取对象
- IoC的目的是降低对象之间直接耦合
- 加入IoC容器将对象统一管理，让对象关联变为弱耦合
- 苹果对象的创建权限由顾客转嫁到中间角色果商，冷冻仓库集中存储苹果，就是IoC容器；顾客需要的对象都是从IoC容器（冷冻仓库）中提取
- ![image-20220312215724074](http://r8m8y4rji.hn-bkt.clouddn.com/img/202203122157118.png)

#### DI依赖注入（Dependency Injection）

- IoC的具体技术实现，微观实现
- 在运行过程中完成对象的创建和绑定工作
- DI在Java中利用**反射**技术实现注入（Injection）@疑问

#### 例题

![image-20220312222559586](http://r8m8y4rji.hn-bkt.clouddn.com/img/202203122225635.png)

### Spring介绍

#### Spring

- Spring make Java simple
- 狭义Spring：Spring框架（Spring Framework）
  - 企业开发复杂性的一站式解决方案
  - Spring框架的核心是**IoC容器**和**AOP面向切面编程**
  - Spring IoC负责创建和 管理对象，并在基础上扩展功能
  - Spring Framework
    - OVERVIEW
      - The Spring Framework provides a comprehensive programming and configuration model for modern Java-based enterprise applications - on any kind of deployment platform.
      - A key element of Spring is infrastructural support at the application level: Spring focuses on the "plumbing" of enterprise applications so that teams can focus on application-level business logic, without unnecessary ties to specific deployment environments.
    - CORE
      - IoC Container, Events, Resources, i18n, Validation, Data Binding, Type Conversion, SpEL, AOP.
    - Runtime（框架组成模块）
    ![20220314091016](http://r8m8y4rji.hn-bkt.clouddn.com/img/20220314091016.png)
- 广义Spring：Spring生态体系
  - [spring官网](spring.io)
  - What Spring can do？
  - Projects
    - Spring Boot、Spring Framwork…

#### 传统开发方式

- 对象直接引用导致对象硬性关联，程序难以扩展维护
- ![image-20220313104606401](http://r8m8y4rji.hn-bkt.clouddn.com/img/202203131046611.png)

#### Spring IoC容器

- IoC容器是Spring生态的地基，用于统一创建与管理对象依赖

- ![image-20220313104731425](http://r8m8y4rji.hn-bkt.clouddn.com/img/202203131047472.png)

- 通过A的依赖（B对象）注入到A对象中 ，使用者通过容器获取，而不直接面向对象

#### Spring IoC容器职责

- 对象的控制权交由第三方统一管理（IoC控制反转）
- 利用Java反射技术实现运行时对象创建与关联（DI依赖注入）
- 基于配置提高应用程序的可维护性与扩展性

### 分析传统编码方式的不足

举例(代码见s01)

- 妈妈在早餐后给三个孩子分发餐后水果-
- 盘子里装有三个苹果：红富士/青苹果/金帅-
- 孩子们口味不同：莉莉喜欢甜的/安迪喜欢酸的/露娜喜欢软的

缺陷

- 在编译中已经把对象和对象之间建立了强绑定，如需修改得修改源码

Spring IoC 解释

- 通过配置的方式，在不需要new的情况下对对象进行创建

  - 创建的规则按照xml中书写的过程来书写的过程进行的

  - 对于每一个创建的对象都放到IoC容器中，由IoC统一管理，并贴上相应的标签，标签称之为Bean id
  - 直观好处是，把原本的代码变为可配置的文本
  - 利用IoC容器让对象与对象之间有效解耦，原始代码通过new固定写死不便，利用IoC后可动态调整

## Spring XML配置——管理对象（Bean）
### 三种配置方法
  - 基于XML配置Bean实例化对象
  - 基于注解配置Bean实例化对象
  - 基于Java代码配置Bean实例化对象

  ```java
  //spring的XML配置文件 apllicationContext.xml
  // beanId是标签，当后面指定类被IoC容器实例化后，在容器中唯一编号的标签
  <bean id="sweetApple" class="com.imooc.spring.ioc.entity.Apple">
        <property name="title" value="红富士"></property>
        <property name="origin" value="欧洲"></property>
        <property name="color" value="红色"></property>
    </bean>
  
  //XML方式创建IoC容器
  //创建IoC容器并根据配置文件创建对象
  //标准代码 ClassPathXmlApplicationContext：加载指定的xml文件初始化IoC容器
        ApplicationContext context = new ClassPathXmlApplicationContext("classpath:applicationContext.xml");
  ```

## 对象实例化配置  
### 实例化Bean的三种方法
  - 基于构造方法对象化（90%）
    - 默认构造方法
    - 带参构造方法
  - 基于静态工厂实例化
  - 基于工厂实例方法实例化

  ```java
  <!-- applicationContext -->
  <!-- 实例化方法 基于构造方法对象化 参数名/参数位置-->
  <!-- 利用构造方法参数名实例化 实际更推荐-->
  <bean id="sweetApple" class="com.imooc.spring.ioc.entity.Apple">
        <!-- 没有constructor-arg则代表调用默认构造方法实例化 -->
        <property name="title" value="红富士"></property>
        <property name="origin" value="欧洲"></property>
        <property name="color" value="红色"></property>
    </bean>
  
  <!-- 利用构造方法参数位置实例化 尽量避免-->
  <bean id="sweetApple" class="com.imooc.spring.ioc.entity.Apple">
        <!-- constructor-arg 利用构造方法参数位置实例化 -->
        <constructor-arg index="0" value="红富士"/>
        <constructor-arg index="1" value="红色"/>
        <constructor-arg index="2" value="欧洲"/>
    </bean>
  
  <!-- 构造方法 默认构造/带参构造-->
    
  <!--bean标签默认通过默认构造方法创建对象-->
  <bean id="apple1" class="com.imooc.spring.ioc.entity.Apple">
  
  </bean>
  <!--使用带参构造constructor-arg方法实例化对象，使用name进行动态设置-->
  <bean id="apple2" class="com.imooc.spring.ioc.entity.Apple">
        <constructor-arg name="title" value="红富士"/>
        <constructor-arg name="color" value="红色"/>
        <constructor-arg name="origin" value="欧洲"/>
        <constructor-arg name="price" value="19.8"/>
    </bean>
  
  <!--使用带参构造constructor-arg方法实例化对象，使用用索引位置进行设置（尽量避免）-->
  <bean id="apple3" class="com.imooc.spring.ioc.entity.Apple">
      <constructor-arg index="0" value="红富士"/>
      <constructor-arg index="1" value="红色"/>
      <constructor-arg index="2" value="欧洲"/>
      <constructor-arg index="3" value="19.8"/>
  </bean>
  ```

  两种工厂本质一样，都是通过封装对应的方法，隐藏创建对象的细节
  最大的不同是 是否在创建对象方法上加static

    ```java
          /**
    * 静态工厂通过静态方法创建对象，隐藏创建对象的细节
    优点：可以将当前方法执行日志打印输出 logger.info("")
    */
    public class AppleStaticFactory {
        public static Apple createSweetApple(){
            //logger.info("")
            Apple apple = new Apple();
            apple.setTitle("红富士");
            apple.setOrigin("欧洲");
            apple.setColor("红色");
            return apple;
        }
    }
    ```

    <!--利用静态工厂获取对象-->
    <bean id="apple4" class="com.imooc.spring.ioc.factory.AppleStaticFactory"
          factory-method="createSweetApple"/>
    
    /*
    * 工厂实例方法创建对象是指IoC容器对工厂类进行实例化并调用对应的实例方法创建对象的过程
    * */
    public class AppleFactoryInstance {
        public Apple createSweetApple(){
            //logger.info("将当前方法日志打印输出")
            Apple apple = new Apple();
            apple.setTitle("红富士");
            apple.setOrigin("欧洲");
            apple.setColor("红色");
            return apple;
        }
    
    }
    
    <!--利用工厂实例方法获取对象-->
    <!--在IoC容器初始化过程中，首先对工厂进行实例化-->
    <bean id="factoryInstance" class="com.imooc.spring.ioc.factory.AppleFactoryInstance"/>
    <!--利用工厂的createSweetApple方法获取对象，这里配置项变成了factory-bean，
    factory-bean将工厂实例放入，同时仍然使用factory-method指向createSweetApple-->
    <bean id="apple5" factory-bean="factoryInstance" factory-method="createSweetApple"/>
    
    ```

### 从IoC容器获取bean
    ```java
    //方法一(建议)：sweetApple就是个标签，Apple.class是其类型
    Apple sweetApple = context.getBean("sweetApple",Apple.class);
    //方法二：强制转换
    Apple sweetApple = (Apple)context.getBean("sweetApple");
    ```

- id和name属性相同点
  - bean id与name都是设置对象在IoC容器中唯一标识
  - 两者在同一个配置文件中斗不允许出现重复
  - 两者允许在多个配置文件中出现重复，新对象覆盖旧对象
- id与name区别
  - id要求更为严格，一次只能定义一个对象标识（推荐）
  - name更为宽松，一次允许定义多个对象标识
  - tips：id与name的命名要求有意义，按驼峰命名书写
- 没有id和name的情况下，bean默认使用类名全称作为bean标识 

  ```java
    <!-- applicationContext1 -->
    <bean id="apple2" class="com.imooc.spring.ioc.entity.Apple">
    <!--name可以设置多个标识，而id只能设置一个，绝大多数只用一个情况，优先用id-->
    <bean name="apple2,apple7" class="com.imooc.spring.ioc.entity.Apple">
  
    <!-- SpringApplication -->
    Apple apple2 = context.getBean("apple2",Apple.class);
    System.out.println(apple2.getTitle());
    Apple apple7 = context.getBean("apple7",Apple.class);
    System.out.println(apple2.getTitle());
    
    <!-- 没有id和name的情况下，bean默认使用类名全称作为bean标识(比较少见)  -->
    <!-- applicationContext1 -->
    <bean class="com.imooc.spring.ioc.entity.Apple">
        <constructor-arg name="title" value="红富士3号"/>
        <constructor-arg name="color" value="红色"/>
        <constructor-arg name="origin" value="欧洲"/>
        <constructor-arg name="price" value="29.8"/>
    </bean>
  
    <!-- SpringApplication -->
    Apple apple = context.getBean("com.imooc.spring.ioc.entity.Apple",Apple.class);
    System.out.println(apple.getTitle());
  ```

  ## 依赖注入配置
  ## 注解与Java Config
  ## Spring 单元测试