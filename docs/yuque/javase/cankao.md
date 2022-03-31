# day01

## 二进制与十进制的转换运算
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/03-%E4%BA%8C%E8%BF%9B%E5%88%B6%E4%B8%8E%E5%8D%81%E8%BF%9B%E5%88%B6%E7%9A%84%E8%BD%AC%E6%8D%A2%E8%BF%90%E7%AE%97.png)

## JDK&JRE&JVM关系示意图
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/07-JDK&JRE&JVM%E5%85%B3%E7%B3%BB%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## 计算机存储单位转换

```txt
位（bit）：一个数字0或者一个数字1，代表一位。
字节（Byte）：每逢8位是一个字节，这是数据存储的最小单位。

1 Byte = 8 bit

1 KB = 1024 Byte
1 MB = 1024 KB
1 GB = 1024 MB
1 TB = 1024 GB
1 PB = 1024 TB
1 EB = 1024 PB
1 ZB = 1024 EB
```

## 命令提示符的常用命令

```txt
MS-DOS(Microsoft Disk Operating System)

命令提示符（cmd）

启动：		Win+R，输入cmd回车
切换盘符	盘符名称:
进入文件夹	cd 文件夹名称
进入多级文件夹	cd 文件夹1\文件夹2\文件夹3
返回上一级	cd ..
直接回根路径	cd \
查看当前内容	dir
清屏		cls
退出		exit
```

## 关键字的概念举例和特征

```txt
12345@qq.com
javaitcast@163.com

_______@163.com

abc@163.com
abc123@163.com

尼古拉斯·赵四
nigulasi@zhaosi@itcast.cn

@是电子邮箱当中有特殊含义的、被保留的、不能随意使用的字符。
这样的字符被称为关键字。

关键字的特点：
	1. 完全小写的字母。
	2. 在增强版的记事本当中（例如Notepad++）有特殊颜色。
```

## 数据类型分类

```txt
基本数据类型【今天重点】
	整数型	byte short int long
	浮点型	float double
	字符型	char
	布尔型	boolean

引用数据类型（今后学习）
	字符串、数组、类、接口、Lambda
	
注意事项：
1. 字符串不是基本类型，而是引用类型。
2. 浮点型可能只是一个近似值，并非精确的值。
3. 数据范围与字节数不一定相关，例如float数据范围比long更加广泛，但是float是4字节，long是8字节。
4. 浮点数当中默认类型是double。如果一定要使用float类型，需要加上一个后缀F。
   如果是整数，默认为int类型，如果一定要使用long类型，需要加上一个后缀L。推荐使用大写字母后缀。
```

---

# day02 数据类型转换、运算符、方法入门

## 强制类型转换的数据溢出问题

![01-强制类型转换的数据溢出问题](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/01-%E5%BC%BA%E5%88%B6%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2%E7%9A%84%E6%95%B0%E6%8D%AE%E6%BA%A2%E5%87%BA%E9%97%AE%E9%A2%98.png)


---


# day03 流程控制语句

## 顺序结构的流程图

![01-顺序结构的流程图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/01-%E9%A1%BA%E5%BA%8F%E7%BB%93%E6%9E%84%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## 单if语句

![02-单if语句的流程图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/02-%E5%8D%95if%E8%AF%AD%E5%8F%A5%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## 标准if-else语句

![03-标准if-else语句的流程图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/03-%E6%A0%87%E5%87%86if-else%E8%AF%AD%E5%8F%A5%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## 扩展if-else语句

![04-扩展if-else语句的流程图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/04-%E6%89%A9%E5%B1%95if-else%E8%AF%AD%E5%8F%A5%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## for循环

![05-for循环的流程图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/05-for%E5%BE%AA%E7%8E%AF%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)

## while循环

![06-while循环的流程图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/06-while%E5%BE%AA%E7%8E%AF%E7%9A%84%E6%B5%81%E7%A8%8B%E5%9B%BE.png)


---

# day04 

## 集成开发环境IDE的概述 
```txt
Integrated Development Environment，IDE，集成开发环境

如果自己手洗衣服：
1. 准备一盆水
2. 放入衣服浸泡30分钟
3. 搓洗衣服
4. 倒掉水，换一盆水
5. 漂洗衣服
6. 倒掉水
7. 拧干衣服
8. 晾晒

如果使用全自动洗衣机：
1. 放入衣服，打开开关
2. 拿出衣服，晾晒

回顾一下开发Java程序的步骤：
1. 编写代码
2. 启动cmd
3. 调用javac编译
4. 调用java运行

集成开发环境，是一种专门用来提高Java开发效率的软件。
免费的IDE当中：Eclipse
收费的IDE当中：IntelliJ IDEA
免费+收费所有的IDE当中：全世界用得最多的就是IntelliJ IDEA
```

## IDEA的项目结构
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/02-IDEA%E7%9A%84%E9%A1%B9%E7%9B%AE%E7%BB%93%E6%9E%84.png)

## 方法调用流程图解
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/03-%E6%96%B9%E6%B3%95%E8%B0%83%E7%94%A8%E6%B5%81%E7%A8%8B%E5%9B%BE%E8%A7%A3.png)

## 方法返回值的有无
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/04-%E6%96%B9%E6%B3%95%E8%BF%94%E5%9B%9E%E5%80%BC%E7%9A%84%E6%9C%89%E6%97%A0.png)


---

# day05 数组

## Java中的内存划分

![01-Java中的内存划分](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/01-Java%E4%B8%AD%E7%9A%84%E5%86%85%E5%AD%98%E5%88%92%E5%88%86.png)

## 只有一个数组的内存图

![02-只有一个数组的内存图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/02-%E5%8F%AA%E6%9C%89%E4%B8%80%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

## 有两个独立数组的内存图

![03-有两个独立数组的内存图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/03-%E6%9C%89%E4%B8%A4%E4%B8%AA%E7%8B%AC%E7%AB%8B%E6%95%B0%E7%BB%84%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

## 两个引用指向同一个数组的内存图

![04-两个引用指向同一个数组的内存图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/04-%E4%B8%A4%E4%B8%AA%E5%BC%95%E7%94%A8%E6%8C%87%E5%90%91%E5%90%8C%E4%B8%80%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

## 数组的长度运行期间不可改变

![05-数组的长度运行期间不可改变](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/05-%E6%95%B0%E7%BB%84%E7%9A%84%E9%95%BF%E5%BA%A6%E8%BF%90%E8%A1%8C%E6%9C%9F%E9%97%B4%E4%B8%8D%E5%8F%AF%E6%94%B9%E5%8F%98.png)

## 比武招亲的示意图

![06-比武招亲的示意图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/06-%E6%AF%94%E6%AD%A6%E6%8B%9B%E4%BA%B2%E7%9A%84%E7%A4%BA%E6%84%8F%E5%9B%BE.png)

## 数组元素反转的思路

![07-数组元素反转的思路](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/07-%E6%95%B0%E7%BB%84%E5%85%83%E7%B4%A0%E5%8F%8D%E8%BD%AC%E7%9A%84%E6%80%9D%E8%B7%AF.png)

---

# day06 类与对象、封装、构造方法

## 只有一个对象的内存图
![01-只有一个对象的内存图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/01-%E5%8F%AA%E6%9C%89%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

## 两个对象使用同一个方法的内存图
![02-两个对象使用同一个方法的内存图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/02-%E4%B8%A4%E4%B8%AA%E5%AF%B9%E8%B1%A1%E4%BD%BF%E7%94%A8%E5%90%8C%E4%B8%80%E4%B8%AA%E6%96%B9%E6%B3%95%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

## 两个引用指向同一个对象的内存图
![03-两个引用指向同一个对象的内存图](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/03-%E4%B8%A4%E4%B8%AA%E5%BC%95%E7%94%A8%E6%8C%87%E5%90%91%E5%90%8C%E4%B8%80%E4%B8%AA%E5%AF%B9%E8%B1%A1%E7%9A%84%E5%86%85%E5%AD%98%E5%9B%BE.png)

## 使用对象类型作为方法的参数
![04-使用对象类型作为方法的参数](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/04-%E4%BD%BF%E7%94%A8%E5%AF%B9%E8%B1%A1%E7%B1%BB%E5%9E%8B%E4%BD%9C%E4%B8%BA%E6%96%B9%E6%B3%95%E7%9A%84%E5%8F%82%E6%95%B0.png)

## 使用对象类型作为方法的返回值
![04-使用对象类型作为方法的参数](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/05-%E4%BD%BF%E7%94%A8%E5%AF%B9%E8%B1%A1%E7%B1%BB%E5%9E%8B%E4%BD%9C%E4%B8%BA%E6%96%B9%E6%B3%95%E7%9A%84%E8%BF%94%E5%9B%9E%E5%80%BC.png)

---

# day07 Scanner类、Random类、ArrayList类






