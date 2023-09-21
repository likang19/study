---

---



spring 生命周期
spring 重要周期扩展点
spring 最常用扩展点
spring 如果自定义扩展点 BeanPostProcessor

参考地址：https://cloud.tencent.com/developer/article/2291844



### 一、Spring高手之路1——深入理解与实现IOC依赖查找与依赖注入

~~~
IOC控制反转和依赖查找，在spring framework是一种设计模式，解决模块之间的解耦关系，注意集中在业务上，而不是业务上
依赖查找是一种技术手段，使我们对象可以成为一个管理的容器。
两种实现方式：
 1.依赖查找（配置xml与类型依赖查找是一种主种依赖方式，需要显示的调用api）
 2.依赖注入 (被动依赖，基于setter的依赖注入)

~~~



### 二、Spring高手之路2——深入理解注解驱动配置与XML配置的融合与区别

~~~
1.配置类的编写与Bean的注册
  通过编码与xml都可以编写Bean 
2.注解驱动IOC的依赖与xml依赖对比
  一个是xml配置里面加一种是通过依赖注入进行写
3.spring中的组件概念
	@ComponentScan 扫描并注册的"组件" 扫描后的都会被注入到spring的容器里面
4.组件注册
	@Configuration 就表示被注册了组件
5.组件扫描
 	5.1 使用@ComponentScan的组件扫描
 	5.2 xml中启用component-scan组件扫描
 	5.3 不使用@ComponentScan的组件扫描 AnnotationConfigApplicationContext指定类读取 	
6.组件注册其它注解
	@Controller, @Service, @Repository和@Component
7.将注解驱动的配置与XML驱动的配置结合使用
	xml与注解一起使用
思考1问：为什么我们需要组件，这与Bean有什么关系
  Bean 对象是spring IOC 管理的， 常用与数据管理对象，业务逻辑组件，dao层对象
  组件注册：spring 通过扫描后标识的类，告诉spring框架这是一个组件，spring 需要创建它的实例并管理它的生命周期，这样当使用的时候就可以在你需要的时注入。
 思考2问：什么是组件扫描，为什么我们需要它，它是如何工作的？
 组件扫描是自动的，自动注册到spring 上下文中  
~~~

### 三、Spring依赖注入和SpEL表达式

~~~
1.setter属性注入
  使用xml与@Bean 注入实体
2.构造器注入
  注入是一种在对象被实例化之后（通过调用无参构造器创建实例）
  XML进行构造器注入。指定序列号注入@Bean注入
3.注解式属性注入
  @Value
  引入外部配置文件@PropertySource
  在XML中引入外部配置文件
4.SpEL表达式属性	
~~~

### 四、解析Spring内置作用域及其在实践中的应用

~~~
1.Spring的内置作用域 5.x版本中 6种
	singleton：在IOC容器中，对应的Bean只有一个实例，所有对它的引用都指向同一个对象。这种作用域非常适合对于无状态的Bean，比如工具类或服务类。
	prototype：每次请求都会创建一个新的Bean实例，适合对于需要维护状态的Bean。
	request：在Web应用中，为每个HTTP请求创建一个Bean实例。适合在一个请求中需要维护状态的场景，如跟踪用户行为信息。
	session：在Web应用中，为每个HTTP会话创建一个Bean实例。适合需要在多个请求之间维护状态的场景，如用户会话。
	application：在整个Web应用期间，创建一个Bean实例。适合存储全局的配置数据等。
	websocket：在每个WebSocket会话中创建一个Bean实例。适合WebSocket通信场景
2.
	
~~~

### 五、spring 生命周期

~~~
大致如下：
	1.实例化： spring 启动时，会在配置上声明每个Bean 并创建实例
	2.属性赋值：通过反射机制给每个属性赋值
	3.调用初始化方法：Bean配置了初始化方法，初始化方法在赋值后处理业务逻辑
	4.Bean运行周期：Bean已经准备好被程序使用了
	5.应用程序关闭：当IOC关闭容器时
	6.调用销毁方法： Bean配置了销毁方法时
@PostConstruct和@PreDestroy
Spring中控制Bean生命周期的三种方式总结
~~~

![b822564e06a4cad648ce8d3bb8bf093f](.\images\b822564e06a4cad648ce8d3bb8bf093f.png)



### 六、Bean生命周期的扩展点：BeanPostProcessor

~~~
BeanPostProcessor 后置处理器,设计目标是为开为人员提供的一种扩展机制，可以在spring初始化的时候自定义操作，spring 的一种重要原则（开闭原则）开闭原则强调（类，模板，函数等）应该对扩展开发放性的，让开发者不侯源码情况下，实现对Bean的自定义操作
1.BeanPostProcessor的文档说明
	postProcessBeforeInitialization：会在Bean的属性已设置完毕，但还未进行初始化的时候进行调用
	postProcessAfterInitialization：bean的属性值已经被填充完毕。返回的bean实例可能是原始bean的一个包装
2.利用BeanPostProcessor修改Bean的初始化结果的返回值
  通过BeanPostProcessor实现Bean属性的动态修改
  当返回值为null ，对原属性对象没有任何变化，
3.Bean生命周期与后置处理器的交互时序
	
~~~

![](/Bean生命周期与后置处理器交互时序.png)

### 七、事件机制与监听器的全面探索

~~~
1.spring 中的观察者模式
  观察者模式是一种设计模式，它定义对象之间的依赖关系，所有依赖它的对象都会被通知到并自动更新，在这个模式中，改变状态的对象被叫主题，依赖它的对象被叫观察者
  事件源（Event source），事件(Event),广播器（Event publisher/Multicaster），观察者(listener))
2.监听器
  
3.spring的事件机制
  ApplicationEvent
  ApplicationContextEvent
  ContextRefreshedEvent 和 ContextClosedEvent
  ContextStartedEvent 和 ContextStoppedEvent
~~~

### 八、Spring Bean模块装配的艺术 @Import详解

~~~
1.spring 手动装配
  new 一个对象，或者xml中配置bean spring2.0后支持注解
2.Spring 框架中的模块装配
	就是将类或者组件注册到spring ioc里面
3.@Import模块装配的四种方式
	导入普通类与自定义注解的使用
		@Retention(RetentionPolicy.RUNTIME)
        @Target(ElementType.TYPE)
        @Documented
        @Import({Librarian.class, Book.class, BookShelf.class})
        public @interface ImportLibrary {
        }
	导入配置类的策略
	使用ImportSelector进行选择性装配
	使用ImportBeanDefinitionRegistrar进行动态装配	 
~~~

### 九。spring 条件装配

~~~
条件装配，是允许开发者根据自己条件，动态的进行装配Beam注册与创建
常用注解：
	@Profile 这个注解表示特点的情况下才会被激活，
	@Conditional 它接受一个或多个Condition类
Spring Boot
	@ConditionalOnProperty 这个注解表示只有当一个或多个给定的属性有特定的值时，才创建带有该注解的
	@ConditionalOnClass 和 @ConditionalOnMissingClass： 这两个注解表示只有当Classpath中有（或没有）特定的类时，才创建带有该注解的Bean
	@ConditionalOnBean 和 @ConditionalOnMissingBean：这两个注解表示只有当Spring ApplicationContext中有（或没有）特定的Bean时，才创建带有该注解的Bean
	
	@ConditionalOnProperty 检查某个属性配置存在，在注册Bean
	@ConditionalOnProperty(name = "my.feature.enabled", havingValue = "true", matchIfMissing = true)
~~~

### 十、spring 组件扫描
~~~test
1.组件扫描路径
2.按注解过滤组件（包含）
3.按注解过滤组件（排除）
4. 通过正则表达式过滤组件
5. Assignable类型过滤组件
6. 自定义组件过滤器
7. 组件扫描的其他特性
8. 组件扫描的组件名称生成
~~~

### 十一、BeanDefinition解密：构建和管理Spring Beans的基石

~~~
BeanDefinition包含了大量的配置信息，这些信息可以指导Spring如何创建Bean，包括Bean的构造函数参数，属性值，初始化方法，静态工厂方法名称等等
存储了关于如何创建、初始化、配置一个具体的Bean实例的详细信息
完全限定的类名，以便Spring容器通过反射创建Bean实例。
Bean的名称和别名，用于在应用中引用和查找Bean。
Bean的作用域，如单例或原型，决定了Spring如何管理Bean实例的生命周期。
构造函数参数和属性值，用于实例化Bean和依赖注入。
自动装配模式，指示Spring如何自动注入依赖。
初始化和销毁方法，让Spring知道在Bean生命周期的特定时刻如何执行自定义逻辑。
Bean的依赖关系，告诉Spring在创建当前Bean之前需要先创建哪些Bean
~~~

### 十二、BeanDefinitionRegistry与BeanDefinition合并解析

~~~
BeanDefinitionRegistry：是Spring 中注册和管理 BeanDefinition 的核心组件，它的主要职责就是注册和管理这些， BeanDefinition看存放注册表，检索和删除现有的 BeanDefinition
在spring 的内部，BeanDefinittionRegistry 通常由 BeanFactory 实现
1.为什么需要BeanDefinitionRegistry
	资源解析的统一性
	依赖查找和注入
	延迟初始化和作用域管理
	配置验证
	生命周期管理
2.BeanDefinitionRegistry 的使用
	BeanDefinition合并的目的
		提供完整的BeanDefinition信息
		优化性能
~~~

#####十三、BeanFactoryPostProcessor与BeanDefinitionRegistryPostProcessor解析

~~~
1.解读 BeanFactoryPostProcessor
  BeanFactoryPostProcessor的主要目的是对Bean的配置元数据进行操作，这意味着它可以影响Bean的初始配置数据。BeanFactoryPostProcessor 与 BeanPostProcessor 的差异
 BeanFactoryPostProcessor 和 BeanPostProcessor 都是 Spring 框架中为了增强容器的处理能力而提供的扩展点。它们都可以对 Bean 进行定制化处理，但它们的关注点和应用时机不同。

BeanFactoryPostProcessor:
功能: 允许我们在 Spring 容器实例化任何 bean 之前读取 bean 的定义(bean 的元数据)并进行修改。
作用时机: 它会在 BeanFactory 的标准初始化之后被调用，此时，所有的 bean 定义已经被加载到容器中，但还没有实例化任何 bean。此时我们可以添加、修改或移除某些 bean 的定义。
常见应用: 动态修改 bean 的属性、改变 bean 的作用域、动态注册新的 bean 等。
示例接口方法：void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException;
BeanPostProcessor:
功能: 允许我们在 Spring 容器实例化 bean 之后对 bean 进行处理，提供了一种机会在 bean 的初始化前后插入我们的自定义逻辑。
作用时机: 它在 bean 的生命周期中的两个时间点被调用，即在自定义初始化方法(如 @PostConstruct, init-method)之前和之后。
常见应用: 对特定的 bean 实例进行一些额外处理，如进行某种代理、修改 bean 的状态等。
示例接口方法：Object postProcessBeforeInitialization(Object bean, String beanName) throws BeansException; 和 Object postProcessAfterInitialization(Object bean, String beanName) throws BeansException;
总结:

BeanFactoryPostProcessor 主要关注于整个容器的配置，允许我们修改 bean 的定义或元数据。它是容器级别的。
BeanPostProcessor 主要关注于 bean 的实例，允许我们在初始化前后对 bean 实例进行操作。它是 bean 级别的。
4.2. BeanFactoryPostProcessor 与 BeanDefinitionRegistryPostProcessor 的关系
 BeanFactoryPostProcessor 和 BeanDefinitionRegistryPostProcessor 都是 Spring 中提供的两个重要的扩展点，它们都允许我们在 Spring 容器启动过程中对 Bean 的定义进行定制处理。但它们的应用时机和功能上存在一些不同。

BeanFactoryPostProcessor:
功能: 允许我们在 Spring 容器实例化任何 bean 之前读取 bean 的定义 (BeanDefinition) 并进行修改。
作用时机: 在所有的 bean 定义都被加载、但 bean 实例还未创建的时候执行。
常见应用: 修改已加载到容器中的 bean 定义的属性，例如更改某个 bean 的作用域、属性值等。
主要方法: void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException;
BeanDefinitionRegistryPostProcessor:
功能: 扩展了 BeanFactoryPostProcessor，提供了一个新的方法来修改应用程序的上下文的 bean 定义。此外，还可以动态注册新的 bean 定义。
作用时机: 它也是在所有 bean 定义被加载后执行，但在 BeanFactoryPostProcessor 之前。
常见应用: 动态注册新的 bean 定义、修改或移除已有的 bean 定义。
主要方法: void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry registry) throws BeansException;
总结：

BeanFactoryPostProcessor 主要是用来修改已经定义的 bean 定义，而不是注册新的 bean。
BeanDefinitionRegistryPostProcessor 是 BeanFactoryPostProcessor 的扩展，并提供了额外的能力来动态地注册、修改、移除 bean 定义。
在 Spring 容器的启动过程中，首先执行的是 BeanDefinitionRegistryPostProcessor 的方法，之后才是 BeanFactoryPostProcessor 的方法。
~~~

### 十四、SPI机制在JDK与Spring Boot中的应用

~~~
什么是SPI?是一种服务发现机制，它允许第三方提供者为核心库或主框架提供实现或扩展。这种设计允许核心库/框架在不修改自身代码的情况下，通过第三方实现来增强功能
SPI在Spring框架中的应用
 1.Spring的SPI：Spring的核心框架提供了很多接口和抽象类，如BeanPostProcessor, PropertySource, ApplicationContextInitializer等，这些都可以看作是Spring的SPI
 2.Spring Boot的spring.factories机制
 spring.factories是Spring Boot的一个特性，允许开发者自定义自动配置。通过spring.factories文件，开发者可以定义自己的自动配置类，这些类在Spring Boot启动时会被自动加载。
 3.SPI在JDBC驱动加载中的应用
 4.如何通过Spring Boot自动配置理解SPI思想
 	这种机制有点类似于Java的SPI，因为它允许第三方库提供一些默认的配置。但它比Java的SPI更为强大和灵活SPI（Service Provider Interface）总结
 	SPI，即服务提供者接口，是一种特定的设计模式。它允许框架或核心库为第三方开发者提供一个预定义的接口，从而使他们能够为框架提供自定义的实现或扩展
 	核心目标:
解耦：SPI机制让框架的核心与其扩展部分保持解耦，使核心代码不依赖于具体的实现。
动态加载：系统能够通过特定的机制（如Java的ServiceLoader）动态地发现和加载所需的实现。
灵活性：框架用户可以根据自己的需求选择、更换或增加新的实现，而无需修改核心代码。可插拔：第三方提供的服务或实现可以轻松地添加到或从系统中移除，无需更改现有的代码结构。
~~~



