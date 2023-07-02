# Spring

>1. Spring里面有哪些设计模式   Spring默认是单例还是多例，讲讲单例模式
>2. Spring中bean的默认作用域，怎么改变作用域范围，Spring的几种事务说一遍
>3. 事件订阅的接口名字是什么?
>4. Spring 的后置处理器接口名字是什么?
>5. XML 的两种解析策略?两种有什么差异?
>6. Spring三级缓存机制
>7. 为什么很多[项目](https://www.nowcoder.com/jump/super-jump/word?word=项目)都选择Spring? Spring有啥特点？IoC底层是什么？如果让你去实现IoC会怎么实现
>8. Spring[项目]()启动的时候会加载哪些资源，顺序是怎么样的  
>9. spring配置线程池方式：自定义线程工厂bean需要实现ThreadFactory，可参考该接口的其它默认实现类，使用方式直接注入bean

>- IOC 的初始化流程?
>- AOP是怎么和 IOC 做整合的?
>- 循环依赖怎么解决?
>- SpringMVC 处理请求的一个流程?
>- Servlet 的监听器和拦截器?
>- 有哪些方法可以拦截一个 HTTP 请求?
>- 关于接受请求的参数,你有没有一套自己总结的方法?
>- 你对 IOC 的理解?
>- AOP 的各种实现有什么差异?
>- 为什么会有多种代理的方式?
>- 外挂的 Tomcat 和 SpringBoot 内嵌的 Tomcat 有什么区别?
>- Tomcat 的设计模式了解么?
>- SpringBoot 怎么调起Tomcat?
>- 实际开发当中你哪些地方使用了 Bean 的前置后置处理器?
>- Spring 怎么把 Java 对象初始化成 SpringBean 的?
>- IOC 的初始化流程?
>- 讲讲自动装配?
>- 我们自己也可以实现 IOC 和 AOP,甚至是前置后置处理器,为什么还要用 Spring 提供的?
>- 怎样才能知道 Spring 的 IOC 容器已经完全初始化了?
>- 事件订阅的接口名字是什么?
>- 为什么我会问这个问题?为什么我们需要知道 Spring IOC 容器的初始化进度?
>- Spring 的后置处理器接口名字是什么?
>- AOP 是怎么做动态代理的?
>- CGLIB 是怎么操作字节码的?
>- ASM 操作字节码的原理?
>- XML 的两种解析策略?两种有什么差异?
>- web开发 cookies 与 session
>- BeanFactory和FactoryBean的区别
>- Spring如何解决循环依赖
>- SpingIOC注入对象过程
>- Spring三级缓存机制
>- SpringBoot启动过程
>- Spring 两个方法，方法A加了Transactional注解，方法B没加，方法B中调用方法A，调用方法B是否会有事务。(没回答出来，但是让我从注解和反射的角度分析)
>- Cookie跨域问题（开始考错题）
>- Spring中autowired有啥用
>- 当一个注入接口有两个实现类时，自动注入会出现什么情况？
>- 当autowire一个list<A>会出现什么
>- Spring中的Bean的执行流程 (这个我不太了解，之后会了解)
>- SpringMVC是用来做什么功能的 （我是对比的没使用框架的[项目](https://www.nowcoder.com/jump/super-jump/word?word=项目)，进行的讲解）
>- 用过较多的注解
>- @autoweird注解在抽象类上生效吗
>- 为什么很多[项目](https://www.nowcoder.com/jump/super-jump/word?word=项目)都选择Spring?
>- 为什么在[项目]()中使用ioc?(这里我答了交给spring管理之后,可以通过干预Spring Bean的生命周期来达到一个可扩展 解耦合的地步,由于答了Spring管理bean的生命周期,所以有了31问的追问)
>- Spring的生命周期,(反正大概把[源码](https://www.nowcoder.com/jump/super-jump/word?word=源码)那一套东西说了一下,大概答了4分钟,由于提到了Spring在postBeforeInstiation提供了给bean aop的机会,所以有了32问的追问)
>- Spring自身有什么地方使用了aop么?这我答的是 [@Transactional](https://www.nowcoder.com/profile/986587404)
>- @Transactional在使用的时候有没有遇见过因为aop的缺陷而导致的不生效的问题,比如一个类里,没加Transactional的方法,调用加了@Transactional注解的方法,可能生效也可能不生效,不生效的可能原因是什么,要求围绕aop的实现来答,这个我答的不好,面试官要我下去之后看看[源码]()再思考一下
>- Spring有啥特点？IoC底层是什么？如果让你去实现IoC会怎么实现
>- MyBatis的实现原理
>- SpringMVC请求流程、url请求流程 
>- Spring[项目]()启动的时候会加载哪些资源，顺序是怎么样的 
>- Cglib和jdk的动态代理哪个快，原理是什么。 
>- SpringBoot和Spring的区别，简单说一下 
>- spring的配置文件，常见的各种注解（贼多的注解，@Autowired，@Resource，@component等等.......），都有什么用，怎么使用，有什么区别
>- 就是问maven的许多指令(这个好多没答出来，因为是idea玩家，懂的都懂，哈哈哈哈,接着就是springmvc的流程,以及这里面常用的各种注解(我真是快没了，还好[项目](https://www.nowcoder.com/jump/super-jump/word?word=项目)做得多，都能勉强答出一些)
>
>

---------------

>1. 为什么在[项目]()中使用ioc?(这里我答了交给spring管理之后,可以通过干预Spring Bean的生命周期来达到一个可扩展 解耦合的地步,由于答了Spring管理bean的生命周期,所以有了31问的追问)
>2. Spring的生命周期,(反正大概把[源码](https://www.nowcoder.com/jump/super-jump/word?word=源码)那一套东西说了一下,大概答了4分钟,由于提到了Spring在postBeforeInstiation提供了给bean aop的机会,所以有了32问的追问)
>3. Spring自身有什么地方使用了aop么?这我答的是 [@Transactional](https://www.nowcoder.com/profile/986587404)
>4. @Transactional在使用的时候有没有遇见过因为aop的缺陷而导致的不生效的问题,比如一个类里,没加Transactional的方法,调用加了@Transactional注解的方法,可能生效也可能不生效,不生效的可能原因是什么,要求围绕aop的实现来答,这个我答的不好,面试官要我下去之后看看[源码]()再思考一下

>1. 你现在用过哪些中间件?
>2. JPA 和 MyBatis 做对象映射的区别?原理?
>3. 你更倾向于 MyBatis 还是 JPA?
>4. 这两个 ORM 的实现和区别?
>5. 问我平时用什么中间件或组件,dubbo zk elasticsearch springboot springcloud kubernetes mysql
>6. . Mybatis # 和 $ 的区别 
>7. Mybatis接口里的方法和XML里的SQL名可以不一样吗，不一样怎么办 
>8. Mybatis是如何完成SQL和接口里的方法的映射的（我回答了怎么配置），那你知道它是怎么实现的吗 
>9. 了解ElasticSearch么?说一下ElasticSearch从写入数据到别的进程可以看到这个数据的整个流程?
>10. 先写到一个buffer里面，同时把数据写到一个日志里面，然后每隔一秒，那个buffer里的数据会刷到segment file里，写入文件的时候先写pageCache,写  到pageCache之后就可以搜到了
>11. ElasticSearch是实时的么  不是，因为要先写到内存的一个buffer里然后过一段时间再写到磁盘里
>
>- 接着就是mybatis xml文件里各种标签，mybatis执行流程，怎么使用的（嵌套[项目](https://www.nowcoder.com/jump/super-jump/word?word=项目)还进行提问）（这个过程我提醒了面试官我才大三，已经把我掏空了.面试官笑了笑继续提问）
>- 我们来聊下mybatis，你说下mybatis 他的dao接口为什么不写实现类就可以，工作原理。这个老八股文了
>- 那你知道为什么mybatis的XML文件可以转化为bean呢？ 那我肯定不知道啊哈哈哈哈哈
>- mybatis怎么防止sql注入

## spring优势

>- 简化开发，解耦，集成其它框架。
>- 低侵入式设计，代码污染级别较低。
>- Spring的DI机制降低了业务对象替换的复杂性，提高了软件之间的解耦。
>- Spring AOP支持将一些通用的任务进行集中式的管理，例如：安全，事务，日志等，从而使代码能更好的复用。
>- spring高度开放性，并不强制应用依赖于spring,开发者可自由选用spring框架的部分或者全部



## ==Spring Spring MVC Spring Boot 三者比较==

>这三者专注的领域不同，解决的问题也不一样；
>
>Spring 就像一个大家族，有众多衍生产品例如 Boot，Security，JPA等等。但他们的基础都是Spring 的 IOC 和 AOP，IOC提供了依赖注入的容器，而AOP解决了面向切面的编程，然后在此两者的基础上实现了其他衍生产品的高级功能；
>
>spring MVC是基于 Servlet 的一个 MVC 框架，主要解决 WEB 开发的问题，涵盖面包括前端视图、文件配置、后端接口等逻辑开发
>
>因为 Spring 的配置非常复杂，各种xml，properties处理起来比较繁琐。于是为了简化开发者的使用，Spring社区创造性地推出了Spring Boot，它遵循约定优于配置，简化了spring mvc的配置流程。区别于spring mvc的是，springboot更专注于单体微服务接口开发和前端解耦。





## spring Bean生命周期

>1. 实例化 Instantiation
>2. 属性赋值 Populate
>3. 初始化 Initialization
>4. 销毁 Destruction
>
>实例化Bean对象--->设置对象属性---->检查Aware相关接口--->BeanPost前置处理---->检查是否调用初始化方法(并查看afterPropertiesSet方法)--->BeanPost后置处理---->注册必要的(Destruction)相关回调接口-->使用--->是否实现Disposable接口(是否具有自定义destory方法)
>
>1. 实例化Bean ，以反射的方式生成对象
>2. 填充Bean属性： PopulateBean()中方法具体实现，其中这里边就是存在循环依赖问题（三级缓存）
>3. 调用Aware接口相关的方法：例如invokeAwareMethod(完成BeanName,BeanFactory,BeanClassLoader对象属性的赋值)
>4. 调用BeanPostProcessor()中的前置处理方法：使用比较多的有ApplicationContextPostProcessor 设置ApplicationContext中的Environment、Resourceloader等对象
>5. 调用initmethod初始化方法：invokeinitmethod()：判断是否实现了initialzingBean接口
>6. 调用BeanPostProcessor的后置处理方法，spring 中AOP就是在此实现的 AbstractAutoProxyCreator。注册Destuction相关回调接口
>7. 获取到完成对象 可以通过getBean方式来进行对象的获取
>8. 销毁流程  判断是否实现了dispoable接口  调用销毁方法
>
>-------
>
><img src="https://upload-images.jianshu.io/upload_images/4558491-dc3eebbd1d6c65f4.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp" alt="img" style="zoom:67%;" />
>
>#### 第一大类：影响多个Bean的接口
>
>实现了这些接口的Bean会切入到多个Bean的生命周期中。正因为如此，这些接口的功能非常强大，Spring内部扩展也经常使用这些接口，例如自动注入以及AOP的实现都和他们有关。
>
>- BeanPostProcessor									Bean 的实例化、配置和其他的初始化前后添加一些自己的逻辑处理
>- InstantiationAwareBeanPostProcessor
>
>#### 第二大类：只调用一次的接口
>
>这一大类接口的特点是功能丰富，常用于用户自定义扩展。
>第二大类中又可以分为两类：
>
>1. Aware类型的接口
>2. 生命周期接口
>
>##### 简单的两个生命周期接口
>
>至于剩下的两个生命周期接口就很简单了，实例化和属性赋值都是Spring帮助我们做的，能够自己实现的有初始化和销毁两个生命周期阶段。
>
>1. InitializingBean 对应生命周期的初始化阶段，在上面源码的`invokeInitMethods(beanName, wrappedBean, mbd);`方法中调用。
>    有一点需要注意，因为Aware方法都是执行在初始化方法之前，所以可以在初始化方法中放心大胆的使用Aware接口获取的资源，这也是我们自定义扩展Spring的常用方式。
>    除了实现InitializingBean接口之外还能通过注解或者xml配置的方式指定初始化方法，至于这几种定义方式的调用顺序其实没有必要记。因为这几个方法对应的都是同一个生命周期，只是实现方式不同，我们一般只采用其中一种方式。
>2. DisposableBean 类似于InitializingBean，对应生命周期的销毁阶段，以ConfigurableApplicationContext#close()方法作为入口，实现是通过循环取所有实现了DisposableBean接口的Bean然后调用其destroy()方法 。感兴趣的可以自行跟一下源码。



## spring中单例Bean是否线程安全

>spring中Bean对象默认是单例的，框架没有对Bean进行多线程封装处理
>
>线程安全与否取决于是否有共享的资源竞争关系存在，Spring中单例Bean是否是线程安全取决于Bean是有状态的Bean还是无状态的Bean。
>
>- 有状态的Bean：有数据存储功     Bean中有User对象用于存储用户信息；
>- 无状态的Bean：无数据存储功能
>
>------
>
>有状态：spring中Bean如果是有状态的也就是有数据存储功能，那么就需要我们开发人员自己来保证线程安全问题，最好的解决办法就是改变Bean的作用域把`singleton`改变成`prototype`，这样每次请求Bean对象就是相当于创建新的对象来保证线程安全。
>
>无状态：无状态是不会存储数据，我们自身`Controller service dao`层线程不安全，只是调用里边的方法，而且多线程调用一个实例方法，会在内存中复制遍历，这里边是自己线程的工作内存。是线程安全的
>
>-----
>
>因此我们在声明Bean的时候尽量不要声明有状态的实例变量或者类变量，如果非要声明的话，我们可以使用`threadlocal`变量变成线程私有，当前变量只属于当前线程，他们之间批次并不是线程共享的，这样就保证了线程安全问题。
>
>其次如果Bean的实例变量或者类变量需要在多个线程之间共享，那么只能使用`synchronized lock cas`等这些关键字来实现同步方法。
>
>--------
>
>或者在共享变量上 我们可以存放在数据库里边或者缓存里边也是一种解决方案  



## spring中支持的Bean作用域

>1. Singleton: 使用该属性定义Bean的时，IOC容器创建一个Bean实例，IOC容器每次返回的是同一个Bean实例
>2. Prototype: 使用该属性定义Bean的时，IOC容器创建多个Bean实例，每次返回都是一个新的Bean实例
>3. Request:   该属性仅对Http请求产生作用，使用该属性定义Bean的时候，每次Http请求都会创建一个新的Bean，适用于Web环境
>4. Session:  该属性仅用于hTTP Session，同一个session共享一个Bean实例，不同session使用不同的实例。
>5. Global-session: 适用于Http Session 同session的作用域不同，所有session共享一个Bean实例



## spring事务传播机制

>什么是事务传播机制？
>
>多个事务方法相互调用的时，事务如何在这些方发生进行传播，spring提供了7中不同的传播特性。
>
>-----
>
>在Spring中对于事务的传播行为定义了七种类型分别是：**REQUIRED、SUPPORTS、MANDATORY、REQUIRES_NEW、NOT_SUPPORTED、NEVER、NESTED**。
>
>- required(spring默认传播机制) 		**如果当前没有事务，则自己新建一个事务，如果当前存在事务，则加入这个事务**
>- Supports :                                          **当前存在事务，则加入当前事务，如果当前没有事务，就以非事务方法执行**
>- Mandatory:                                        **当前存在事务，则加入当前事务，如果当前事务不存在，则抛出异常。**
>- Require_new                                      **创建一个新事务，如果存在当前事务，则挂起该事务(阻塞)。**不管A有没有事务 B就是要创建一个新事物
>- Not_supported:                                 **始终以非事务方式执行,如果当前存在事务，则挂起当前事务**不论当前是否存在事务，都会以非事务的方式运行
>- never:                                                  **不使用事务，如果当前事务存在，则抛出异常**  以非事务方式来运行
>- Nested:                                               **如果当前事务存在，则在嵌套事务中执行，否则REQUIRED的操作一样（开启一个事务）**
>
>解释嵌套的意思：如果方法A有事务，那么在调用B方法时，会把A当前事务设置一个保存点，B按照这个事务往下走，如果B异常回滚，回到A保存的那个节点，也就是像开启一个临时线程来保存一下状态。
>
>Nested和REQUIRES_NEW的区别:
>
>REQUIRES_NEW是新建一个事务并且新开启的这个事务与原有事务无关，而NESTED则是当前存在事务时（我们把当前事务称之为父事务）会开启一个嵌套事务（称之为一个子事务）。
>在NESTED情况下父事务回滚时，子事务也会回滚，而在REQUIRES_NEW情况下，原有事务回滚，不会影响新开启的事务。
>
>Nested和REQUIRED的区别
>
>REQUIRED情况下，调用方存在事务时，则被调用方和调用方使用同一事务，那么被调用方出现异常时，由于共用一个事务，所以无论调用方是否catch其异常，事务都会回滚
>而在NESTED情况下，被调用方发生异常时，调用方可以catch其异常，这样只有子事务回滚，父事务不受影响



## ==IOC 谈谈springIOC的理解==

>IOC有两层意思：第一就是控制反转思想  第二就是容器
>
>首先就是**控制反转**思想：原来的对象是由使用者进行控制，有了spring之后，就可以把对象交给spring来帮我进行管理, 依赖对象的获取给反转了。之前，依赖对象由对象内部主动创建获取，现在，依赖对象由容器创建，对象从容器中获取依赖对象。
>
>**DI**: IoC的一个重点是在系统运行中，动态的向某个对象提供它所需要的其他对象。这一点是通过DI（Dependency Injection，依赖注入）来实现的。  简单理解：
>A对象需要一个B对象的依赖，以前，我们需要编写代码手动构建B对象，有了DI(依赖注入)，我们不需要构建B对象、何时构建，Spring会在合适的时候注入B对象，完成各个对象之间的控制。
>
>
>
>容器设计上：对于 IoC 来说，最重要的就是容器，容器管理着 Bean 的生命周期，控制着 Bean 的依赖注入。Spring中设计了两个接口来表示容器，分别是BeanFactory、ApplicationContext。
>
>BeanFactory： BeanFactory可以理解为就是个 HashMap，Key 是 BeanName，Value 是 Bean 实例。通常只提供注册（put），获取（get）这两个功能。
>
>ApplicationContext： ApplicationContext比 BeanFactory 多了更多的功能，比如：资源的获取，支持多种消息、以及国际化等，该接口定义了一个 refresh 方法，即重新加载/刷新所有的 Bean。
>
>-----
>
>容器：存储对象，使用map结构来存储，在spring中一般存在三级缓存，singletonObjects存放完成的bean对象。
>
>​		    整个bean的生命周期，重创建到使用到销毁的过程中都是由容器来管理的（bean的生命周期）

## ==AOP 谈谈spring AOP的理解==

>1. AOP（Aspect Oriented Programming），即面向切面编程，可以说是 OOP（Object Oriented Programming，面向对象编程）的补充和完善。
>
>AOP是Spring框架面向切面的编程思想，AOP采用一种称为“横切”的技术，将涉及多业务流程的通用功能抽取并单独封装，形成独立的切面，在合适的时机将这些切面横向切入到业务流程指定的位置中。以下结合实际案例详细讲述AOP的原理及实现过程。
>
>**● Aspect**
>
>表示切面。切入业务流程的一个独立模块。例如，前面案例的VerifyUserAspect类，一个应用程序可以拥有任意数量的切面。
>
>**● Join point**
>
>表示连接点。也就是业务流程在运行过程中需要插入切面的具体位置。例如，前面案例的EmailNoticeImpl类的setTeacher方法就是一个连接点。
>
>**● Advice**
>
>表示通知。是切面的具体实现方法。可分为前置通知（@Before）、后置通知（@After）、异常通知（@AfterThrowing）、返回通知（@AfterReturning）和环绕通知（@Around）五种。实现方法具体属于哪类通知，是在配置文件和注解中指定的。例如，VerifyUserAspect类的beforeAdvice方法就是前置通知。
>
>**● Pointcut**
>
>表示切入点。用于定义通知应该切入到哪些连接点上，不同的通知通常需要切入到不同的连接点上。例如，前面案例配置文件的`<aop:pointcut>`标签。
>
>**● Target**
>
>表示目标对象。被一个或者多个切面所通知的对象。例如，前面案例的EmailNoticeImpl类。
>
>**● Proxy**
>
>表示代理对象。将通知应用到目标对象之后被动态创建的对象。可以简单地理解为，代理对象为目标对象的业务逻辑功能加上被切入的切面所形成的对象。
>
>**● Weaving**
>
>表示切入，也称为织入。将切面应用到目标对象从而创建一个新的代理对象的过程。这个过程可以发生在编译期、类装载期及运行期。
>
> `Spring`的`AOP`实现原理其实很简单，就是通过**动态代理**实现的。如果我们为`Spring`的某个`bean`配置了切面，那么`Spring`在创建这个`bean`的时候，实际上创建的是这个`bean`的一个代理对象，我们后续对`bean`中方法的调用，实际上调用的是代理类重写的代理方法。而`Spring`的`AOP`使用了两种动态代理，分别是**JDK的动态代理**，以及**CGLib的动态代理**。
>
>**（一）JDK动态代理**
>
>```xml
> * Cglib 夫类动态代理 跟JDK接口动态代理区别就是
>
> * Proxy.newInstance(ClassLoader classLoader,Interface[],InvocationHandler handler)
> * JDK动态代理类 没有源文件 也即没有.class文件 没有.class文件也就无法创建通过类加载器创建java.lang.Class对象 重而就无法创建类实例
> * 源码程序进行验证、优化、缓存、同步、生成字节码sun.misc.ProxyGenerator::generatorProoxyClass()方法来完成生成字节码的动作件 但是字节码有了 ，没有类加载器就无法将字节码文件加载进JVM当中 所以就需要借一个类加载器（随便那个都可以）
> * JDK动态代理需要实现目标类实现的接口时Interface[] 例如UserService.getClass.getInterface();
> * InvocationHandler 实现这个接口完成  public Object invoke(Object proxy, Method method, Object[] args)  来完成额外附加的方法
> * proxy是目标类 method是目标方法 args是目标方法的参数   通过method.invoke(target,args);
>
> * 而Cglib 基于代理是我们想代理某个类 而这个类又没有实现接口 所以Cglib是父子继承的动态代理
> * Proxy.newInstance(ClassLoader classLoader,Interface[],InvocationHandler 实施invoke方法)
> * Enhancer.setClassLoader();
> * Enhance.setSupperClass()
> * MethodInterceptor 实施interceptor方法
> * Enhancer.create();
>cglib 没有接口也能实现动态代理，而且采用字节码增强技术，性能也不错。  由于CGLib由于是采用动态创建子类的方法，对于final方法，无法进行代理。
>JDK 动态代理是基于接口设计实现的，如果没有接口，会抛异常。
>```
>
>  **Spring默认使用JDK的动态代理实现AOP，类如果实现了接口，Spring就会使用这种方式实现动态代理**。熟悉`Java`语言的应该会对`JDK`动态代理有所了解。`JDK`实现动态代理需要两个组件，首先第一个就是`InvocationHandler`接口。我们在使用`JDK`的动态代理时，需要编写一个类，去实现这个接口，然后重写`invoke`方法，这个方法其实就是我们提供的代理方法。然后`JDK`动态代理需要使用的第二个组件就是`Proxy`这个类，我们可以通过这个类的`newProxyInstance`方法，返回一个代理对象。生成的代理类实现了原来那个类的所有接口，并对接口的方法进行了代理，我们通过代理对象调用这些方法时，底层将通过反射，调用我们实现的`invoke`方法。
>
>`JDK`的动态代理是基于**反射**实现。`JDK`通过反射，生成一个代理类，这个代理类实现了原来那个类的全部接口，并对接口中定义的所有方法进行了代理。当我们通过代理对象执行原来那个类的方法时，代理类底层会通过反射机制，回调我们实现的`InvocationHandler`接口的`invoke`方法。**并且这个代理类是Proxy类的子类**（记住这个结论，后面测试要用）。这就是`JDK`动态代理大致的实现方式。
>
>**（二）CGLib动态代理**
>
>  `JDK`的动态代理存在限制，那就是被代理的类必须是一个实现了接口的类，代理类需要实现相同的接口，代理接口中声明的方法。若需要代理的类没有实现接口，此时`JDK`的动态代理将没有办法使用，于是`Spring`会使用`CGLib`的动态代理来生成代理对象。`CGLib`直接操作字节码，生成类的子类，重写类的方法完成代理。
>
>  以上就是`Spring`实现动态的两种方式，下面我们具体来谈一谈这两种生成动态代理的方式。
>
>

## spring IOC 底层实现 getBean流程

>1. 先通过BeanFactory创建一个Bean工厂
>2. 开始循环创建对象，因为容器中的bean默认都是单例的，所以通过getBean doGetBean从容器中查找
>3. 如果找不到通过createBean,doCreateBean方法，以反射方式创建对象，一般以无惨构造方法来创建
>4. 进行对象的属性填充 populateBean
>5. 进行其他的初始化操作  (initializingBean)





## Spring容器的启动流程

![image-20210711192434607](/Users/whig/Library/Application Support/typora-user-images/image-20210711192434607.png)

>- 1、初始化Spring容器，注册内置的BeanPostProcessor的BeanDefinition到容器中
>- 2、将配置类的BeanDefinition注册到容器中
>- 3、调用refresh()方法刷新容器
>
>-----
>
>spring容器的初始化时，通过this()调用了无参构造函数，主要做了以下三个事情：
>
>（1）实例化BeanFactory【DefaultListableBeanFactory】工厂，用于生成Bean对象
>（2）实例化BeanDefinitionReader注解配置读取器，用于对特定注解（如@Service、@Repository）的类进行读取转化成  BeanDefinition 对象，（BeanDefinition 是 Spring 中极其重要的一个概念，它存储了 bean 对象的所有特征信息，如是否单例，是否懒加载，factoryBeanName 等）
>（3）实例化ClassPathBeanDefinitionScanner路径扫描器，用于对指定的包目录进行扫描查找 bean 对象
>
>```java
>public AnnotationConfigApplicationContext(Class<?>... annotatedClasses) {
>    // 注册 Spring 内置后置处理器的 BeanDefinition 到容器
>    this();
>    // 注册配置类 BeanDefinition 到容器
>    register(annotatedClasses);				传入的 Spring 配置类，解析成一个 BeanDefinition 然后注册到容器中
>    // 加载或者刷新容器中的Bean
>    refresh();
>}
>```
>
>-------
>
>refresh()主要用于容器的刷新，Spring 中的每一个容器都会调用 refresh() 方法进行刷新
>
>```java
>public void refresh() throws BeansException, IllegalStateException {
>	synchronized (this.startupShutdownMonitor) {
>		// 1. 刷新前的预处理
>		prepareRefresh();
> 
>		// 2. 获取 beanFactory，即前面创建的【DefaultListableBeanFactory】
>		ConfigurableListableBeanFactory beanFactory = obtainFreshBeanFactory();
> 
>		// 3. 预处理 beanFactory，向容器中添加一些组件
>		prepareBeanFactory(beanFactory);
> 
>		try {
>			// 4. 子类通过重写这个方法可以在 BeanFactory 创建并与准备完成以后做进一步的设置
>			postProcessBeanFactory(beanFactory);
> 
>			// 5. 执行 BeanFactoryPostProcessor 方法，beanFactory 后置处理器
>			invokeBeanFactoryPostProcessors(beanFactory);
> 
>			// 6. 注册 BeanPostProcessors，bean 后置处理器
>			registerBeanPostProcessors(beanFactory);
> 
>			// 7. 初始化 MessageSource 组件（做国际化功能；消息绑定，消息解析）
>			initMessageSource();
> 
>			// 8. 初始化事件派发器，在注册监听器时会用到
>			initApplicationEventMulticaster();
> 
>			// 9. 留给子容器（子类），子类重写这个方法，在容器刷新的时候可以自定义逻辑，web 场景下会使用
>			onRefresh();
> 
>			// 10. 注册监听器，派发之前步骤产生的一些事件（可能没有）
>			registerListeners();
> 
>			// 11. 初始化所有的非单实例 bean
>			finishBeanFactoryInitialization(beanFactory);
> 
>			// 12. 发布容器刷新完成事件
>			finishRefresh();
>		}
>		...
>	}
>}
>```
>
>1、prepareRefresh()刷新前的预处理：
>
>- initPropertySources()：初始化一些属性设置，子类自定义个性化的属性设置方法；
>- getEnvironment().validateRequiredProperties()：检验属性的合法性
>- earlyApplicationEvents = new LinkedHashSet<ApplicationEvent>()：保存容器中的一些早期的事件；
>
>----
>
>2. obtainFreshBeanFactory()：获取在容器初始化时创建的BeanFactory：
>
>（1）refreshBeanFactory()：刷新BeanFactory，设置序列化ID；
>（2）getBeanFactory()：返回初始化中的GenericApplicationContext创建的BeanFactory对象，即【DefaultListableBeanFactory】类型
>
>----
>
>3、prepareBeanFactory(beanFactory)：BeanFactory的预处理工作，向容器中添加一些组件：
>
>（1）设置BeanFactory的类加载器、设置表达式解析器等等
>（2）添加BeanPostProcessor【ApplicationContextAwareProcessor】
>（3）设置忽略自动装配的接口：EnvironmentAware、EmbeddedValueResolverAware、ResourceLoaderAware、  ApplicationEventPublisherAware、MessageSourceAware、ApplicationContextAware；
>（4）注册可以解析的自动装配类，即可以在任意组件中通过注解自动注入：BeanFactory、ResourceLoader、ApplicationEventPublisher、ApplicationContext
>（5）添加BeanPostProcessor【ApplicationListenerDetector】
>（6）添加编译时的AspectJ；
>（7）给BeanFactory中注册的3个组件：environment【ConfigurableEnvironment】、systemProperties【Map<String, Object>】、systemEnvironment【Map<String, Object>】
>
>------
>
>4、postProcessBeanFactory(beanFactory)：子类重写该方法，可以实现在BeanFactory创建并预处理完成以后做进一步的设置
>
>------
>
>5、invokeBeanFactoryPostProcessors(beanFactory)：在BeanFactory标准初始化之后执行BeanFactoryPostProcessor的方法，即BeanFactory的后置处理器：
>
>（1）先执行BeanDefinitionRegistryPostProcessor： postProcessor.postProcessBeanDefinitionRegistry(registry)
>
>① 获取所有的实现了BeanDefinitionRegistryPostProcessor接口类型的集合
>② 先执行实现了PriorityOrdered优先级接口的BeanDefinitionRegistryPostProcessor
>③ 再执行实现了Ordered顺序接口的BeanDefinitionRegistryPostProcessor
>④ 最后执行没有实现任何优先级或者是顺序接口的BeanDefinitionRegistryPostProcessors        
>（2）再执行BeanFactoryPostProcessor的方法：postProcessor.postProcessBeanFactory(beanFactory)
>
>① 获取所有的实现了BeanFactoryPostProcessor接口类型的集合
>② 先执行实现了PriorityOrdered优先级接口的BeanFactoryPostProcessor
>③ 再执行实现了Ordered顺序接口的BeanFactoryPostProcessor
>④ 最后执行没有实现任何优先级或者是顺序接口的BeanFactoryPostProcessor
>
>-----
>
>6、registerBeanPostProcessors(beanFactory)：向容器中注册Bean的后置处理器BeanPostProcessor，它的主要作用是干预Spring初始化bean的流程，从而完成代理、自动注入、循环依赖等功能
>
>（1）获取所有实现了BeanPostProcessor接口类型的集合：
>（2）先注册实现了PriorityOrdered优先级接口的BeanPostProcessor；
>（3）再注册实现了Ordered优先级接口的BeanPostProcessor；
>（4）最后注册没有实现任何优先级接口的BeanPostProcessor；
>（5）最refresh主要可划分为12个步骤，其中比较重要的步骤下面会有详细说明。Spring 中的每一个容器都会调用 refresh() 方法进行刷新，无论是 Spring 的父子容器，还是 Spring Cloud Feign 中的 feign 隔离容器，每一个容器都会调用这个方法完成初始化。终注册MergedBeanDefinitionPostProcessor类型的BeanPostProcessor：beanFactory.addBeanPostProcessor(postProcessor);
>（6）给容器注册一个ApplicationListenerDetector：用于在Bean创建完成后检查是否是ApplicationListener，如果是，就把Bean放到容器中保存起来：applicationContext.addApplicationListener((ApplicationListener<?>) bean);
>此时容器中默认有6个默认的BeanProcessor(无任何代理模式下)：【ApplicationContextAwareProcessor】、【ConfigurationClassPostProcessorsAwareBeanPostProcessor】、【PostProcessorRegistrationDelegate】、【CommonAnnotationBeanPostProcessor】、【AutowiredAnnotationBeanPostProcessor】、【ApplicationListenerDetector】
>
>-----
>
>7、initMessageSource()：初始化MessageSource组件，主要用于做国际化功能，消息绑定与消息解析：
>
>（1）看BeanFactory容器中是否有id为messageSource 并且类型是MessageSource的组件：如果有，直接赋值给messageSource；如果没有，则创建一个DelegatingMessageSource；
>（2）把创建好的MessageSource注册在容器中，以后获取国际化配置文件的值的时候，可以自动注入MessageSource；
>
>---
>
>8、initApplicationEventMulticaster()：初始化事件派发器，在注册监听器时会用到：
>
>（1）看BeanFactory容器中是否存在自定义的ApplicationEventMulticaster：如果有，直接从容器中获取；如果没有，则创建一个SimpleApplicationEventMulticaster
>（2）将创建的ApplicationEventMulticaster添加到BeanFactory中，以后其他组件就可以直接自动注入
>
>----
>
>9、onRefresh()：留给子容器、子类重写这个方法，在容器刷新的时候可以自定义逻辑
>
>-----
>
>10、registerListeners()：注册监听器：将容器中所有的ApplicationListener注册到事件派发器中，并派发之前步骤产生的事件：
>
> （1）从容器中拿到所有的ApplicationListener
>（2）将每个监听器添加到事件派发器中：getApplicationEventMulticaster().addApplicationListenerBean(listenerBeanName);
>（3）派发之前步骤产生的事件applicationEvents：getApplicationEventMulticaster().multicastEvent(earlyEvent);
>
>-----
>
>11、finishBeanFactoryInitialization(beanFactory)：初始化所有剩下的单实例bean，核心方法是preInstantiateSingletons()，会调用getBean()方法创建对象；
>
>（1）获取容器中的所有beanDefinitionName，依次进行初始化和创建对象
>（2）获取Bean的定义信息RootBeanDefinition，它表示自己的BeanDefinition和可能存在父类的BeanDefinition合并后的对象
>（3）如果Bean满足这三个条件：非抽象的，单实例，非懒加载，则执行单例Bean创建流程：    
>（4）所有Bean都利用getBean()创建完成以后，检查所有的Bean是否为SmartInitializingSingleton接口的，如果是；就执行afterSingletonsInstantiated()；
>
>------
>
>12、finishRefresh()：发布BeanFactory容器刷新完成事件：
>
>（1）initLifecycleProcessor()：初始化和生命周期有关的后置处理器：默认从容器中找是否有lifecycleProcessor的组件【LifecycleProcessor】，如果没有，则创建一个DefaultLifecycleProcessor()加入到容器；
>（2）getLifecycleProcessor().onRefresh()：拿到前面定义的生命周期处理器（LifecycleProcessor）回调onRefresh()方法
>（3）publishEvent(new ContextRefreshedEvent(this))：发布容器刷新完成事件；
>（4）liveBeansView.registerApplicationContext(this);



## spring如何解决循环依赖

>三级缓存、提前暴露对象、AOP
>
>首先，需要明确的是spring对循环依赖的处理有三种情况： ①构造器的循环依赖：这种依赖spring是处理不了的，直 接抛出BeanCurrentlylnCreationException异常。 ②单例模式下的setter循环依赖：通过“三级缓存”处理循环依赖。 ③非单例循环依赖：无法处理。
>
>spring单例对象的初始化大略分为三步：
>
>1. createBeanInstance：实例化，其实也就是调用对象的构造方法实例化对象
>2. populateBean：填充属性，这一步主要是多bean的依赖属性进行填充
>3. initializeBean：调用spring xml中的init 方法。
>
>----
>
>singletonFactories ： 进入实例化阶段的单例对象工厂的cache （三级缓存）
>
>earlySingletonObjects ：完成实例化但是尚未初始化的，提前暴光的单例对象的Cache （二级缓存）
>
>singletonObjects：完成初始化的单例对象的cache（一级缓存）
>
>
>
>- Spring是通过递归的方式获取目标bean及其所依赖的bean的；
>- Spring实例化一个bean的时候，是分两步进行的，首先实例化目标bean，然后为其注入属性。
>
>结合这两点，也就是说，Spring在实例化一个bean的时候，是首先递归的实例化其所依赖的所有bean，直到某个bean没有依赖其他bean，此时就会将该实例返回，然后反递归的将获取到的bean设置为各个上层bean的属性的。









## AOP

>AOP是Spring框架面向切面的编程思想，AOP采用一种称为“横切”的技术，将涉及多业务流程的通用功能抽取并单独封装，形成独立的切面，在合适的时机将这些切面横向切入到业务流程指定的位置中。以下结合实际案例详细讲述AOP的原理及实现过程。
>
>**● Aspect**
>
>表示切面。切入业务流程的一个独立模块。例如，前面案例的VerifyUserAspect类，一个应用程序可以拥有任意数量的切面。
>
>**● Join point**
>
>表示连接点。也就是业务流程在运行过程中需要插入切面的具体位置。例如，前面案例的EmailNoticeImpl类的setTeacher方法就是一个连接点。
>
>**● Advice**
>
>表示通知。是切面的具体实现方法。可分为前置通知（@Before）、后置通知（@After）、异常通知（@AfterThrowing）、返回通知（@AfterReturning）和环绕通知（@Around）五种。实现方法具体属于哪类通知，是在配置文件和注解中指定的。例如，VerifyUserAspect类的beforeAdvice方法就是前置通知。
>
>**● Pointcut**
>
>表示切入点。用于定义通知应该切入到哪些连接点上，不同的通知通常需要切入到不同的连接点上。例如，前面案例配置文件的`<aop:pointcut>`标签。
>
>**● Target**
>
>表示目标对象。被一个或者多个切面所通知的对象。例如，前面案例的EmailNoticeImpl类。
>
>**● Proxy**
>
>表示代理对象。将通知应用到目标对象之后被动态创建的对象。可以简单地理解为，代理对象为目标对象的业务逻辑功能加上被切入的切面所形成的对象。
>
>**● Weaving**
>
>表示切入，也称为织入。将切面应用到目标对象从而创建一个新的代理对象的过程。这个过程可以发生在编译期、类装载期及运行期。
>
>----
>
>
>
> `Spring`的`AOP`实现原理其实很简单，就是通过**动态代理**实现的。如果我们为`Spring`的某个`bean`配置了切面，那么`Spring`在创建这个`bean`的时候，实际上创建的是这个`bean`的一个代理对象，我们后续对`bean`中方法的调用，实际上调用的是代理类重写的代理方法。而`Spring`的`AOP`使用了两种动态代理，分别是**JDK的动态代理**，以及**CGLib的动态代理**。
>
>**（一）JDK动态代理**
>
>```xml
>  * Cglib 夫类动态代理 跟JDK接口动态代理区别就是
>
>  * Proxy.newInstance(ClassLoader classLoader,Interface[],InvocationHandler handler)
>  * JDK动态代理类 没有源文件 也即没有.class文件 没有.class文件也就无法创建通过类加载器创建java.lang.Class对象 重而就无法创建类实例
>  * 源码程序进行验证、优化、缓存、同步、生成字节码sun.misc.ProxyGenerator::generatorProoxyClass()方法来完成生成字节码的动作件 但是字节码有了 ，没有类加载器就无法将字节码文件加载进JVM当中 所以就需要借一个类加载器（随便那个都可以）
>  * JDK动态代理需要实现目标类实现的接口时Interface[] 例如UserService.getClass.getInterface();
>  * InvocationHandler 实现这个接口完成  public Object invoke(Object proxy, Method method, Object[] args)  来完成额外附加的方法
>  * proxy是目标类 method是目标方法 args是目标方法的参数   通过method.invoke(target,args);
>
>  * 而Cglib 基于代理是我们想代理某个类 而这个类又没有实现接口 所以Cglib是父子继承的动态代理
>  * Proxy.newInstance(ClassLoader classLoader,Interface[],InvocationHandler 实施invoke方法)
>  * Enhancer.setClassLoader();
>  * Enhance.setSupperClass()
>  * MethodInterceptor 实施interceptor方法
>  * Enhancer.create();
>cglib 没有接口也能实现动态代理，而且采用字节码增强技术，性能也不错。  由于CGLib由于是采用动态创建子类的方法，对于final方法，无法进行代理。
>JDK 动态代理是基于接口设计实现的，如果没有接口，会抛异常。
>```
>
>  **Spring默认使用JDK的动态代理实现AOP，类如果实现了接口，Spring就会使用这种方式实现动态代理**。熟悉`Java`语言的应该会对`JDK`动态代理有所了解。`JDK`实现动态代理需要两个组件，首先第一个就是`InvocationHandler`接口。我们在使用`JDK`的动态代理时，需要编写一个类，去实现这个接口，然后重写`invoke`方法，这个方法其实就是我们提供的代理方法。然后`JDK`动态代理需要使用的第二个组件就是`Proxy`这个类，我们可以通过这个类的`newProxyInstance`方法，返回一个代理对象。生成的代理类实现了原来那个类的所有接口，并对接口的方法进行了代理，我们通过代理对象调用这些方法时，底层将通过反射，调用我们实现的`invoke`方法。
>
>`JDK`的动态代理是基于**反射**实现。`JDK`通过反射，生成一个代理类，这个代理类实现了原来那个类的全部接口，并对接口中定义的所有方法进行了代理。当我们通过代理对象执行原来那个类的方法时，代理类底层会通过反射机制，回调我们实现的`InvocationHandler`接口的`invoke`方法。**并且这个代理类是Proxy类的子类**（记住这个结论，后面测试要用）。这就是`JDK`动态代理大致的实现方式。
>
>**（二）CGLib动态代理**
>
>  `JDK`的动态代理存在限制，那就是被代理的类必须是一个实现了接口的类，代理类需要实现相同的接口，代理接口中声明的方法。若需要代理的类没有实现接口，此时`JDK`的动态代理将没有办法使用，于是`Spring`会使用`CGLib`的动态代理来生成代理对象。`CGLib`直接操作字节码，生成类的子类，重写类的方法完成代理。
>
>  以上就是`Spring`实现动态的两种方式，下面我们具体来谈一谈这两种生成动态代理的方式。



## spring注解 

>-----------------------------------------------------------------------------创建对象相关注解-------------------------------------------------------------------------------------------------------------
>
>- **@Component 声明bean**
>
>```xml
>@Component                         实体类不需要注解 因为实体类是跟数据库属性对应 为DAO提供
>@Service 在业务逻辑层使用（service层）
>@Repository 在数据访问层使用（dao层）
>@Controller 在展现层使用，控制器的声明（Controller）
>
>@Componet
>public Class User{    ====  <bean id="user"  class="com.whig.pojo.User"/>
>							<默认id=user 就是 类名小写   或者直接@Compomet("whig")  id=whig
>                            后续可以让xml来覆盖注解 但是id值和class必须和注解的保持一致
>                             
>}
>                             spring与mybatis整合  不需要注解 @Repository 和 @Compenet
>```
>
>- **@scope 作用域**
>
>```xml
><bean id="user" class="com.whig.User" scope="singelon|propotrpe" />   spring xml中不写scope默认是单例
>
>@Component              这里类上如果不加@scope也是单例
>@Scope("singelon")
>public Class User{
>
>}
>```
>
>- **@Lazy 延迟创建**
>
>```xml
>这个只对于 单例模式下起作用    <bean id="user" class="com.whig.User" scope="singelon|propotrpe " lazy-init="true" />
>工厂创建的时候并不会初始化bean  而是在调用的时候在创建
>```
>
>- 生命周期相关注解
>
>```xml
>1.初始化相关方法 
>  initialngBean            ==@PostConstruct
>  <bean init-method=""/>
>
>2.销毁方法
>  DisposableBean  Disposable=用完即可丢弃的
>  <bean init-destory=""/>   ==@PreDestory
>
>JSR(JAVA EE )520提供的
>```
>
>---------------------------------------------
>
>-----------------------------------------------------------------------------注入相关注解-------------------------------------------------------------------------------------------------------------
>
>- Autowired 这个是对用户自定义类 为另一个类注入 当一个属性  而不能当JDK类型
>
>```xml
>如上述配置   下述是用户自定义类    Autowired  是利用 set注入 <property name="" ref=”“>  ==》UserDao userDao=new UserServiceImpl*****
>    																								UserServiceImpl前提以是bean
>AutoWired 细节分析
>    1.是基于类型进行注入的 ： 注入对象的类型 必须与目标成员变量类型相同或者其子类（实现类）
>    
>    2.基于名字类进行注入  ： 配合 @Qualifier("userDaoImpl") 必须是这样写的 因为UserDaoImpl对象注入到容器了 而@Qualifier("userDao")并不可以
>    
>    3.方式位置 ： 
>    			set()方法上： spring是通过调用set方法来为成员变量赋值
>    			成员变量上：   spring是通过反射直接对成员变量来进行注入（赋值）
>    
>    4.java EE规范的类似注解
>    			@Resource("name=userDaoImpl") ==@AutoWired+@Qualifier("userDaoImpl")  基于名字来进行注入
>    			@Resource                     ==@AutoWired                            基于类型来进程注入
>     
>```
>
>
>
>--------------------------------------------------------------------------------------------JDK内置成员变量 注入属性--------------------------------------------------------
>
>​                                                                这个其实一般用不上  我们pojo都是数据库映射 dao来操作pojo 
>
>```java
>@Component
>@PropertySource("classpath:/init.properties")    //读取配置文件的位置 来添加属性
>public class Category {
>    @Value("${id}")
>    private Integer id;
>    @Value("${name}")
>    private String name;
>
>    /**
>     * <bean id="category" class="com.whig.pojo.Category"/>  ===@Component
>     *      <property name="id" value="10"/>                 ===须在配置文件中写
>     *      <property name="name" value="ahui"/>
>     */
>}
>
>@Value 注意细节
>    1.不能对类变量、静态成员变量赋值
>    2.不能对集合类进行赋值  yml文件可以支持
>```
>
>- 注解开发思考
>
>```xml
>什么时候该使用注解  什么时候使用xml
>	spring注解配置 和xml配置是相同的
>	
>	使用注解：程序员自己开发的类 UserServieImpl UserDaoImpl  
>	
>	使用xml:应用其他程序员开发的类型 sqlSessionFactory ScanMapperConfig 只能就是xml配置
>
>
>```
>
>- **@configuration 相当于替换掉原来的application.xml   底层是cglib代理实现 增加额外功能 默认单例**
>
>- **@Bean**
>
>```markdown
>@configuration相当于 替换掉原来的xml文件
>
>@Bean是在配置文件下生效的 相当于原来的 <bean id class >  
>			注意事项：这里可以自定义ID  @Bean("user");
>					创建对象创建次数  @Bean()  在加@Scope
>
>创建对象分为两种 简单对象 复杂对象                     疑问创建对象 @Component 必须在xml文件中配置包扫描路径
>```
>
>



## spring注解

>**@RequestBody**：主要用来接收前端传递给后端的json字符串中的数据的(请求体中的数据的)；GET方式无请求体，所以使用@RequestBody接收数据时，前端不能使用GET方式提交数据，而是用POST方式进行提交。在后端的同一个接收方法里，@RequestBody与@RequestParam()可以同时使用，@RequestBody最多只能有一个，而@RequestParam()可以有多个
>
>**@ResponseBody**  主要就是用于后端返回给前端数据 就是json数据格式被 对吧哈
>
>**@valid**：校验规则
>
>**@CrossOrigin**    //这个就是解决跨域支持被 就是哈
>
>**@PathVariable** 对应路径上的变量，用在参数前，路径上的变量名需和参数名称一致
>
>**1、@SpringBootApplication**
>
>这是 Spring Boot 最最最核心的注解，用在 Spring Boot 主类上，标识这是一个 Spring Boot 应用，用来开启 Spring Boot 的各项能力。
>
>其实这个注解就是 `@SpringBootConfiguration`、`@EnableAutoConfiguration`、`@ComponentScan` 这三个注解的组合，也可以用这三个注解来代替 `@SpringBootApplication` 注解。
>
>**2、@EnableAutoConfiguration**
>
>允许 Spring Boot 自动配置注解，开启这个注解之后，Spring Boot 就能根据当前类路径下的包或者类来配置 Spring Bean。
>
>如：当前类路径下有 Mybatis 这个 JAR 包，`MybatisAutoConfiguration` 注解就能根据相关参数来配置 Mybatis 的各个 Spring Bean。
>
>**3、@Configuration**
>
>这是 Spring 3.0 添加的一个注解，用来代替 applicationContext.xml 配置文件，所有这个配置文件里面能做到的事情都可以通过这个注解所在类来进行注册。
>
>**4、@SpringBootConfiguration**
>
>这个注解就是 @Configuration 注解的变体，只是用来修饰是 Spring Boot 配置而已，或者可利于 Spring Boot 后续的扩展。
>
>**5、@ComponentScan**
>
>这是 Spring 3.1 添加的一个注解，用来代替配置文件中的 component-scan 配置，开启组件扫描，即自动扫描包路径下的 @Component 注解进行注册 bean 实例到 context 中。
>
>前面 5 个注解可以在Java技术栈的这篇文章《[Spring Boot 最核心的 3 个注解详解](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/kNvy_0jb4oJtYdaxryq5xg)》中了解更多细节的。
>
>**6、@Conditional**
>
>这是 Spring 4.0 添加的新注解，用来标识一个 Spring Bean 或者 Configuration 配置文件，当满足指定的条件才开启配置。
>
>**7、@ConditionalOnBean**
>
>组合 `@Conditional` 注解，当容器中有指定的 Bean 才开启配置。
>
>**8、@ConditionalOnMissingBean**
>
>组合 `@Conditional` 注解，和 `@ConditionalOnBean` 注解相反，当容器中没有指定的 Bean 才开启配置。
>
>**9、@ConditionalOnClass**
>
>组合 `@Conditional` 注解，当容器中有指定的 Class 才开启配置。
>
>**10、@ConditionalOnMissingClass**
>
>组合 `@Conditional` 注解，和 `@ConditionalOnMissingClass` 注解相反，当容器中没有指定的 Class 才开启配置。
>
>**11、@ConditionalOnWebApplication**
>
>组合 `@Conditional` 注解，当前项目类型是 WEB 项目才开启配置。
>
>**12、@ConditionalOnNotWebApplication**
>
>组合 `@Conditional` 注解，和 `@ConditionalOnWebApplication` 注解相反，当前项目类型不是 WEB 项目才开启配置。
>
>**13、@ConditionalOnProperty**
>
>组合 `@Conditional` 注解，当指定的属性有指定的值时才开启配置。
>
>**14、@ConditionalOnExpression**
>
>组合 `@Conditional` 注解，当 SpEL 表达式为 true 时才开启配置。
>
>**15、@ConditionalOnJava**
>
>组合 `@Conditional` 注解，当运行的 Java JVM 在指定的版本范围时才开启配置。
>
>**16、@ConditionalOnResource**
>
>组合 `@Conditional` 注解，当类路径下有指定的资源才开启配置。
>
>**17、@ConditionalOnJndi**
>
>组合 `@Conditional` 注解，当指定的 JNDI 存在时才开启配置。
>
>**18、@ConditionalOnCloudPlatform**
>
>组合 `@Conditional` 注解，当指定的云平台激活时才开启配置。
>
>**19、@ConditionalOnSingleCandidate**
>
>组合 `@Conditional` 注解，当指定的 class 在容器中只有一个 Bean，或者同时有多个但为首选时才开启配置。
>
>**20、@ConfigurationProperties**
>
>用来加载额外的配置（如 .properties 文件），可用在 `@Configuration` 注解类，或者 `@Bean` 注解方法上面。
>
>关于这个注解的用法可以参考Java技术栈《 [Spring Boot读取配置的几种方式](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/aen2PIh0ut-BSHad-Bw7hg)》这篇文章。
>
>**21、@EnableConfigurationProperties**
>
>一般要配合 `@ConfigurationProperties` 注解使用，用来开启对 `@ConfigurationProperties` 注解配置 Bean 的支持。
>
>**22、@AutoConfigureAfter**
>
>用在自动配置类上面，表示该自动配置类需要在另外指定的自动配置类配置完之后。
>
>如 Mybatis 的自动配置类，需要在数据源自动配置类之后。
>
>```text
>@AutoConfigureAfter(DataSourceAutoConfiguration.class)
>public class MybatisAutoConfiguration {
>```
>
>**23、@AutoConfigureBefore**
>
>这个和 `@AutoConfigureAfter` 注解使用相反，表示该自动配置类需要在另外指定的自动配置类配置之前。
>
>**24、@Import**
>
>这是 Spring 3.0 添加的新注解，用来导入一个或者多个 `@Configuration` 注解修饰的类，这在 Spring Boot 里面应用很多。
>
>**25、@ImportResource**
>
>这是 Spring 3.0 添加的新注解，用来导入一个或者多个 Spring 配置文件，这对 Spring Boot 兼容老项目非常有用，因为有些配置无法通过 Java Config 的形式来配置就只能用这个注解来导入。



## 设计模式

>- 1.简单工厂(非23种设计模式中的一种)
>- 2.工厂方法
>- 3.单例模式
>- 4.适配器模式
>- 5.装饰器模式
>- 6.代理模式
>- 7.观察者模式
>- 8.策略模式
>- 9.模版方法模式
>
>## 1.简单工厂(非23种设计模式中的一种)
>
>## 实现方式：
>
>BeanFactory。Spring中的BeanFactory就是简单工厂模式的体现，根据传入一个唯一的标识来获得Bean对象，但是否是在传入参数后创建还是传入参数前创建这个要根据具体情况来定。
>
>## 实质：
>
>由一个工厂类根据传入的参数，动态决定应该创建哪一个产品类。
>
>## 实现原理：
>
>**bean容器的启动阶段：**
>
>- 读取bean的xml配置文件,将bean元素分别转换成一个BeanDefinition对象。
>- 然后通过BeanDefinitionRegistry将这些bean注册到beanFactory中，保存在它的一个ConcurrentHashMap中。
>- 将BeanDefinition注册到了beanFactory之后，在这里Spring为我们提供了一个扩展的切口，允许我们通过实现接口BeanFactoryPostProcessor 在此处来插入我们定义的代码。典型的例子就是：PropertyPlaceholderConfigurer，我们一般在配置数据库的dataSource时使用到的占位符的值，就是它注入进去的。
>
>**容器中bean的实例化阶段：**
>
>实例化阶段主要是通过反射或者CGLIB对bean进行实例化，在这个阶段Spring又给我们暴露了很多的扩展点：
>
>- **各种的Aware接口** ，比如 BeanFactoryAware，对于实现了这些Aware接口的bean，在实例化bean时Spring会帮我们注入对应的BeanFactory的实例。
>- **BeanPostProcessor接口** ，实现了BeanPostProcessor接口的bean，在实例化bean时Spring会帮我们调用接口中的方法。
>- **InitializingBean接口** ，实现了InitializingBean接口的bean，在实例化bean时Spring会帮我们调用接口中的方法。
>- **DisposableBean接口** ，实现了BeanPostProcessor接口的bean，在该bean死亡时Spring会帮我们调用接口中的方法。
>
>## 设计意义：
>
>**松耦合。** 可以将原来硬编码的依赖，通过Spring这个beanFactory这个工厂来注入依赖，也就是说原来只有依赖方和被依赖方，现在我们引入了第三方——spring这个beanFactory，由它来解决bean之间的依赖问题，达到了松耦合的效果.
>
>**bean的额外处理。** 通过Spring接口的暴露，在实例化bean的阶段我们可以进行一些额外的处理，这些额外的处理只需要让bean实现对应的接口即可，那么spring就会在bean的生命周期调用我们实现的接口来处理该bean。[非常重要]
>
>## 2.工厂方法
>
>## 实现方式：
>
>FactoryBean接口。
>
>## 实现原理：
>
>实现了FactoryBean接口的bean是一类叫做factory的bean。其特点是，spring会在使用getBean()调用获得该bean时，会自动调用该bean的getObject()方法，所以返回的不是factory这个bean，而是这个bean.getOjbect()方法的返回值。
>
>### 例子：
>
>典型的例子有spring与mybatis的结合。
>
>**代码示例：**
>
>
>
>![img](https://pic3.zhimg.com/80/v2-57952d80301d013e42197b368bb4f062_1440w.jpg)
>
>
>
>**说明：**
>
>我们看上面该bean，因为实现了FactoryBean接口，所以返回的不是 SqlSessionFactoryBean 的实例，而是它的 SqlSessionFactoryBean.getObject() 的返回值。
>
>## 3.单例模式
>
>Spring依赖注入Bean实例默认是单例的。
>
>Spring的依赖注入（包括lazy-init方式）都是发生在AbstractBeanFactory的getBean里。getBean的doGetBean方法调用getSingleton进行bean的创建。
>
>分析getSingleton()方法
>
>```text
>public Object getSingleton(String beanName){
>    //参数true设置标识允许早期依赖
>    return getSingleton(beanName,true);
>}
>protected Object getSingleton(String beanName, boolean allowEarlyReference) {
>    //检查缓存中是否存在实例
>    Object singletonObject = this.singletonObjects.get(beanName);
>    if (singletonObject == null && isSingletonCurrentlyInCreation(beanName)) {
>        //如果为空，则锁定全局变量并进行处理。
>        synchronized (this.singletonObjects) {
>            //如果此bean正在加载，则不处理
>            singletonObject = this.earlySingletonObjects.get(beanName);
>            if (singletonObject == null && allowEarlyReference) {
>                //当某些方法需要提前初始化的时候则会调用addSingleFactory 方法将对应的ObjectFactory初始化策略存储在singletonFactories
>                ObjectFactory<?> singletonFactory = this.singletonFactories.get(beanName);
>                if (singletonFactory != null) {
>                    //调用预先设定的getObject方法
>                    singletonObject = singletonFactory.getObject();
>                    //记录在缓存中，earlysingletonObjects和singletonFactories互斥
>                    this.earlySingletonObjects.put(beanName, singletonObject);
>                    this.singletonFactories.remove(beanName);
>                }
>            }
>        }
>    }
>    return (singletonObject != NULL_OBJECT ? singletonObject : null);
>}
>```
>
>**getSingleton()过程图**
>
>ps：spring依赖注入时，使用了 双重判断加锁 的单例模式
>
>
>
>![img](https://pic2.zhimg.com/80/v2-6b4832167212c80bcde58e9ee747165d_1440w.jpg)
>
>
>
>**总结**
>
>**单例模式定义：** 保证一个类仅有一个实例，并提供一个访问它的全局访问点。
>
>**spring对单例的实现：** spring中的单例模式完成了后半句话，即提供了全局的访问点BeanFactory。但没有从构造器级别去控制单例，这是因为spring管理的是任意的java对象。
>
>## 4.适配器模式
>
>## 实现方式：
>
>SpringMVC中的适配器HandlerAdatper。
>
>## 实现原理：
>
>HandlerAdatper根据Handler规则执行不同的Handler。
>
>## 实现过程：
>
>DispatcherServlet根据HandlerMapping返回的handler，向HandlerAdatper发起请求，处理Handler。
>
>HandlerAdapter根据规则找到对应的Handler并让其执行，执行完毕后Handler会向HandlerAdapter返回一个ModelAndView，最后由HandlerAdapter向DispatchServelet返回一个ModelAndView。
>
>## 实现意义：
>
>HandlerAdatper使得Handler的扩展变得容易，只需要增加一个新的Handler和一个对应的HandlerAdapter即可。
>
>因此Spring定义了一个适配接口，使得每一种Controller有一种对应的适配器实现类，让适配器代替controller执行相应的方法。这样在扩展Controller时，只需要增加一个适配器类就完成了SpringMVC的扩展了。
>
>## 5.装饰器模式
>
>## 实现方式：
>
>Spring中用到的包装器模式在类名上有两种表现：一种是类名中含有Wrapper，另一种是类名中含有Decorator。
>
>## 实质：
>
>动态地给一个对象添加一些额外的职责。
>
>就增加功能来说，Decorator模式相比生成子类更为灵活。
>
>## 6.代理模式
>
>## 实现方式：
>
>AOP底层，就是动态代理模式的实现。
>
>## 动态代理：
>
>在内存中构建的，不需要手动编写代理类
>
>## 静态代理：
>
>需要手工编写代理类，代理类引用被代理对象。
>
>## 实现原理：
>
>切面在应用运行的时刻被织入。一般情况下，在织入切面时，AOP容器会为目标对象创建动态的创建一个代理对象。SpringAOP就是以这种方式织入切面的。
>
>织入：把切面应用到目标对象并创建新的代理对象的过程。
>
>## 7.观察者模式
>
>## 实现方式：
>
>spring的事件驱动模型使用的是 观察者模式 ，Spring中Observer模式常用的地方是listener的实现。
>
>## 具体实现：
>
>事件机制的实现需要三个部分,事件源,事件,事件监听器
>
>ApplicationEvent抽象类[事件]
>
>继承自jdk的EventObject,所有的事件都需要继承ApplicationEvent,并且通过构造器参数source得到事件源.
>
>该类的实现类ApplicationContextEvent表示ApplicaitonContext的容器事件.
>
>代码：
>
>```text
>publicabstractclass ApplicationEvent extends EventObject {
>    privatestaticfinallong serialVersionUID = 7099057708183571937L;
>    privatefinallong timestamp;
>    public ApplicationEvent(Object source) {
>    super(source);
>    this.timestamp = System.currentTimeMillis();
>    }
>    public final long getTimestamp() {
>        returnthis.timestamp;
>    }
>}
>```
>
>ApplicationListener接口[事件监听器]
>
>继承自jdk的EventListener,所有的监听器都要实现这个接口。
>
>这个接口只有一个onApplicationEvent()方法,该方法接受一个ApplicationEvent或其子类对象作为参数,在方法体中,可以通过不同对Event类的判断来进行相应的处理。
>
>当事件触发时所有的监听器都会收到消息。
>
>代码：
>
>```text
>publicinterface ApplicationListener<E extends ApplicationEvent> extends EventListener {
>     void onApplicationEvent(E event);
>}
>```
>
>ApplicationContext接口[事件源]
>
>ApplicationContext是spring中的全局容器，翻译过来是”应用上下文”。
>
>实现了ApplicationEventPublisher接口。
>
>## 职责：
>
>负责读取bean的配置文档,管理bean的加载,维护bean之间的依赖关系,可以说是负责bean的整个生命周期,再通俗一点就是我们平时所说的IOC容器。
>
>代码：
>
>```text
>publicinterface ApplicationEventPublisher {
>        void publishEvent(ApplicationEvent event);
>}
>
>public void publishEvent(ApplicationEvent event) {
>    Assert.notNull(event, "Event must not be null");
>    if (logger.isTraceEnabled()) {
>         logger.trace("Publishing event in " + getDisplayName() + ": " + event);
>    }
>    getApplicationEventMulticaster().multicastEvent(event);
>    if (this.parent != null) {
>    this.parent.publishEvent(event);
>    }
>}
>```
>
>ApplicationEventMulticaster抽象类[事件源中publishEvent方法需要调用其方法getApplicationEventMulticaster]
>
>属于事件广播器,它的作用是把Applicationcontext发布的Event广播给所有的监听器.
>
>代码：
>
>```text
>publicabstractclass AbstractApplicationContext extends DefaultResourceLoader
>    implements ConfigurableApplicationContext, DisposableBean {
>    private ApplicationEventMulticaster applicationEventMulticaster;
>    protected void registerListeners() {
>    // Register statically specified listeners first.
>    for (ApplicationListener<?> listener : getApplicationListeners()) {
>    getApplicationEventMulticaster().addApplicationListener(listener);
>    }
>    // Do not initialize FactoryBeans here: We need to leave all regular beans
>    // uninitialized to let post-processors apply to them!
>    String[] listenerBeanNames = getBeanNamesForType(ApplicationListener.class, true, false);
>    for (String lisName : listenerBeanNames) {
>    getApplicationEventMulticaster().addApplicationListenerBean(lisName);
>    }
>  }
>}
>```
>
>## 8.策略模式
>
>## 实现方式：
>
>Spring框架的资源访问Resource接口。该接口提供了更强的资源访问能力，Spring 框架本身大量使用了 Resource 接口来访问底层资源。
>
>## Resource 接口介绍
>
>source 接口是具体资源访问策略的抽象，也是所有资源访问类所实现的接口。
>
>Resource 接口主要提供了如下几个方法:
>
>- **getInputStream()：** 定位并打开资源，返回资源对应的输入流。每次调用都返回新的输入流。调用者必须负责关闭输入流。
>- **exists()：** 返回 Resource 所指向的资源是否存在。
>- **isOpen()：** 返回资源文件是否打开，如果资源文件不能多次读取，每次读取结束应该显式关闭，以防止资源泄漏。
>- **getDescription()：** 返回资源的描述信息，通常用于资源处理出错时输出该信息，通常是全限定文件名或实际 URL。
>- **getFile：** 返回资源对应的 File 对象。
>- **getURL：** 返回资源对应的 URL 对象。
>
>最后两个方法通常无须使用，仅在通过简单方式访问无法实现时，Resource 提供传统的资源访问的功能。
>
>Resource 接口本身没有提供访问任何底层资源的实现逻辑，**针对不同的底层资源，Spring 将会提供不同的 Resource 实现类，不同的实现类负责不同的资源访问逻辑。**
>
>Spring 为 Resource 接口提供了如下实现类：
>
>- **UrlResource：** 访问网络资源的实现类。
>- **ClassPathResource：** 访问类加载路径里资源的实现类。
>- **FileSystemResource：** 访问文件系统里资源的实现类。
>- **ServletContextResource：** 访问相对于 ServletContext 路径里的资源的实现类.
>- **InputStreamResource：** 访问输入流资源的实现类。
>- **ByteArrayResource：** 访问字节数组资源的实现类。
>
>这些 Resource 实现类，针对不同的的底层资源，提供了相应的资源访问逻辑，并提供便捷的包装，以利于客户端程序的资源访问。
>
>## 9.模版方法模式
>
>## 经典模板方法定义：
>
>父类定义了骨架（调用哪些方法及顺序），某些特定方法由子类实现。
>
>最大的好处：代码复用，减少重复代码。除了子类要实现的特定方法，其他方法及方法调用顺序都在父类中预先写好了。
>
>**所以父类模板方法中有两类方法：**
>
>**共同的方法：** 所有子类都会用到的代码
>
>**不同的方法：** 子类要覆盖的方法，分为两种：
>
>- 抽象方法：父类中的是抽象方法，子类必须覆盖
>- 钩子方法：父类中是一个空方法，子类继承了默认也是空的
>
>注：为什么叫钩子，子类可以通过这个钩子（方法），控制父类，因为这个钩子实际是父类的方法（空方法）！
>
>## Spring模板方法模式实质：
>
>是模板方法模式和回调模式的结合，是Template Method不需要继承的另一种实现方式。Spring几乎所有的外接扩展都采用这种模式。
>
>## 具体实现：
>
>JDBC的抽象和对Hibernate的集成，都采用了一种理念或者处理方式，那就是模板方法模式与相应的Callback接口相结合。
>
>采用模板方法模式是为了以一种统一而集中的方式来处理资源的获取和释放，以JdbcTempalte为例:
>
>```text
>publicabstractclass JdbcTemplate {
>     publicfinal Object execute（String sql）{
>        Connection con=null;
>        Statement stmt=null;
>        try{
>            con=getConnection（）;
>            stmt=con.createStatement（）;
>            Object retValue=executeWithStatement（stmt,sql）;
>            return retValue;
>        }catch（SQLException e）{
>             ...
>        }finally{
>            closeStatement（stmt）;
>            releaseConnection（con）;
>        }
>    }
>    protectedabstract Object executeWithStatement（Statement   stmt, String sql）;
>}
>```
>
>## 引入回调原因：
>
>JdbcTemplate是抽象类，不能够独立使用，我们每次进行数据访问的时候都要给出一个相应的子类实现,这样肯定不方便，所以就引入了回调。
>
>回调代码
>
>```text
>publicinterface StatementCallback{
>    Object doWithStatement（Statement stmt）;
>}
>```
>
>利用回调方法重写JdbcTemplate方法
>
>```text
>publicclass JdbcTemplate {
>    publicfinal Object execute（StatementCallback callback）{
>        Connection con=null;
>        Statement stmt=null;
>        try{
>            con=getConnection（）;
>            stmt=con.createStatement（）;
>            Object retValue=callback.doWithStatement（stmt）;
>            return retValue;
>        }catch（SQLException e）{
>            ...
>        }finally{
>            closeStatement（stmt）;
>            releaseConnection（con）;
>        }
>    }
>
>    ...//其它方法定义
>}
>```
>
>Jdbc使用方法如下：
>
>```text
>JdbcTemplate jdbcTemplate=...;
>    final String sql=...;
>    StatementCallback callback=new StatementCallback(){
>    public Object=doWithStatement(Statement stmt){
>        return ...;
>    }
>}
>jdbcTemplate.execute(callback);
>```



# ==SpringBoot 自动装配==

>1.  首先就是重注解说起 然后就是按照如下图进行说呗 

>![image-20210731123214767](/Users/whig/Library/Application Support/typora-user-images/image-20210731123214767.png)



# springmvc

>![img](https://user-gold-cdn.xitu.io/2020/2/9/17027be056d14499?imageslim)
>
>- 用户发送出请求到前端控制器DispatcherServlet。
>
> DispatcherServlet收到请求调用HandlerMapping（处理器映射器）。
>
> HandlerMapping找到具体的处理器(可查找xml配置或注解配置)，生成处理器对象及处理器拦截器(如果有)，再一起返回给DispatcherServlet。
>
> DispatcherServlet调用HandlerAdapter（处理器适配器）。
>
> HandlerAdapter经过适配调用具体的处理器（Handler/Controller）。
>
> Controller执行完成返回ModelAndView对象。
>
> HandlerAdapter将Controller执行结果ModelAndView返回给DispatcherServlet。
>
>
>
>- 关键组件分析
>
>DispatcherServlet将ModelAndView传给ViewReslover（视图解析器）。
>
>ViewReslover解析后返回具体View（视图）。
>
>DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。
>
>DispatcherServlet响应用户。
>
>前端控制器：DispatcherServlet（不需要程序员开发）,由框架提供，在web.xml中配置。 作用：接收请求，响应结果，相当于转发器，中央处理器。
>
>处理器映射器：HandlerMapping(不需要程序员开发),由框架提供。 作用：根据请求的url查找Handler(处理器/Controller)，可以通过XML和注解方式来映射。
>
>处理器适配器：HandlerAdapter(不需要程序员开发),由框架提供。 作用：按照特定规则（HandlerAdapter要求的规则）去执行Handler。
>
>处理器：**Handler(也称之为Controller，需要工程师开发)**。 注意：编写Handler时按照HandlerAdapter的要求去做，这样适配器才可以去正确执行Handler。 作用：接受用户请求信息，调用业务方法处理请求，也称之为后端控制器。
>
>视图解析器：ViewResolver(不需要程序员开发)，由框架提供。 作用：进行视图解析，把逻辑视图名解析成真正的物理视图。





# ==---------------------------------------------------------------------Mybatis==

 ##  Mybatis防止sql注入 #{}

>#{}是占位符，预编译处理；${}是拼接符，字符串替换，没有预编译处理。
>
>Mybatis在处理#{}时，#{}传入参数是以字符串传入，会将SQL中的#{}替换为?号，调用PreparedStatement的set方法来赋值。
>
>Mybatis在处理时 ， 是 原 值 传 入 ， 就 是 把 {}时，是原值传入，就是把时，是原值传入，就是把{}替换成变量的值，相当于JDBC中的Statement编译
>
>变量替换后，#{} 对应的变量自动加上单引号 ‘’；变量替换后，${} 对应的变量不会加上单引号 ‘’
>
>#{} 可以有效的防止SQL注入，提高系统安全性；${} 不能防止SQL 注入
>
>#{} 的变量替换是在DBMS 中；${} 的变量替换是在 DBMS 外
>
>

## Mybatis分页  limit

>1、基本语法
>
>```
>SELECT * FROM table LIMIT stratIndex，pageSize
>#列子#<1>检索记录为1到10行数据，下标是从0开始的select * from user limit 0,10;#<2>limit 只给一个参数表示从0开始到参数值的记录数，下面的语句相当于limit 0,5select * from user limit 5;
>```
>
>复制代码
>
>2、添加接口方法
>
>```
>//实现分页操作List<User> getUserList1(Map<String,Object> map);
>```
>
>复制代码
>
>3、添加 UserMapper.xml。通过 map 将其实记录数和每页显示条数传进去
>
>```
><select id="getUserList1" parameterType="map" resultMap="resultmap">        select * from user limit #{startindex},#{pagesize}</select>
>```
>
>复制代码
>
>3、添加测试
>
>```
> @Test    public void testGetUserList(){        SqlSession sqlSession = MysqlUtil.getSqlSession();        UserMapper mapper = sqlSession.getMapper(UserMapper.class);        Map<String, Object> map = new HashMap<String, Object>();        map.put("startindex",0);        map.put("pagesize",2);        List<User> userList1 = mapper.getUserList1(map);        for(User user:userList1){            System.out.println(user);        }    }
>```
>
>复制代码
>
>4、查看测试结果，返回 1、2 两条记录
>
>```
>User{id=1, name='张三', password='322334'}User{id=2, name='李四', password='123456'}
>```
>
>复制代码
>
>
>
>## RowBounds 实现分页
>
>1、添加 mapper 接口
>
>```
>//通过RowBounds 方法实现分页    List<User> getUserListByRowBounds();
>```
>
>复制代码
>
>2、UserMapper.xml 配置文件
>
>```
> <select id="getUserListByRowBounds" resultType="user" resultMap="resultmap">        select * from user;    </select>
>```
>
>复制代码
>
>3、添加测试方法
>
>```
>  @Test    public void getUserByRowBounds(){        SqlSession sqlSession = MysqlUtil.getSqlSession();                int currPage =1; //当前页        int pageSize = 2; //每页大小        RowBounds rowBounds = new RowBounds((currPage-1)*pageSize,pageSize);        ////通过session.**方法进行传递rowBounds，[此种方式现在已经不推荐使用了]        List<User> userList = sqlSession.selectList("com.xiezhr.dao.UserMapper.getUserListByRowBounds", null, rowBounds);        for(User user:userList){            System.out.println(user);        }        sqlSession.close();
>```





## 缓存特性

>**一级缓存**
>
>
>一级缓存是SqlSession级别的缓存。在操作数据库时需要构造 sqlSession对象，在对象中有一个(内存区域)数据结构（HashMap）用于存储缓存数据。不同的sqlSession之间的缓存数据区域（HashMap）是互相不影响的。
>
>一级缓存的作用域是同一个SqlSession，在同一个sqlSession中两次执行相同的sql语句，第一次执行完毕会将数据库中查询的数据写到缓存（内存），第二次会从缓存中获取数据将不再从数据库查询，从而提高查询效率。当一个sqlSession结束后该sqlSession中的一级缓存也就不存在了。Mybatis默认开启一级缓存。
>
>一级缓存只是相对于同一个SqlSession而言。所以在参数和SQL完全一样的情况下，我们使用同一个SqlSession对象调用一个Mapper方法，往往只执行一次SQL，因为使用SelSession第一次查询后，MyBatis会将其放在缓存中，以后再查询的时候，如果没有声明需要刷新，并且缓存没有超时的情况下，SqlSession都会取出当前缓存的数据，而不会再次发送SQL到数据库。
>
>1、一级缓存的生命周期有多长？
>　　a、MyBatis在开启一个数据库会话时，会 创建一个新的SqlSession对象，SqlSession对象中会有一个新的Executor对象。Executor对象中持有一个新的PerpetualCache对象；当会话结束时，SqlSession对象及其内部的Executor对象还有PerpetualCache对象也一并释放掉。
>
>　　b、如果SqlSession调用了close()方法，会释放掉一级缓存PerpetualCache对象，一级缓存将不可用。
>
>　　c、如果SqlSession调用了clearCache()，会清空PerpetualCache对象中的数据，但是该对象仍可使用。
>
>　　d、SqlSession中执行了任何一个update操作(update()、delete()、insert()) ，都会清空PerpetualCache对象的数据，但是该对象可以继续使用
>
> 2、怎么判断某两次查询是完全相同的查询？
>　　mybatis认为，对于两次查询，如果以下条件都完全一样，那么就认为它们是完全相同的两次查询。
>
>　　2.1 传入的statementId
>
>　　2.2 查询时要求的结果集中的结果范围
>
>　　2.3. 这次查询所产生的最终要传递给JDBC java.sql.Preparedstatement的Sql语句字符串（boundSql.getSql() ）
>
>　　2.4 传递给java.sql.Statement要设置的参数值
>
> 
>
>**二级缓存**
>MyBatis的二级缓存是Application级别的缓存，它可以提高对数据库查询的效率，以提高应用的性能。
>
>　　MyBatis的缓存机制整体设计以及二级缓存的工作模式
>
>
>
>二级缓存是mapper级别的缓存，多个SqlSession去操作同一个Mapper的sql语句，多个SqlSession去操作数据库得到数据会存在二级缓存区域，多个SqlSession可以共用二级缓存，二级缓存是跨SqlSession的。
>
>    二级缓存是多个SqlSession共享的，其作用域是mapper的同一个namespace，不同的sqlSession两次执行相同namespace下的sql语句且向sql中传递参数也相同即最终执行相同的sql语句，第一次执行完毕会将数据库中查询的数据写到缓存（内存），第二次会从缓存中获取数据将不再从数据库查询，从而提高查询效率。Mybatis默认没有开启二级缓存需要在setting全局参数中配置开启二级缓存。
>
>sqlSessionFactory层面上的二级缓存默认是不开启的，二级缓存的开启需要进行配置，实现二级缓存的时候，MyBatis要求返回的POJO必须是可序列化的。 也就是要求实现Serializable接口，配置方法很简单，只需要在映射XML文件配置就可以开启缓存了<cache/>，如果我们配置了二级缓存就意味着：
>
>映射语句文件中的所有select语句将会被缓存。
>映射语句文件中的所欲insert、update和delete语句会刷新缓存。
>缓存会使用默认的Least Recently Used（LRU，最近最少使用的）算法来收回。
>根据时间表，比如No Flush Interval,（CNFI没有刷新间隔），缓存不会以任何时间顺序来刷新。
>缓存会存储列表集合或对象(无论查询方法返回什么)的1024个引用
>缓存会被视为是read/write(可读/可写)的缓存，意味着对象检索不是共享的，而且可以安全的被调用者修改，不干扰其他调用者或线程所做的潜在修改。
>如果缓存中有数据就不用从数据库中获取，大大提高系统性能。

## Mybatis都有哪些Executor执行器？它们之间的区别是什么？
>Mybatis有三种基本的Executor执行器，SimpleExecutor、ReuseExecutor、BatchExecutor。
>
>SimpleExecutor：每执行一次update或select，就开启一个Statement对象，用完立刻关闭Statement对象。
>
>ReuseExecutor：执行update或select，以sql作为key查找Statement对象，存在就使用，不存在就创建，用完后，不关闭Statement对象，而是放置于Map<String, Statement>内，供下一次使用。简言之，就是重复使用Statement对象。
>
>BatchExecutor：执行update（没有select，JDBC批处理不支持select），将所有sql都添加到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。与JDBC批处理相同。
>
>作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内



