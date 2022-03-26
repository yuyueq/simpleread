
# 前言

这块还是比较关键的，考察你对整个业务流程的熟练度吧，虽然企业级的项目没有接触过，但像最基本的内容必须得融会贯通，这一点我感觉自己还是处于浅层，没有深入的去思考以及练习过，其实就像那句话，“打字速度不够，说明你敲的代码不够多”，其实有时候最原始的方法是最简单有效的，虽然会耗大量时间，但一件事有利就有弊，所以还是加强自身代码熟练度。
还是那句话，**如果文中有明显错误，劳烦请及时纠正我，在这不胜感激！！！**

------

# 一、JavaWeb

## 1.解释一下Servlet以及生命周期？

答：servlet就是sun公司开发动态web程序的一门技术，通过前端请求，服务器端进行逻辑判断，完成对前端的响应；生命周期大致可分为三个阶段，初始化阶段、运行阶段、销毁阶段；首先初始化阶段会调用init()方法对servlet对象的初始化，二是通过调用service方法来处理和响应客户端的请求，三是通过调用destroy方法表示服务器资源已经被移除。而我们一般是通过继承HttPServlet这个抽象类，因为这个类对servlet默认方法有实现而且也添加自己的方法，然后平时用的较多的就是doPost和doGet方法。

## 2.Cookie和Session有什么区别以及工作原理？

答：首先Http协议是无状态的，所以服务器端需要确认用户状态时，就得有某种机制去记录；cookie是提供给客户端的技术，session是提供给服务器端的技术；客户端第一次请求服务器端时，服务器端会产生一个session对象，来用于保存客户信息，并且每个session都有唯一的sessionID与之对应，用来区分session，然后服务器端会产生一个cookie，此时cookie中name=JSESSIONID参数，然后value值是和sessionID的值是一样的，当服务器端响应给客户端的同时，将cookie发送给客户端，然后客户端就有一个JSESSIONID与服务器端sessionID一一对应。当第二次请求时，服务器端会先用客户端的JSESSIONID去匹配session中的sessionID。cookie保存的内容较为不安全，内容是String类型的，而session中保存在服务器这块，较为安全，内容是object类型的。一般是浏览器关了后cookie就过期了，当然这也跟设置过期时间有关。

## 4.谈一下SQL注入

答：就是对用户输入的数据没有进行合法性没有判断，也没有过滤，然后攻击者可以通过特殊的字符提交，改变SQL运行的结果，实现非法操作。基本上后端都是用预编译PreparedStatement对象，或者增加正则表达式来防止SQL注入。目前了解就这么多。

## 5.说一下XSS攻击

答：跨站脚本攻击，不需要用户去登录认证，然后通过合法操作在页面中注入脚本，然后操控用户浏览器，类似SQL注入。

## 6.CSRF攻击是什么？如何避免?

答：跨站请求伪造攻击，诱使用户登录认证第三方网站，然后通过用户认证凭证绕过后台验证，然后冒充用户从而去达到某项操作的目的。比如盗取账号、转账、发布虚假信息。验证码和token都是比较用的多的防范措施。

## 7.doGet和doPost有什么区别？

答：两种方式主要针对get和post方法，而get一般用来获取数据，因为它请求的数据会附加在URL上，而且get参数有长度限制，get请求还会保存在浏览器记录中，而post方式更适合提交数据，相比get方式更加安全，因为它是将header先发过去，然后通过服务器判断再发送data，而且它也是放在请求体中的，虽然通过抓包可以看见，但至少比get明文传输的稍微安全一些。且post参数大小是无限制。

------



## [提一些需要知道的JSP知识，个人感觉这一方面的知识还是要懂的]

## JSP与Servlet的区别？

答：JSP本质上就是Servlet，JSP首先通过翻译成servlet，然后再将servlet编译成“.class”文件，然后其中java代码在服务器端执行，最终通过out.write()方法将HTML内容发送到浏览器进行解析。
![image](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20210802195508783-254698916.png)

## JSP内置对象

答：九大内置对象，1是request封装客户端请求，2是response封装服务器端请求，3是pageContext通过该对象可以获得其他对象，4是session封装用户会话的对象，5是application封装服务器端运行环境的对象，6是page JSP本身对象，7是config web应用配置对象，8是out 输出服务器端响应的输出流对象，9是exception封装页面抛出异常的对象。

## JSP作用域

答：四种作用域；page表示一个页面相关的对象和属性；request表示客户端向服务器发出的请求，产生的数据，临时性的，常见于新闻这类型；session表示一次会话，就是发送请求后，产生的数据，一会还有用。比如购物车；application表示发送的请求，产生的数据，一个用户用完别的用户还能继续用，全局作用域。


------

# 二、JavaEE

## I.Spring

### 1.说一下IOC

答：IOC就是控制反转，控制就是传统的是由程序本身创建对象，现在交给spring容器去创建，反转就是程序不去创建对象而是去被动的接收对象；而具体的一种实现方式就是依赖注入，注入方式的话就有构造器注入（默认无参构造，有参通过下标、参数名、类型赋值）和setter方式注入、注解方式注入；而依赖就是bean对象的创建是由容器完成的，注入就是bean对象中的属性都由容器来注入。最终还是为了解耦合。

**参考文章**：《Spring：源码解读Spring IOC原理》https://www.cnblogs.com/ITtangtang/p/3978349.html

### 2.说一下AOP

答：理解AOP的话，就得首先对Java的代理模式有认识；代理模式的话可以去看一下这个狂神的视频【https://www.bilibili.com/video/BV1WE411d7Dv?p=17】
AOP面向切面编程，简单说就是那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块之间的耦合度，并有利于未来的可操作性和可维护性

**参考文章**：《Spring3：AOP》 https://www.cnblogs.com/xrq730/p/4919025.html

### 3.Bean的作用域

答：官方文档作用域有六种，一是单例模式也就是单个bean定义范围只有单个实例，二是原型模式，每次从容器中get时，就会产生新的实例，剩下的request（一次请求中存活）、session（一个session会话中存活）、application（全局存活）、websocket都在web中用到。

### 4.Bean的自动装配

答：两种装配，一是xml中的显式配置、java中的显式配置、二是隐式自动装配bean（一种是byName会自动在容器上下文中找和自己对象set方法后面值对应的bean id，即需要保证所有的bean的id唯一；一种是byType会在容器上下文中找，和自己对象属性类型相同的bean，即需要保证所有bean的class唯一）；

------

## II.SpringMVC



### 1.说一下SpringMVC的流程？

答：首先URL请求会发送到前端控制器DispatcherServlet，然后DispatcherServlet寻找HandlerMapping处理器映射，通过HandlerExcution根据URL寻找处理器Handler，然后将信息返回给DispatchServlet前端控制器，然后前端控制器去请求处理器适配器HandlerAdapter，该适配器通过给Controller去执行Handler，最后将视图逻辑名或模型数据返回给前端控制器，然后前端控制器去调用视图解析器去解析逻辑视图名，然后将信息返回给前端控制器，前端控制器再去调用具体视图。
参考以下两图：
![image](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20210802195440046-754646628.png)
![image](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20210802195431749-1448041306.png)

------

## III.MyBatis

### 1.谈一下你对MyBatis的理解？

答：MyBatis就是简化了数据库连接和操作，通过xml文件或注解来映射原生类型，接口和简单的实体类，而且没有第三方的依赖。因为以前JDBC的话，在Java中操作数据库，首先要加载驱动，配置一些连接参数，而且数据返回结果需要一个个遍历赋值给我们写的POJO，当需要变更一些驱动信息时，会消耗很大一部分时间，而且都是重复性的工作，所以MyBatis的话就简化了开发，松解了耦合。 

### 2. #{} 与 ${} 的区别

答：#号是可以防止SQL注入问题，因为是预编译的，相当于jdbc中占位符“？”；$符号是直接替换的值，不安全的。能用#{}尽量用#{}。

### 3.MyBatis和MyBatis-Plus有什么区别？

答：相对于Mybatis的话，以前需要每写一个DAO就要有一个Mapper去对应操作数据库，而Mybatis-Plus对mybatis做了增强，也就是将平时一些常用的CRUD操作数据库语句做了封装，简化了一些重复性的操作。

### 4.MyBatis的一级缓存和二级缓存是怎样的？

答：默认情况下，一级缓存开启，也就是SQLSession级别的缓存，本地缓存；二级缓存基于namespace级别的缓存，需要手动开启，而且MyBatis为了提高扩展性，在其中定义了cache接口，通过接口去实现二级缓存。


------

## IV.SpringBoot

### 1.SpringBoot与普通的SpringMVC开发的区别？

答：SpringMVC是基于servlet的一个MVC框架主要解决WEB开发的问题，通过xml配置统一开发前端视图和后端逻辑，提供一种轻度耦合的方式来开发web应用；SpringBoot专注于微服务方面的接口开发，和前端解耦，同时也解决了Spring配置的复杂，简化了SpringMVC的开发流程；从而提供一种与Spring框架紧密结合用于提升开发者体验的工具，同时它也集成了大量的第三方库配置。
**具体的理解可自行网上搜索文章查阅，还是感觉只有在项目中才能更加的去理解这一部分的知识，所以平时还是要多做一些demo来梳理自己的对开发技术的理解**

### 2.SpringBoot的核心注解有哪些？

答：目前是知道@SpringBootApplication复合注解，因为它包含了SpringBootConfiguration（标注当前类是配置类）、EnableAutoConfiguration（根据我们添加的jar组件来完成默认配置，比如mvc的配置和tomcat）、ComponentScan（扫描当前包以及子包中被Component、Controller、Service、Repository注解标记的类并纳入Spring容器进行管理）；@Controller表示这个类是个控制类，@RequestMapping一般是使用Rest风格，比如@GetMapping、@PostMapping等等；@CrossOrigin解决跨域访问问题；@AutoWired是Spring的自动装配；（**_其实像后面的这些注解都是Spring和SpringMVC中的，严格意义上来讲我觉得也不算SpringBoot的，只有像第一个复合注解才是比较核心的，目前也是了解这么多，还需后期不断深入的学习理解_**）

### 3.SpringBoot的自动装配原理是怎样的？

答：这个点我感觉自己把握也不是很好，所以找了点一些内容
**狂神笔记内容：**

```
//表示这是一个配置类，和以前编写的配置文件一样，也可以给容器中添加组件；
@Configuration 

//启动指定类的ConfigurationProperties功能；
  //进入这个HttpProperties查看，将配置文件中对应的值和HttpProperties绑定起来；
  //并把HttpProperties加入到ioc容器中
@EnableConfigurationProperties({HttpProperties.class}) 

//Spring底层@Conditional注解
  //根据不同的条件判断，如果满足指定的条件，整个配置类里面的配置就会生效；
  //这里的意思就是判断当前应用是否是web应用，如果是，当前配置类生效
@ConditionalOnWebApplication(
    type = Type.SERVLET
)

//判断当前项目有没有这个类CharacterEncodingFilter；SpringMVC中进行乱码解决的过滤器；
@ConditionalOnClass({CharacterEncodingFilter.class})

//判断配置文件中是否存在某个配置：spring.http.encoding.enabled；
  //如果不存在，判断也是成立的
  //即使我们配置文件中不配置pring.http.encoding.enabled=true，也是默认生效的；
@ConditionalOnProperty(
    prefix = "spring.http.encoding",
    value = {"enabled"},
    matchIfMissing = true
)

public class HttpEncodingAutoConfiguration {
    //他已经和SpringBoot的配置文件映射了
    private final Encoding properties;
    //只有一个有参构造器的情况下，参数的值就会从容器中拿
    public HttpEncodingAutoConfiguration(HttpProperties properties) {
        this.properties = properties.getEncoding();
    }
    
    //给容器中添加一个组件，这个组件的某些值需要从properties中获取
    @Bean
    @ConditionalOnMissingBean //判断容器没有这个组件？
    public CharacterEncodingFilter characterEncodingFilter() {
        CharacterEncodingFilter filter = new OrderedCharacterEncodingFilter();
        filter.setEncoding(this.properties.getCharset().name());
        filter.setForceRequestEncoding(this.properties.shouldForce(org.springframework.boot.autoconfigure.http.HttpProperties.Encoding.Type.REQUEST));
        filter.setForceResponseEncoding(this.properties.shouldForce(org.springframework.boot.autoconfigure.http.HttpProperties.Encoding.Type.RESPONSE));
        return filter;
    }
    //。。。。。。。
}



 一句话总结 ：根据当前不同的条件判断，决定这个配置类是否生效！
 一但这个配置类生效；这个配置类就会给容器中添加各种组件； 
 
 这些组件的属性是从对应的 properties 类中获取的，这些类里面的每一个属性又是和配置文件绑定的； 
 所有在配置文件中能配置的属性都是在 xxxxProperties 类中封装着； 
 配置文件能配置什么就可以参照某个功能对应的这个属性类 


//从配置文件中获取指定的值和bean的属性进行绑定
@ConfigurationProperties(prefix = "spring.http") 
public class HttpProperties {
    // .....
}



精髓

1、SpringBoot 启动会加载大量的自动配置类

2、我们看我们需要的功能有没有在 SpringBoot 默认写好的自动配置类当中；

3、我们再来看这个自动配置类中到底配置了哪些组件；（只要我们要用的组件存在在其中，我们就不需要再手动配置了）

4、给容器中自动配置类添加组件的时候，会从 properties 类中获取某些属性。我们只需要在配置文件中指定这些属性的值即可；

xxxxAutoConfigurartion：自动配置类；给容器中添加组件

xxxxProperties: 封装配置文件中相关属性；

```

**参考文章**：

[这样讲 SpringBoot 自动配置原理，你应该能明白了吧](https://juejin.cn/post/6844903849178873870)

[SpringBoot自动配置原理](https://www.cnblogs.com/wuzhenzhao/p/9151673.html)

**本人无打广告嫌疑**！！！！

------

# 三、JVM

## 1.说说JVM内存结构？

答：ProcessOn上找的一张图，看标注应该是尚硅谷的图，感觉这个图还是能初步认识JVM。

![image](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20210802195342905-975321220.png)

还有三张图链接放这，自行查看，感觉还是解释的比较全面。

**_JVM内存模型完整版【_**[https://www.processon.com/view/5ea7a1b9e401fd21c196eb17?fromnew=1](https://www.processon.com/view/5ea7a1b9e401fd21c196eb17?fromnew=1)**_】_**

**_JVM相关知识_**【[https://www.processon.com/view/5ec5d7c60791290fe0768668?fromnew=1](https://www.processon.com/view/5ec5d7c60791290fe0768668?fromnew=1)】

**_JVM【_**[https://www.processon.com/view/5c749debe4b0f9fba6921d15?fromnew=1](https://www.processon.com/view/5c749debe4b0f9fba6921d15?fromnew=1)**_】_**


## 2.为什么用双亲委派机制，它是什么？

答：首先当某一个类加载器加载“.class”文件的时候，会把任务交给上级类加载器，进行递归操作，也就是当上级类加载器都没有加载，当前加载器才会去加载这个类；就比如：先从BootStrapClassLoader根加载器找，找不到则在ExtClassLoder扩展加载器找，如果还找不到，才会在当前AppClassLoader应用程序加载器找（一般是执行main方法）。双亲委派机制，它防止了去加载同一个“.class”文件，而且保证了核心“.class”文件被篡改，这样保证了Class执行安全。 
![image](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20210802195621202-121782016.png)
![image](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20210802195617062-1898476039.png)


------

# 最后

   关于这块的知识，感觉还是注重实践，因为许多概念上的东西，不通过自己去敲，去练的话，对这方面处于一种只知皮毛的状态；其实我感觉我个人也是在表面上漂着，没有去静下心来去认真的思考过一个问题而且也没有认真的去看过JDK的源码；一路走来，感觉就是没真正的扎进去，通过几次简单的面试其实就能感觉到自己在    哪些方面的缺失，可以帮助自己找到更多的缺点。

   那在这我也想总结一下自己的学习方式：对某块东西的认识先从视频看起，因为我感觉视频还是快的，视频和书各有各的好处吧，我感觉视频可以快速入门，而且中间出现的错误也会有个影响；看完视频的话，像JavaEE方面的知识点，个人觉得看官方文档来的比较快，比较有权威一点，毕竟网上的文章太多了，或者也可以通过某些人整理的简化的官方文档，再去了解真正的官方文档。最后还是就是动手，个人感觉自己动的手太少了，所以对一些东西的理解不是很深；然后在一段时间内去总结一下自己学的东西，必须要总结，这样可以提高自己的逻辑以及以后查阅起来自己学的知识点方便一些，可以简单记录，也可以详细记录，但一般我感觉能让几个月之后的自己看到自己写的东西可以瞬间想起来整个思路的话就其实很好。

   剩下的就是关于微服务这块的知识，个人感觉这块知识单单从平时的demo学习的话，理解其实比较浅，还是觉得应该在实习的时候去真正接触项目的时候，再来去深入的学习一下这方面的知识，虽然现在很卷，但是实习的话，面试官也不会对分布式微服务问的太多，最多问一下一些基础。当然可能毕业后，问的点比较多了。

 **也祝看到此篇随笔的小伙伴，面试顺利，成功拿到心仪Offer！！！**



------

# 题外话



最近，也是偶然间看到了一个视频，叫《经济机器是怎样运行的》，感觉像我这样的经济小白很有启蒙作用！视频的话B站有，可以直接搜。（放个有字幕的视频链接地址：[经济机器是怎样运行的 Ray Dalio（字幕)](https://www.bilibili.com/video/BV1DT4y1A7Qt)）

> **人物介绍**
> **雷·达利奥**（英语：Raymond Dalio，1949年8月8日）出生于[纽约](https://zh.wikipedia.org/wiki/%E7%BA%BD%E7%BA%A6)，现居[康乃狄克州](https://zh.wikipedia.org/wiki/%E5%BA%B7%E4%B9%83%E7%8B%84%E5%85%8B%E5%B7%9E)[费尔菲尔德县](https://zh.wikipedia.org/wiki/%E8%B4%B9%E5%B0%94%E8%8F%B2%E5%B0%94%E5%BE%B7%E5%8E%BF_(%E5%BA%B7%E4%B9%83%E7%8B%84%E5%85%8B%E5%B7%9E))，是美国的著名[对冲基金](https://zh.wikipedia.org/wiki/%E5%AF%B9%E5%86%B2%E5%9F%BA%E9%87%91)经理、慈善家。瑞·达利奥是[桥水基金](https://zh.wikipedia.org/wiki/%E6%A9%8B%E6%B0%B4%E5%9F%BA%E9%87%91)公司的创始人兼首席执行官，而桥水基金于2013年被列为[全世界最大的避险基金公司](https://zh.wikipedia.org/w/index.php?title=%E5%85%A8%E4%B8%96%E7%95%8C%E6%9C%80%E5%A4%A7%E7%9A%84%E9%81%BF%E9%9A%AA%E5%9F%BA%E9%87%91%E5%85%AC%E5%8F%B8&action=edit&redlink=1) [[2]](https://zh.wikipedia.org/wiki/%E9%9B%B7%C2%B7%E9%81%94%E5%88%A9%E5%A5%A7#cite_note-2)[[3]](https://zh.wikipedia.org/wiki/%E9%9B%B7%C2%B7%E9%81%94%E5%88%A9%E5%A5%A7#cite_note-3)。达利奥于2017出版了关于[企业管理](https://zh.wikipedia.org/wiki/%E5%85%AC%E5%8F%B8%E6%B2%BB%E7%90%86)和[金融经济学](https://zh.wikipedia.org/wiki/%E9%87%91%E8%9E%8D%E7%B6%93%E6%BF%9F%E5%AD%B8)的著作《[原则](https://zh.wikipedia.org/wiki/%E5%8E%9F%E5%89%87)》。根据[彭博社](https://zh.wikipedia.org/wiki/%E5%BD%AD%E5%8D%9A%E7%A4%BE)报导，截至2019年1月，他是世界上最富有的100个人中的第79位[[4]](https://zh.wikipedia.org/wiki/%E9%9B%B7%C2%B7%E9%81%94%E5%88%A9%E5%A5%A7#cite_note-4)
> **早年生活**
> 瑞·达利奥出生在一个意大利裔家庭，他的父亲是一位音乐家。12岁时在林克斯高尔夫球场打工并受到那些雇主的耳濡目染下开始把赚来的钱拿来炒股。买进了人生第一支股票[东北航空公司](https://zh.wikipedia.org/wiki/%E4%B8%9C%E5%8C%97%E8%88%AA%E7%A9%BA_(%E7%BE%8E%E5%9B%BD))（Northeast Airlines）。而购买东北航空股票的原因是因为东北航空股价较低，瑞・逹利奥当时以为买的股数越多赚的钱也越多。最后结果是幸运的，成功赚了两倍的钱，但其实是因为东北航空在即将破产之际被收购，才不至让初买股票的瑞・逹利奥血本无归。以后瑞·达利奥先后就读于[长岛大学](https://zh.wikipedia.org/wiki/%E9%95%BF%E5%B2%9B%E5%A4%A7%E5%AD%A6)和[哈佛大学](https://zh.wikipedia.org/wiki/%E5%93%88%E4%BD%9B%E5%A4%A7%E5%AD%A6)，并取得金融学本科学位和[工商管理硕士](https://zh.wikipedia.org/wiki/%E5%B7%A5%E5%95%86%E7%AE%A1%E7%90%86%E7%A2%A9%E5%A3%AB)学位。

> 如果有兴趣的话可以去了解一下，感觉还是很有意思的，下面是MBA智库中的介绍
> **链接**：[https://wiki.mbalib.com/wiki/%E7%91%9E%E8%BE%BE%E5%88%A9%E6%AC%A7](https://wiki.mbalib.com/wiki/%E7%91%9E%E8%BE%BE%E5%88%A9%E6%AC%A7)

























