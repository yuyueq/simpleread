> SpringMVC执行流程



# 简单原理

> Spring MVC 框架像许多其他 MVC 框架一样, **以请求为驱动** , **围绕一个中心 Servlet 分派请求及提供其他功能**，**DispatcherServlet 是一个实际的 Servlet (它继承自 HttpServlet 基类)**

当发起请求时被前置的控制器拦截到请求，根据请求参数生成代理请求，找到请求对应的实际控制器，控制器处理请求，创建数据模型，访问数据库，将模型响应给中心控制器，控制器使用模型与视图渲染视图结果，将结果返回给中心控制器，再将结果返回给请求者
![](https://unleashed.oss-cn-beijing.aliyuncs.com/win10yuyueq/2031154-20210404220740151-1563231377.png)

---


# 简单的执行流程
![](https://unleashed.oss-cn-beijing.aliyuncs.com/win10yuyueq/2031154-20210404220824710-2074215679.png)


1.**DispatcherServlet**表示一个前端控制器，是整个SpringMVC的控制中心。

​	当用户发出请求，**DispatchServlet**接收请求并拦截请求。

​

 - 我们假设请求的 url 为 : <http://localhost:8080/SpringMVC/hello>

- **如上 url 拆分成三部分：**
 
- <http://localhost:8080> ------> 服务器域名

- SpringMVC ------> 部署在服务器上的 web 站点

 - hello ------> 表示控制器

 - 通过分析，如上 url 表示为：请求位于服务器 localhost:8080 上的 SpringMVC 站点的 hello 控制器

2.**HandlerMapping**表示处理器映射，所以**DispatchSerlvet**去调用**HandlerMapping**,然后**HandlerMapping**根据url去查找**Handler**。

3.**HandlerExcution**表示具体的Handler，主要作用是根据URL去找控制器。

4.HandlerExcution将解析后的信息传递给DispatcherServlet。

5.**HandlerAdapter**表示处理器适配器，它是按照特定的规则去执行**Handler**。

6.**Handler**让具体的Controller执行。

7.**Controller**将具体的执行信息返回给HanderAdapter，比如ModelAndView。

8.HandlerAdapter将视图逻辑名或模型传递给DispatcherServlet。

9.DispatcherServlet调用**视图解析器(ViewResolver**)来解析HandlerAdapter传递的逻辑视图名。

10.视图解析器将解析的逻辑视图名传递给DispatcherServlet。

11.DispatcherServlet根据视图解析器解析的视图结果，调用具体的视图。

12.最后呈现给用户。