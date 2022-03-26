> 安装Nginx

> 这篇记录只不过做了一个简单总结，如果对这块没什么概念的话可以看一下知乎的这篇文章
> https://zhuanlan.zhihu.com/p/83890573




# window下安装

window下安装其实是很简单的

## 1、去官网下载安装
**http://nginx.org/en/download.html**

这里我选择的1.18.0版本，可自行选择

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642663294066-9f3e163a-edaf-49a3-9faa-f9b13108b51b.png)

## 2、下载完成之后直接解压得到

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642663435904-d8df3294-52aa-4cbb-b531-3de479a25948.png)

## 3、运行

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642663543428-a78966d6-7651-4603-a682-64e705743d12.png)

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642663640521-bb49f423-ce94-4ab0-bfa7-0df5fc438674.png)

访问：http://localhost:80 

端口可以在**nginx.conf**文件中改

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642663774369-0e7fb906-409a-4cbd-aad8-87521eed5cfc.png)



# Centos7下安装

## 1、去官网下载

### 第一种方式：

直接在终端中用wget工具拉取

```java
wget http://nginx.org/download/nginx-1.18.0.tar.gz
```

### 第二种方式：

去官网下载之后利用filezilla工具从本地传到云服务器上（工具的左侧是本地，右侧可以选择云服务器的路径；如何上传？直接双击左侧本地文件，自动上传到当前右侧目录下，请注意路径的选择！）

filezilla：https://download.filezilla-project.org/client/FileZilla_3.57.0_win64_sponsored-setup.exe

或者也可以使用xshell、xftp工具这些，其实无较大区别。

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642663864305-8dbf32c8-3815-4ef2-8b54-88a3a5c111fc.png)

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642665115695-ed34da14-d9bd-4184-a848-4c0e40b77b29.png)

## 2、安装

首先需要做一些准备工作

> 1、安装gcc
> 安装 nginx 需要先将官网下载的源码进行编译，编译依赖 gcc 环境，如果没有 gcc 环境，则需要安装：

```java
yum install gcc-c++ 
```



> 2、PCRE pcre-devel 安装
> PCRE(Perl Compatible Regular Expressions) 是一个Perl库，包括 perl 兼容的正则表达式库。nginx 的 http 模块使用 pcre 来解析正则表达式，所以需要在 linux 上安装 pcre 库，pcre-devel 是使用 pcre 开发的一个二次开发库。nginx也需要此库。命令：

```java
yum install -y pcre pcre-devel 
```

> 3、zlib 安装
> zlib 库提供了很多种压缩和解压缩的方式， nginx 使用 zlib 对 http 包的内容进行 gzip ，所以需要在 Centos 上安装 zlib 库。

```java
yum install -y zlib zlib-devel 
```

> 4、OpenSSL 安装
> OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及 SSL 协议，并提供丰富的应用程序供测试或其它目的使用。
> nginx 不仅支持 http 协议，还支持 https（即在ssl协议上传输http），所以需要在 Centos 安装 OpenSSL 库。

```java
yum install -y openssl openssl-devel
```

## 完成之后

这里我是以我下载的文件为例

将文件“nginx-1.18.0.tar.gz”放到“usr/local/”目录用“tar -zxvf nginx-1.18.0.tar.gz ”进行解压，然后进入到“nginx-1.18.0”文件夹，依次执行以下三条命令

```java
./configure
make
make install
```

然后查找安装路径命令： whereis nginx

```java
按照我的路径装的nginx，在usr/local/nginx路径下

常用命令
cd /usr/local/nginx/sbin/
./nginx  启动
./nginx -s stop  停止
./nginx -s quit  安全退出
./nginx -s reload  重新加载配置文件
ps aux|grep nginx  查看nginx进程
```

还有就是因为防火墙的问题，可以直接去云服务的面板上做处理开放端口，或者直接在终端中采用命令的方式进行设置防火墙。

```java
# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop
# 查看防火墙规则
firewall-cmd --list-all
# 查询端口是否开放
firewall-cmd --query-port=8080/tcp
# 开放80端口
firewall-cmd --permanent --add-port=80/tcp
# 移除端口
firewall-cmd --permanent --remove-port=8080/tcp

#重启防火墙(修改配置后要重启防火墙)
firewall-cmd --reload

# 参数解释
1、firwall-cmd：是Linux提供的操作firewall的一个工具；
2、--permanent：表示设置为持久；
3、--add-port：标识添加的端口；
```

参考于：https://www.cnblogs.com/hellokuangshen/p/14334300.html

