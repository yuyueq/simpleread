
# Spring

## IOC与DI

**1.[SpringIoC&DI](docs/java/framework/spring/1/SpringIoC&DI.md)**

  + 1. spring概述
    - 1.1 Spring是什么（理解）
    - 1.2 Spring发展历程 （了解）
    - 1.3 Spring的优势（理解）
    - 1.4 Spring的体系结构（了解）
  + 2. spring快速入门
    - 2.1 Spring程序开发步骤 
    - 2.2 导入Spring开发的基本包坐标
    - 2.3 编写Dao接口和实现类
    - 2.4 创建Spring核心配置文件
    - 2.5 在Spring配置文件中配置UserDaoImpl
    - 2.6 使用Spring的API获得Bean实例
  + 3. Spring配置文件
    - 3.1 Bean标签基本配置 
    - 3.2 Bean标签范围配置 
    - 3.3 Bean生命周期配置
    - 3.4 Bean实例化三种方式
    - 3.5 Bean的依赖注入入门
    - 3.6 Bean的依赖注入概念
    - 3.7 Bean的依赖注入方式
    - 3.8 Bean的依赖注入的数据类型
    - 3.9 引入其他配置文件（分模块开发）
  + 4. spring相关API
    - 4.1 ApplicationContext的继承体系
    - 4.2 ApplicationContext的实现类
    - 4.3 getBean()方法使用



**2.[SpringIoC和DI注解开发](docs/java/framework/spring/2/SpringIoC和DI注解开发.md)**

+ 1.Spring配置数据源
  - 1.1 数据源（连接池）的作用 
  - 1.2 数据源的手动创建
  - 1.3 Spring配置数据源
  - 1.4 抽取jdbc配置文件
  - 1.5 知识要点 
+ 2. Spring注解开发
  - 2.1 Spring原始注解
  - 2.2 Spring新注解
+ 3. Spring整合Junit
  - 3.1 原始Junit测试Spring的问题
  - 3.2 上述问题解决思路
  - 3.3 Spring集成Junit步骤
  - 3.4 Spring集成Junit代码实现


## Aop

**3.[SpringAop](docs/java/framework/spring/3/SpringAop.md)**

+ 1.**Spring 的 AOP 简介**
  
  - 1.1 什么是 AOP 
  - 1.2 AOP 的作用及其优势
  - 1.3 AOP 的底层实现
  - 1.4 AOP 的动态代理技术
  - 1.5 JDK 的动态代理
  - 1.6 cglib 的动态代理
  - 1.7 AOP 相关概念
  - 1.8 AOP 开发明确的事项
    - 1)需要编写的内容
    - 2）AOP 技术实现的内容
    - 3）AOP 底层使用哪种代理方式
- 1.9 知识要点
  
+ 2. **基于 XML 的 AOP 开发**
  - 2.1 快速入门
  - 2.2 XML 配置 AOP 详解
    - 1) 切点表达式的写法
    - 2) 通知的类型
    - 3) 切点表达式的抽取
  - 2.3 知识要点

+ 3 **.基于注解的 AOP 开发**
  
  - 3.1 快速入门
  - 3.2 注解配置 AOP 详解
    - 1) 注解通知的类型
    - 2) 切点表达式的抽取
  - 3.3 知识要点

**3.[SpringJdbcTemplate&声明式事务](docs/java/framework/spring/4/SpringJdbcTemplate&声明式事务.md)**


+ **JdbcTemplate基本使用**
  
  - 01-JdbcTemplate基本使用-概述(了解)
  - 02-JdbcTemplate基本使用-开发步骤(理解)
  - 03-JdbcTemplate基本使用-快速入门代码实现(应用)
  - 04-JdbcTemplate基本使用-spring产生模板对象分析(理解)
  - 05-JdbcTemplate基本使用-spring产生模板对象代码实现(应用)
  - 06-JdbcTemplate基本使用-spring产生模板对象代码实现（抽取jdbc.properties）(应用)
  - 07-JdbcTemplate基本使用-常用操作-更新操作(应用)
  - 08-JdbcTemplate基本使用-常用操作-查询操作(应用)
  - 09-JdbcTemplate基本使用-知识要点(理解，记忆)
  
+ **声明式事务控制**
  
  - 1. **编程式事务控制相关对象**
    - 1.1 PlatformTransactionManager 
    - 1.2 TransactionDefinition
      - 1. 事务隔离级别
      - 2. 事务传播行为
  - 1.3 TransactionStatus
  - 1.4 知识要点
+ 2 **基于 XML 的声明式事务控制**
  
  - 2.1 什么是声明式事务控制
  - 2.2 声明式事务控制的实现
  - 2.3 切点方法的事务参数的配置
- 2.4 知识要点
  
+ 3 **基于注解的声明式事务控制**
  
  - 3.1 使用注解配置声明式事务控制
  - 3.2 注解配置声明式事务控制解析
  - 3.3 知识要点

---
# SpringMVC

**1.[Spring与Web环境集成即入门](docs/java/framework/springMVC/1/Spring与Web环境集成即入门.md)**

1. **Spring与Web环境集成**

    1.1 ApplicationContext应用上下文获取方式

    1.2 Spring提供获取应用上下文的工具

    1.3 导入Spring集成web的坐标

    1.4 配置ContextLoaderListener监听器

    1.5 通过工具获得应用上下文对象

2. **SpringMVC的简介**

    2.1 SpringMVC概述

    2.3 SpringMVC快速入门

    2.3 SpringMVC流程图示

    2.4 知识要点

3. **SpringMVC的组件解析**

    3.1 SpringMVC的执行流程

    3.2 SpringMVC组件解析

    3.3 SpringMVC注解解析

    3.4 SpringMVC的XML配置解析

    3.5 知识要点

**2.[SpringMVC数据请求与响应](docs/java/framework/springMVC/2/SpringMVC数据请求与响应.md)**

**SpringMVC的数据响应**

   01-SpringMVC的数据响应-数据响应方式(理解)
   
   02-SpringMVC的数据响应-页面跳转-返回字符串形式（应用）

   03-SpringMVC的数据响应-页面跳转-返回ModelAndView形式1(应用)

   04-SpringMVC的数据响应-页面跳转-返回ModelAndView形式2(应用)

   05-SpringMVC的数据响应-页面跳转-返回ModelAndView3(应用)

   06-SpringMVC的数据响应-回写数据-直接回写字符串(应用)

   07-SpringMVC的数据响应-回写数据-直接回写json格式字符串(应用)

   08-SpringMVC的数据响应-回写数据-返回对象或集合(应用)

   09-SpringMVC的数据响应-回写数据-返回对象或集合2(应用)

   10-SpringMVC的数据响应-知识要点小结(理解，记忆)

**SpringMVC的请求**

   11-SpringMVC的请求-获得请求参数-请求参数类型(理解)

   12-SpringMVC的请求-获得请求参数-获得基本类型参数(应用)

   13-SpringMVC的请求-获得请求参数-获得POJO类型参数(应用)

   14-SpringMVC的请求-获得请求参数-获得数组类型参数(应用)

   15-SpringMVC的请求-获得请求参数-获得集合类型参数1(应用)

   16-SpringMVC的请求-获得请求参数-获得集合类型参数2(应用)

   17-SpringMVC的请求-获得请求参数-静态资源访问的开启(应用)

   18-SpringMVC的请求-获得请求参数-配置全局乱码过滤器(应用)

   19-SpringMVC的请求-获得请求参数-参数绑定注解@RequestParam(应用)
   
   20-SpringMVC的请求-获得请求参数-Restful风格的参数的获取(应用)

   21-SpringMVC的请求-获得请求参数-自定义类型转换器(应用)

   22-SpringMVC的请求-获得请求参数-获得Servlet相关API(应用)

   23-SpringMVC的请求-获得请求参数-获得请求头信息(应用)

**3.[SpringMVC的文件上传、拦截器及异常处理](docs/java/framework/springMVC/3/SpringMVC的文件上传、拦截器及异常处理.md)**

**SpringMVC的请求-文件上传**

   1-SpringMVC的请求-文件上传-客户端表单实现(应用)

   2-SpringMVC的请求-文件上传-文件上传的原理(理解)

   3-SpringMVC的请求-文件上传-单文件上传的代码实现1(应用)

   4-SpringMVC的请求-文件上传-单文件上传的代码实现2(应用)

   5-SpringMVC的请求-文件上传-多文件上传的代码实现(应用)

   6-SpringMVC的请求-知识要点(理解，记忆)


**SpringMVC的拦截器**

   01-SpringMVC拦截器-拦截器的作用(理解)

   02-SpringMVC拦截器-interceptor和filter区别(理解，记忆)

   03-SpringMVC拦截器-快速入门(应用)

   04-SpringMVC拦截器-快速入门详解(应用)

   05-SpringMVC拦截器-知识小结(记忆)

   06-SpringMVC拦截器-用户登录权限控制分析(理解)

   07-SpringMVC拦截器-用户登录权限控制代码实现1(应用)

   08-SpringMVC拦截器-用户登录权限控制代码实现2(应用)

   09-SpringMVC拦截器-用户登录权限控制代码实现3(应用)

1. **SpringMVC异常处理机制**
1.1 异常处理的思路

1.2 异常处理两种方式

1.3 简单异常处理器SimpleMappingExceptionResolver

1.4 自定义异常处理步骤

1.5 知识要点


## Spring+SpringMVC综合练习
**4.[Spring+SpringMVC综合练习](docs/java/framework/springMVC/4/Spring+SpringMVC综合练习.md)**

**Spring练习**
   01-Spring练习-环境搭建步骤分析(理解)

   02-Spring练习-环境搭建实现1(应用)

   03-Spring练习-环境搭建实现2(应用)

   04-Spring练习-环境搭建实现3(应用)
   
   05-Spring练习-环境搭建实现4(应用)

   06-Spring练习-用户表和角色表的分析(理解)

   07-Spring练习-角色列表展示分析(理解)

   08-Spring练习-角色列表展示-controller层实现(应用)

   09-Spring练习-角色列表展示-service和dao层实现(应用)

   10-Spring练习-角色列表展示-配置实现(应用)

   11-Spring练习-角色列表展示-页面展示(应用)

   12-Spring练习-角色的添加操作(应用)

   13-Spring练习-用户列表展示1(应用)

   14-Spring练习-用户列表展示2(应用)

   15-Spring练习-用户添加操作-添加页面展示(应用)

   16-Spring练习-用户添加操作-添加数据到数据库(应用)

   17-Spring练习-用户添加操作-添加数据到数据库2(应用)

   18-Spring练习-删除用户操作(应用)

---

# MyBatis
**1.[Mybatis快速入门](docs/java/framework/Mybatis/1/Mybatis快速入门.md)**

1. **Mybatis简介**
   1.1原始jdbc操作（查询数据）

   1.2原始jdbc操作（插入数据）

	 1.3 原始jdbc操作的分析

   1.4 什么是Mybatis

2. **Mybatis的快速入门**

	2.1 MyBatis开发步骤

	2.2 环境搭建

	2.3 编写测试代码

	2.4 知识小结

3. **MyBatis的映射文件概述**

4. **MyBatis的增删改查操作**

	4.1 MyBatis的插入数据操作

	4.2 MyBatis的修改数据操作

	4.3 MyBatis的删除数据操作

	4.4 知识小结

5. **MyBatis核心配置文件概述**

	5.1 MyBatis核心配置文件层级关系

	5.2 MyBatis常用配置解析

**2.[Mybatis的dao层实现原理](docs/java/framework/Mybatis/2/Mybatis的dao层实现原理.md)**

1. **Mybatis的Dao层实现**

    1.1 **传统开发方式**

    1.1.1编写UserDao接口

    1.1.2.编写UserDaoImpl实现

	  1.1.3 测试传统方式

    1.2 **代理开发方式**

	  1.2.1 代理开发方式介绍

    1.2.2 编写UserMapper接口

    1.2.3测试代理方式

	1.3 **知识小结**

2. **MyBatis映射文件深入**

	2.1 **动态sql语句**
		2.1.1 动态sql语句概述
    
	  2.1.2 动态 SQL 之<if>

	  2.1.3 动态 SQL 之<foreach>


**3.[Mybatis的多表操作](docs/java/framework/Mybatis/3/Mybatis的多表操作.md)**

1. **Mybatis多表查询**

	1.1 **一对一查询**
		1.1.1 一对一查询的模型MapperScannerConfigurer

	  1.1.2一对一查询的语句

	  1.1.3 创建Order和User实体

    1.1.4 创建OrderMapper接口

	  1.1.5 配置OrderMapper.xml

    1.1.6 测试结果

	1.2 **一对多查询**

	  1.2.1 一对多查询的模型

	  1.2.2 一对多查询的语句

	  1.2.3 修改User实体

	  1.2.4 创建UserMapper接口

	  1.2.5 配置UserMapper.xml

	  1.2.6 测试结果

	1.3 **多对多查询**

	  1.3.1 多对多查询的模型

	  1.3.2 多对多查询的语句

	  1.3.3 创建Role实体，修改User实体

	  1.3.4 添加UserMapper接口方法

	  1.3.5 配置UserMapper.xml

	  1.3.6 测试结果

	1.4 **知识小结**

2.**Mybatis的注解开发**

  2.1 **MyBatis的常用注解**

  2.2 **MyBatis的增删改查**

  2.3 **MyBatis的注解实现复杂映射开发**

  2.4 **一对一查询**

  2.4.1 一对一查询的模型

  2.4.2 一对一查询的语句

  2.4.3 创建Order和User实体

  2.4.4 创建OrderMapper接口

  2.4.5 使用注解配置Mapper

  2.4.6 测试结果

  2.5 **一对多查询**

  2.5.1 一对多查询的模型

  2.5.2 一对多查询的语句

  2.5.3 修改User实体

  2.5.4 创建UserMapper接口

  2.5.5 使用注解配置Mapper

  2.5.6 测试结果

  2.6 **多对多查询**

   2.6.1 多对多查询的模型

   2.6.2 多对多查询的语句

   2.6.3 创建Role实体，修改User实体

   2.6.4 添加UserMapper接口方法

   2.6.5 使用注解配置Mapper
  
   2.6.6 测试结果


**4.[SSM整合](docs/java/framework/Mybatis/4/SSM整合.md)**

SSM框架整合

1.1 原始方式整合

1.准备工作

2.创建Maven工程

3.导入Maven坐标

4.编写实体类

5.编写Mapper接口

6.编写Service接口

7.编写Service接口实现

8.编写Controller

9.编写添加页面

10.编写列表页面

11.编写相应配置文件(文件参考目录：素材/配置文件)

12.测试添加账户

13.测试账户列表

1.2 Spring整合MyBatis

1.整合思路

2.将SqlSessionFactory配置到Spring容器中

3.扫描Mapper，让Spring容器产生Mapper实现类

4.配置声明式事务控制

5.修改Service实现类代码





---


















