
<!-- vim-markdown-toc GFM -->

- [Spring 的优势](#spring-的优势)
- [Spring IOC](#spring-ioc)
- [Spring AOP 简介](#spring-aop-简介)
- [Spring 注解](#spring-注解)
- [SpringMVC 参数传递常用注解](#springmvc-参数传递常用注解)
- [配置大体流程](#配置大体流程)

<!-- vim-markdown-toc -->


### Spring 的优势
- 低侵入 / 低耦合 （降低组件之间的耦合度，实现软件各层之间的解耦）

- 面向切面编程能帮助我们无耦合的实现日志记录，性能统计，安全控制。

- 声明式事务管理（基于切面和惯例）

- Spring 框架中包括了 J2EE 三层的每一层的解决方案（一站式）

- 方便集成其他框架（如MyBatis、Hibernate）


### Spring IOC
> Invertion of controll 控制反转

- 打个比方，原来做个红烧肉，我需要自己去买肉，准备佐料，自己加工，现在我只要外包给Spring，告诉它需要
  什么肉，怎么做，然后后面的事就外包给它，当吃的时候直接拿就行。

- 反转了什么？
  IOC运用Java反射进行依赖注入，将Bean的生成从原来的编译期推迟到运行期，从程序员主动new出Bean变成从容器中动态注入Bean，
  减少了重复代码，并使获得依赖对象的整个过程反转。

- 为什么能够解耦
  另一方面IOC容器相当于一个处理复杂依赖关系的中介，Bean的定义、生成、初始化、后处理、销毁等等控制过程全部交给容器，
  降低了程序员直接操作对象的难度。
  需要Bean的各个模块只与接口或者容器耦合，从而降低了系统之间的耦合，方便代码的维护。

- IOC容器就是一个加强版的工厂模式，只不过用配置文件中的定义借助反射来生成对象。

- 缺点：
  - 对象生成多出一道手续，不直观
  - 运行反射运行时动态生成，效率有一定下降。
  - 需要大量前期配置，SpringBoot已经解决。


### Spring AOP 简介
- AOP 即 Aspect Oriented Program 面向切面编程。它把系统功能分为核心业务和周边功能。
  周边功能在 Spring 的面向切面编程AOP思想里，被定义为切面。
  将与业务无关，却被业务模块共同调用的功能代码（例如事务处理、日志管理、权限控制、缓存处理等）封装起来，
  能减少重复代码，降低模块间耦合，并有利于未来的可拓展性和可维护性。

- 在AOP思想里，核心业务功能和切面功能分别独立进行开发，然后把切面功能和核心业务功能 "编织" 在一起。

- AOP 的目的
  - 解决代码复用及关注点分离问题
  - oop的补充

- AOP 当中的概念：
  - 切入点（Pointcut） 在哪些类，哪些方法上切入，委托类－被代理的类（where）
  - 通知（Advice） 在方法执行的什么时间（when:方法前/方法后/方法前后）做什么（what:增强的功能）
  - 切面（Aspect） 切面 = 切入点 + 通知，通俗点就是：在什么时机，什么地方，做什么增强。 代理类。
  - 织入（Weaving） 把切面加入到对象，并创建出代理对象的过程。（由 Spring 来完成）

- 实现方式：
  - Spring AOP 与 AspectJ 的关系，Spring用了AspectJ的注解，但是自己用JDK动态代理实现的。
    AspectJ需要另外的编译器，是编译期字节码增强的静态代理。

  - 动态代理：JDK动态代理，Cglib动态字节码生成

  - [静态代理和动态代理](../6.工程实践/设计模式/静态代理和动态代理.md)


### Spring 注解
- @Component表示这是一个需要Spring来管理的容器组件。
  component-scan 默认扫描的注解类型是@Component，但是在@Component语义基础上细化的@Repository，@Service，
  @Controller也同样会被扫描。



### SpringMVC 参数传递常用注解
根据处理Request不同内容分为四类：

- 处理requet uri 部分（指uri template中variable，不含queryString部分）的注解： @PathVariable;

- 处理request header部分的注解： @RequestHeader, @CookieValue;
  - @RequestHeader 注解，可以把Request请求header部分的值绑定到方法的参数上。
  - @CookieValue 可以把Request header中关于cookie的值绑定到方法的参数上。

- 处理request body部分的注解：@RequestParam, @RequestBody;
  - @RequestParam 可以处理GET提交中queryString的值。
  - 两个都可以用来处理POST提交Content-Type: 为 application/x-www-form-urlencoded编码的内容。
  - @RequestParam 不能处理复杂类型application/json，application/xml，必须是@RequestBody。

- 处理attribute类型是注解： @SessionAttributes, @ModelAttribute;
  - @ModelAttribute 用在方法上，该Controller处理其他方法前会先调用被绑定的方法，相当于一个公共方法，
    可写在一个BaseController中。为请求绑定需要从后台查询的model。

  - @ModelAttribute 用在参数上，把之前绑定的相应名称的值注入到被注解的参数上。之前绑定的值来源于：
    - @SessionAttributes 启用的attribute对象上。
    - @ModelAttribute 用于方法上时指定的model对象。
    - 假定@ModelAtribute 用在参数Pet上时，首先会查询 @SessionAttributes有无绑定的Pet对象，若没有则查询
      @ModelAttribute方法层面上是否绑定了Pet对象，若没有则将URI template中的路径参数值按对应的名称绑定
      到Pet对象的各属性上，从而构成一个Pet对象。


### 配置大体流程
- 项目依赖，解决依赖

- web.xml
  配置编码过滤器

- spring-mybatis.mxl
  - service包 bean扫描
  - 数据库连接池 Bean注入
  - SqlSessionFactory Bean注入连接池，pojo，mapper包，分页插件
  - DAO接口 Bean注入
  - 事务管理器 Bean注入

- spring-mvc.mxl
  - 配置控制器 组件扫描
  - 视图解析器－JSP或模板引擎

- properties数据库连接池属性配置

- logback.xml日志输出配置

- 实体类，DAO接口设计，对应的mybatis `mapper.xml`配置 SQL语句设计

- 业务类Service层设计，接口及实现类

- 控制层开发


