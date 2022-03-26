# Centos7上一次War包的部署与运行
# 前言
<font size=4>由于前段时间第一次部署一个小型的项目，时间一长所以有些步骤有时候时间一长就忘了，在此做个简单的记录</font>
# 一、原始系统开发环境
+ <font size=4>操作系统：Windows10；</font>
+ <font size=4>开发语言：前端：Html，CSS，JavaScript；后台：Java；</font>
+ <font size=4>开发环境：IntelliJ IDEA 2018，Tomcat8.5；</font>
+ <font size=4>数据库：MySQL；</font>
+ <font size=4>SDK：JDK1.8</font>

---

# 二、当前运行环境
+ <font size=4>阿里云，Centos7系统</font>
+ <font size=4>JDK8，MySql5.7，Tomcat8.5。</font>
+ <font size=4>工具：Xshell，Filezilla或Xftp</font>

# 三、开始部署运行
## 1.下载并使用远程控制终端软件Xshell
**<font size=4>关于ssh终端控制软件还可以使用SecureCRT</font>**

+ <font size=4>连接自己的 阿里云 服务器</font>
+ <font size=4>或者其他的服务器也可以</font>
## 2.安装JDK8
<font size=4>**由于该项目的原因，所以只能使用JDK8进行编译运行代码**</font>
<font size=4>**使用国内镜像源下载jdk：**</font>

<font size=4>**两个链接地址：**</font>

https://repo.huaweicloud.com/java/jdk/

http://www.sousou88.com/spec/java_openjdk.html
+ <font size=4>第一：卸载掉系统原始的OpenJdk</font>
  <font size=4>**命令：**</font>

> <font size=4>I： rpm -qa | grep java   // 查看系统原始的java</font>
> 然后通过rpm -e --nodeps命令或者yum -y remove命令将java开头的安装包均卸载
例子：
> <font size=4>II : rpm -e --nodeps
> java-1.8.0-openjdk-1.8.0.0-1.66.1.13.0.el6.x86_64 //
> 将所有显示出来的java文件利用该命令进行卸载删除</font>
III： yum -y remove java-1.7.0-openjdk-1.7.0.141-2.6.10.5.el7.x86_64

+ <font size=4>第二：利用FTP工具将已下载好的JDK8进行上传</font>

> <font size=4>I: 输入该命令进行解压：tar -zxvf jdk-8u261-linux-x64.tar.gz  </font>
<font size=4>II： 输入该命令进行配置环境变量(也可使用vi编辑器) ： vim /etc/profile</font>
<font size=4>III： 在环境变量中输入以下内容：</font>
<font size=4>注意：JAVA_HOME路径为你的jdk解压后的路径</font>

    #set java environment
    JAVA_HOME=/usr/local/src/java/jdk1.7.0_71
    CLASSPATH=.:$JAVA_HOME/lib.tools.jar
    PATH=$JAVA_HOME/bin:$PATH
    export JAVA_HOME CLASSPATH PATH

><font size=4>IIII： 保存退出后，输入以下命令使环境变量生效： source /etc/profile</font>
<font size=4>IIIII: 输入该命令查看jdk是否安装成功：java -version</font>

- <font size=4>或者可采用联网下载的方式下载 jdk8</font>


## 3.安装MySQL5.7
<font size=4>安装过程在这不在多说，可参考我另一篇文档记录</font>
<font size=4>Centos7或RedHat7下安装Mysql: </font>

> <font size=4>链接：https://www.cnblogs.com/unleashed/p/13917018.html</font>

<font size=4>MySQL安装完成之后，接下来，需要做的是创建一个空的数据库cxxt</font>
<font size=4>注意：如需配置MySQL请自行配置，以下内容为参考内容</font>

> 在/etc ⽬录下新建my.cnf ⽂件
[mysql]
*设置mysql客户端默认字符集
default-character-set=utf8
socket=/var/lib/mysql/mysql.sock
[mysqld]
skip-name-resolve
*设置3306端⼝
port = 3306
socket=/var/lib/mysql/mysql.sock
*设置mysql的安装⽬录
basedir=/usr/local/mysql
*设置mysql数据库的数据的存放⽬录
datadir=/usr/local/mysql/data
*允许最⼤连接数
max_connections=200
*服务端使⽤的字符集默认为8⽐特编码的latin1字符集
character-set-server=utf8
*创建新表时将使⽤的默认存储引擎
default-storage-engine=INNODB
lower_case_table_names=1
max_allowed_packet=16M

## 4.安装Tomcat8
<font size=4>**同样，可以采用联网下载的方式或者利用FTP工具进行上传**</font>

+ <font size=4>将Tomact解压之后，找到“webapps”目录，将war包直接上传至该目录下。</font>
+ <font size=4>返回至Tomcat下的“bin”目录，输入“./startup.sh”命令启动Tomcat；输入“./shutdown.sh”命令进行关闭Tomcat</font>

<font size=5>以下为百度网盘链接</font>

<font size=4>包括JDK8，Tomcat8，MySQL5.7，SecureCRT，FileZilla，Vmware12，centos7，</font>

<font size=4>链接：https://pan.baidu.com/s/1KLn3DJQrlaS3bSxGNa35ZA
提取码：k8wv
</font>

<font size=5>关于war包，如有所需，请联系我！</font>
