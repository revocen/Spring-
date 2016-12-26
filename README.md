# Spring Framework 翻译试水
##翻译内容基于Spring Framework 4.3.4.RELEASE

##第一部分 Spring Framework 概览
  Spring Framework是一个轻量级的，一站式的用于创建企业级应用的解决方案。并且Spring是模块化的，你可以只使用你需要的模块，并非必须全部引用。你可以把任何web framework放在IOC容器之上，也可以只使用hibernate集成或JDBC抽象层这样的代码。Spring Framework支持声明式的事务管理，通过RMI(即Remote Method Invoke 远程方法调用)或web service来访问你的业务逻辑，并提供了几种方式用于保存数据。Spring Framework提供了一个全功能的MVC框架，这样就可以将AOP显示的集成在你的代码中。

  Spring是非侵入式，这就意味着在你的业务代码中通常并不依赖于framework本身。在你的封装层（比如数据访问层），在数据访问技术上一些dependencies和Spring libraries 还是存在的，但这些dependencies可以很容易的与你的基础代码分离。

###   1. Spring 起步
  本文提供了Spring Framework 所有特性的说明文档，也包含了一些诸如“依赖注入”之类的习惯性说法。

  如果你是刚开始使用Spring，你也许可以通过创建一个Spring Boot的基础应用来使用Spring。Spring Boot提供了一个快捷简便的方式来创建可以用于生产环境的Spring 基本应用。它基于Spring Framework，遵循习惯优于配置，并设计成让你能更快的运行起来。

  你可以通过spring.io指导来集成一个基本的工程或采用像“构建RESTful Web Service起步”的方式。这样的方式更加容易理解，同时这些指导内容都非常注重功能本身，他们大部分都是以Spring Boot为基础构建的。这些指导内容同样包含了一些其他的Spring项目，这样当你要解决一个特殊问题的时候就可以考虑这些项目。
### 2. Spring Framework介绍

  Spring Framework 是一个java框架，用来为开发java应用提供多方面的底层支持。Spring负责处理底层问题，让你可以专注于业务本身的逻辑。

  Spring允许通过POJO（简单的java对象）来构建应用，并对其应用非侵入式的企业服务。该功能用于标准的java程序模型，以及整体或部分的JavaEE。

  作为一个应用程序的开发者，你可以通过Spring框架得到如下便利：

 - 掉用Java方法用于数据库事务时，不需要非得通过事务API来解决；
 - 使一个本地的Java方法变为一个远程的程序，而无需处理远程API;
 - 使一个本地的Java方法变为一个管理操作，而无需处理JMX API;
 - 是一个本地的Java方法变为一个消息处理器，而无需处理JMS APS;

#### 2.1. 依赖注入和控制反转
一个java应用：不太标准的说法是一个运行范围从嵌入式程序到N层的大型服务器端企业级的应用程序，通常由很多对象协调来构成一个完整的应用程序。应用程序中的这些对象彼此依赖。

尽管Java平台提供了非常丰富的应用开发功能，但对一个整体而言，缺乏基础构建模块的整合，把这些工作留给了架构师和开发者。尽管你可以使用一些设计模式，比如工厂模式、抽象工厂、生成器模式、装饰模式以及服务定位模式等将不多的类和对象实例来组合成一个应用程序。这些模式都很简单：最佳的命名方式，模式用途的描述、在哪使用、问题的标记等等。模式以最佳的方式被形式化，这就意味着你必须的在你的应用中自己实现这些模式。

Spring Framework的IOC组件针对这一问题，通过在完整的工作应用中使用不同的组件构成的方法来解决该问题。同时将形式化的设计模式编码成可以整合到你自己的应用中的高级对象。许多组织机构使用Spring Framework的这种方法来构建稳定，可维护的应用程序。
  

背景

  2004年Martin Fowler在他的个人网站上提出了一个关于IOC的问题--“到底是哪方面被反转了”。他建议重新命名这个概念的名称（IOC），使其更加一目了然，随后Fowler给他起了一个名字“Dependency Injection”（DI,依赖注入）。

#### 2.2. 模块化

Spring Framework 由很多特性组成，并放到了20个模块中。这些模块被组合进核心容器、数据访问/集成、Web、AOP(面向切面编程)、设备、消息以及测试，如下图所示。

##### 图 2.1 Spring Framework概览

  ![Spring Framework概览](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/xspring-overview.png.pagespeed.ic.r3l2HohxPQ.webp)

  下面列出了各个特性可供使用的模块以及各模块的artifact名称。Artifact名称在依赖管理工具中与artifact id相关联。

##### 2.2.1 核心容器

  核心容器包括几个模块：spring-core,spring-beans,spring-context,spring-context-support以及spring-expression(Spring表达式语言)。

  spring-core和spring-beans模块提供了框架中一些基础的部分，包括IOC和DI功能。BeanFactory是工厂模式的一个更高级的实现。它去除了程序对单例模式的需要，并且允许你解耦配置，然后根据你实际的编码逻辑设置依赖关系。

  Context(spring-context)模块以Core和Beans模块为基础构建：他是一个类似于JNDI注册表式的框架风格的访问对象的方式。Context模块继承了Beans模块的功能，并增加了对国际化的（比如 resource bundles的使用）,事件传播，资源加载，以及Context的透明创造，例如一个Servlet容器。Context模块同样支持像EJB,JMX或基本的远程处理的支持。ApplicationContext接口是Context模块的核心。spring-context-support为Spring应用上下文整合了通用的三方库，比如缓存（EhCache,Guava,JCache）,邮件（JavaMail）,定时任务（CommonJ,Quartz），以及末班引擎（FreeMarker,JasperReports,Velocity）。

  spring-expression模块为runtime时的查询和操作对象图提供了一个强大的EL语言，在JSP 2.1规范中，它作为统一表达式语言规范的一个扩展。该表达式语言支持属性值的setting和gettting，属性分配，方法调用，访问数组，集合，索引器的内容，逻辑和算术运算，变量命名，在IOC中根据名称查找对象。同时也支持列表投影，选择以及通用列表的聚合。

##### 2.2.2. AOP和工具

  spring-aop模块提供了AOP联盟标准的一个面向切面编程的实现，允许你自定义拦截器和切点来干净的解耦应该被分离的代码。使用源码级的元数据功能，同样可以将行为信息放到你的代码中，类似于.NET的属性值。

  独立的spring-aspects模块提供了对AspectJ的整合。

  spring-instrument模块提供了类工具的支持和类加载器的实现，用于某些应用服务中。spring-instrument-tomcat模块包括了Spring对tomcat的代理工具。

##### 2.2.3. 消息

  Spring Framework 4包括了一个spring-messaging模块，这是对Spring集成项目中的像消息，消息通道，消息处理器进行了关键性的抽象。该模块也提供了类似于编程模式spring MVC注解的一系列为方法映射消息的注解。

##### 2.2.4 数据访问/集成

数据访问/集成层包括JDBC、ORM、OXM、JMS以及事物模块。

spring-jdbc模块提供了一个jdbc的抽象层，移除了乏味的JDBC代码，以及对数据库厂商特殊错误代码的转换。

spring-tx模块为实现特殊接口的类提供了编程示和声明式的事物管理，并且可以用于所有的POJO。

spring-orm模块为流行的对象-关系映射API（包括JPA,JDO,hibernate）提供了整合层。使用spring-orm模块你可以将所有这些O/R映射的框架与Spring提供的其他特性整合到一块，比如前面提到的事物管理功能。

spring-oxm模块提供了一个O/X映射的实现，比如JAXB，Castor,XMLBeans,JiBX,XStream的抽象层。

spring-jms模块（java消息服务）包括生产和处理消息的功能。从Spring Framework 4.1开始，使用spring-messaging模块提供了集成。

##### 2.2.5 Web

Web层包括了spring-web,spring-webmvc,spring-websocket以及spring-webmvc-portlet几个模块。

spring-web模块提供了基础的面向web的集成功能，例如文件上传功能，以及通过servlet监听器和一个面向web的应用上下文初始化IOC容器。也包括了一个HTTP客户端和Spring提供的远程支持部分中网络相关的内容。

spring-webmvc模块（也叫web-servlet模块）模块，包括为web应用实现的Spring的模型-视图-控制器（MVC）和REST Web Service。

Spring MVC在domain代码，web表单之间提供了一个干净的隔离，并且和所有Spring Framework的其他功能进行了集成。

spring-webmvc-portlet模块（也叫Web门户组件模块）提供了MVC的实现，用于门户组件环境中，体现了spring-mvc模块的功能。

##### 2.2.6 测试

spring-test模块通过JUnit或TestNG提供了unit测试和集成测试。提供了Spring ApplicationContext和这些context的缓存的一致的加载方式。也提供了模拟对象，这样你就可以在隔离的情况下测试你的代码了。

#### 2.3 使用场景

前面说的构建模块通过使用Spring的事物管理功能和web框架整合让Spring在很多场景中都有一个适合的选择，不论是运行在资源受限的设备的嵌入式应用还是成熟的企业级的应用。

##### 图2.2 典型的成熟Spring Web Application

![Spring Web Application](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-full.png.pagespeed.ce.sC26wirtWB.png)

Spring声明式事物管理功能让web应用布满事物，就像你使用EJB的容器管理事物的样子。你所有自定义的业务逻辑代码都可以通过简单的POJO来实现，并通过Spring的IOC事物管理来管理。其他的服务包括对发邮件的支持，校验（依赖于web层，这样可以让来选择在哪执行校验规则），和JPA、hibernate、JDO集成了的Spring ORM；比如，当用到hibernate，你可以继续使用你已经在的映射文件和标准的hibernate SessionFactory配置。表单控制器通过业务模型与web层无缝集成，并移除了对ActionForm或其他的类（用于将HTTP的参数转换为你的业务模型）的需要。

#####  图 2.3 使用一个第三方web framework的Spring中间层

![Figure 2.3](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-thirdparty-web.png.pagespeed.ce.1lJso2G8WP.png)

有时候并不允许你完全的去选择一个不同的框架。Spring Framework不会强迫你使用它的所有功能，她不是一个“除非全用否则全不用”的方案。目前像Struts,Tapestry,JSF或其他前端UI框架都可以通过一个Spring的基础中间层来集成，这样你就可以使用Spring的事物功能了。你需要使用一个ApplicationContexthe和一个WebApplicatinContext来简单的把你的业务逻辑集成到你的web层。

##### 图 2.4. 远程处理使用环境

![Figure 2.4](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-remoting.png.pagespeed.ce.HIMsJb_Xya.png)

当你需要通过web service来访问已经存在代码，你可以使用Spring的Hessian-,Burlap-,Rmi-或JaxRpcProxyFactory的类。可以无区别的访问存在的应用。

##### 图 2.5. EJB 包装已有的POJO

![Figure 2.5](http://docs.spring.io/spring/docs/current/spring-framework-reference/htmlsingle/images/overview-ejb.png.pagespeed.ce.VN88UiKUhA.png)

Spring Framework 同样为企业级JavaBean提供了一个访问和抽象层，可以使你能复用你已有的POJO，并把他们包装在无状态的session bean中以用在可扩展性，以及需要声明安全的不安全的web应用中。

##### 2.3.1 依赖管理和命名规范

依赖管理和依赖注入是两个不同的东西。为了将Spring那些nice的功能用在你的应用中（比如依赖注入），你需要将所有需要的类库（jar包）集中，并将他们放在你的运行时（也可能在编译时）的classpath中，这些依赖并不是被注入的虚拟组件，而是在文件系统中（通常来说）的真实的资源。以来管理的过程涉及加载那些资源，并存储，然后加到classpath
中。可以是直接依赖（比如我的应用在运行时直接依赖于Spring）或者间接依赖（比如我的应用直接依赖于commons-dbcp，而commons-dbcp直接依赖于commons-pool）。间接依赖也叫“依赖传递”，他是那些特别不容易定义和管理的依赖。

如果你将使用Spring，你需要复制一份你需要用到的Spring的部分的jar包。为了让这件事更容易，Spring被打包成很一系列的模块，尽可能的隔离依赖关系，比如如果你不想写一个web应用，你就不需要spring-web相关的模块。本文中的Spring模块，我们使用一个简短的命名方式spring-* 或spring-\*.jar, \*代表模块的简称（比如spring-core,spring-webmvc,spring-jms等等）实际上你用的jar文件命名一般是模块名加版本号（比如spring-core-4.3.5.RELEASE.jar）。

Spring Framework 每个发行版都会将artifact放到下面地方：

- Maven中央仓库，Maven查找的默认的仓库，并且使用时不要求任何特殊的配置。许多Spring依赖的一般库也可以从Maven中央库中获得，很多Spring社区都是用maven作为依赖管理，对他们来说这很方便。这里的jar包的命名使用spring-\*-< version >.jar的形式，maven的groupid是org.springframework。

- 把Spring托管在一个具体的公共Maven库中。除了最终的GA版（General Availability，最终版），该库中也有开发版的快照和里程碑。jar包的命名与Maven中央库的命名形式相同，因此这是一个很有用的地方，来获取Spring的开发版本，并与部署在Maven中央库的其他类库一块使用。该仓库也包括了一些分发的Zip文件，包括了Spring所有的jar包，以方便下载。

因此，你首先要想的是怎么管理依赖：我们一般推荐使用自动化系统，比如Maven，Gradle或者lvy，当然你也可以手动下载所有的jar包。

下面是Spring artifact的列表，想了解各个模块的具体信息，可以看第2.2章 “模块”。

##### 2.1 Spring Framework Artifacts

| GroupId            | ArtifactId    | Description           |
|:------------------:|:--------------|:----------------------|
|org.springframework | spring-aop    | 基于代理的AOP支持|
|org.springframework | spring-aspects    | 基于AspectJ的aspect|
|org.springframework | spring-beans    | Bean支持，包括Groovy|
|org.springframework | spring-context    | 应用上下文运行时，包括调度和远程的抽象|
|org.springframework | spring-context-support    | 用于支持将第三方库整合进Spring应用上下文的支持类|
|org.springframework | spring-core    | 核心工具，许多其他Spring模块都有用到|
|org.springframework | spring-expression    | Spring表达式语言|
|org.springframework | spring-instrument    | 为JVM引导启动用的代理工具|
|org.springframework | spring-instrument-tomcat    | tomcat的代理工具|
|org.springframework | spring-jdbc    | jdbc支持包，包括数据库加载和jdbc访问支持|
|org.springframework | spring-jms    | JMS支持包，包括收发JMS消息的帮助类|
|org.springframework | spring-messaging    | 提供消息架构和协议的支持|
|org.springframework | spring-orm    | 对象关系映射，包括JPA和hibernate的支持|
|org.springframework | spring-oxm    | 对象XML映射|
|org.springframework | spring-test    | 为单元测试提供支持，并整合Spring组件测试|
|org.springframework | spring-tx    | 事务基础组件，包括DAO支持和JCA集成|
|org.springframework | spring-web    | web支持包包括客户端和web远程|
|org.springframework | spring-webmvc    | 为web应用提供的REST Web Service和模型-视图-控制器的实现|
|org.springframework | spring-webmvc-portlet    | 用于Porlet环境的MVC实现|
|org.springframework | spring-websocket    | WebSocket和SockJS实现，包括STOMP的支持|

##### Spring依赖和在Spring中依赖

尽管Spring提供了集成，也对大量企业级和其他扩展工具提供了支持，但他有意的保持了对一个最小限度的抽象的强制性依赖：你不必去查找并下载（甚至是自动下载）大量的jar包类库，到最后只是为了一个很简单的原因使用Spring。对于基础的依赖注入，只有一个强制性的外部依赖，而且他还是为了记录日志（看下面，可以获取更多的有关日志的描述）。

下一步，我们脱离基础的步骤，需要在Spring上配置应用的依赖。首先使用Maven，然后使用Gradle，最后使用lvy。如果有什么不清楚的，可以看看你使用的依赖工具的文档，或者看看一些简单的代码-Spring本身使用Gradle作为依赖管理工具来构建，并且我们的示例代码大都使用Gradle或者Maven。

##### Maven依赖管理

如果你使用Maven作为依赖工具，你甚至不需要直接的获取日志依赖。比如创建一个应用上下文，并且使用依赖注入来配置一个应用，你的Maven依赖将会是这样：

    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>4.3.5.RELEASE</version>
            <scope>runtime</scope>
       </dependency>
    </dependencies>

这样就可以了。需要说明的是“scope”，如果不需要使用Spring的API来编译代码，可以声明成runtime，在基础的依赖注入使用案例中，这算是一个典型的例子了。

上面是使用Maven中央库的例子。要是使用Spring Maven库的话（比如里程碑或者开发者快照），你需要在你的Maven配置中配置仓库的位置。获取全部发行版：

    <repositories>
        <repository>
            <id>io.spring.repo.maven.release</id>
            <url>http://repo.spring.io/release/</url>
            <snapshots><enabled>false</enabled></snapshots>
        </repository>
    </repositories>

获取里程碑：

    <repositories>
      <repository>
        <id>io.spring.repo.maven.milestone</id>
          <url>http://repo.spring.io/milestone/</url>
        <snapshots><enabled>false</enabled></snapshots>
      </repository>
    </repositories>

获取快照：

    <repositories>
      <repository>
          <id>io.spring.repo.maven.snapshot</id>
          <url>http://repo.spring.io/snapshot/</url>
          <snapshots><enabled>true</enabled></snapshots>
      </repository>
    </repositories>

##### Maven“材料清单”依赖

使用Maven的时候，可能会意外的将各版本Spring的jar包混合使用。比如，你可能从一个第三方库或另一个Spring项目中找到jar包，，然后在一个老版本中把他拉进一个传递依赖中。如果你忘了明确的声明一个直接依赖，那么各种各样的问题将会接憧而至。

为了解决这类问题，Maven支持一个“材料清单”（BOM）依赖的概念
。你可以在你的依赖管理中引入springframework-bom来确保所有的spring依赖（不论直接还是间接依赖）都是相同的版本。

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-framework-bom</artifactId>
                <version>4.3.5.RELEASE</version>
                <type>pom</type>
                <scope>import</scope>
           </dependency>
        </dependencies>
    </dependencyManagement>

使用BOM的另一个好处是你不再需要在依赖中为Spring Framework配置 < version >属性了。

##### Gradle依赖管理

通过Gradle构建工具来使用Spring仓库，在仓库部分加入适当的URL：

    repositories {
        mavenCentral()
        // and optionally...
        maven { url "http://repo.spring.io/release" }
    }

你可以更换仓库URL，/release，/milestone，或者/snapshot都可以。一旦仓库配置完，你就可以使用通常的Gradle方法来声明依赖。

    dependencies {
        compile("org.springframework:spring-context:4.3.5.RELEASE")
        testCompile("org.springframework:spring-test:4.3.5.RELEASE")
    }
