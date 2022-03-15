---
title: Linux目录，rpm及top，vi命令简记
date: 2020-11-03 11:45:39.0
updated: 2022-01-21 11:47:00.889
url: /archives/linux-mu-lu-rpm-ji-topvi-ming-ling-jian-ji
categories: Linux
tags: 学习记录
---

# 一次简单的Linux常用操作记录

## 一、一些Linux目录结构

### /bin

<font size=4>存放二进制可执行文件（ls、cat、mkdir等），一些常用的命令一般都在这里。</font>

### /etc

<font size=4>存放系统管理和配置文件</font>

### /home

<font size=4>存放所有用户文件夹的根目录</font>

### /usr

<font size=4>用于存放系统的应用程序，其中需要注意的是**/usr/local，本地系统管理员软件安装目录（安装系统级的应用）**。</font>

<font size=4>/usr/lib 常用的动态连接库和软件包的配置文件</font>

<font size=4>/usr/man 帮助文档</font>

<font size=4>/usr/src/linux Linux内核的源代码</font>

<font size=4>/opt 额外安装的可选应用程序包放置的位置。一般情况下，我们可以把tomcat等都安装到这</font>

<font size=4>/tmp 用于存放各种临时文件，是公用的临时文件存储点。</font>

<font size=4>/var 用于存放运行时需要改变数据的文件，也是某些大文件的溢出区，比方说**各种服务的日志文件（系统启动日志**）</font>

## 二、rpm执行安装包

### <font size=5>常用命令：</font>

<font size=4>**rpm -ivh //安装软件包**</font>

<font size=4>rpm -Uvh  //升级软件包</font>

<font size=4>rpm -qpi  //列出RPM软件包的描述信息</font>

<font size=4>rpm -qf  //查找指定文件属于哪个RPM软件包[Query File]</font>

<font size=4>rpm -Va  //查找指定文件属于哪个RPM软件包</font>

**<font size=4>rpm -e  //删除包</font>**

<font size=4>rpm -qa | grep htted  //搜索指定rpm包是否安装</font>

### 常用参数:

<font size=4>-i, --install      install package(s)</font>

<font size=4>-v, --verbose             provide more detailed output</font>

<font size=4>-h, --hash    print hash marks as package installs (good with -v)</font>

<font size=4>-e, --erase        erase (uninstall) package</font>

<font size=4>--test      安装测试，并不实际安装</font>

<font size=4>--nodeps      忽略软件包的依赖关系强行安装
 </font>

<font size=4>--force               忽略软件包及文件的冲突</font>

## 三、top命令

<font size=4>TOP命令是Linux下常用的性能分析工具，能够实时显示系统中各个进程的资源占用状况。TOP是一个动态显示过程,即可以通过用户按键来不断刷新当前状态.如果在前台执行该命令,它将独占前台,直到用户终止该程序为止.比较准确的说,top命令提供了实时的对系统处理器的状态监视.它将显示系统中CPU最“敏感”的任务列表.该命令可以按CPU使用.内存使用和执行时间对任务进行排序；而且该命令的很多特性都可以通过交互式命令或者在个人定制文件中进行设定.</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201103180220901-2060600570.png)


<font size=4>**第一行是任务队列信息**</font>

<font size=4>分别是 **当前时间、系统运行时间（格式为时：分）、当前登录用户数、系统负载**</font>

<font size=4>**第二、三行是进程和CPU的信息**</font>

<font size=4>分别是 进程总数，正在运行的进程数，睡眠的进程数，停止的进程数，僵尸进程数、用户空间占用CPU百分比、内核空间占用CPU百分比、用户进程空间内改变过优先级的进程占用CPU百分比、空闲CPU百分比、等待输入输出的CPU时间百分比</font>

<font size=4>**第四、五行为内存信息**</font>

<font size=4>物理内存总量、使用的物理内存总量、空闲内存总量、用作内核缓存的内存量、交换区总量、使用的交换区总量、空闲交换区总量、缓冲交换区总量</font>

<font size=4>剩下 的进程信息区为各个进程的详细信息</font>

## 四、Vi命令

<font size=4>vi编辑器是所有Unix及Linux系统下标准的编辑器，它的强大不逊色于任何最新的文本编辑器，这里只是简单地介绍一下它的用法和一小部分指令。由于对Unix及Linux系统的任何版本，vi编辑器是完全相同的，因此您可以在其他任何介绍vi的地方进一步了解它。Vi也是Linux中最基本的文本编辑器</font>

## 五、Centos6与7一些小区别记录

<font size=4>CentOS7里不推荐使用/etc/rc.local,但是如果要使用,必须加 chmod +x /etc/rc.d/rc.local  加执行权限,才可以正常使用</font>

<font size=4>CentOS6使用:chkconfig 或 /etc/init 和 service； CentOS7使用:systemctl进行了统一,兼容 SysV 和LSB的启动脚本,而且能够在进程启动过程中更有效的引导加载服务</font>

> **启动停止**
>
> [CentOS6]
>
> ```text
> $ service xxxxx start
> $ service xxxxx stop
> $ service sshd restart/status/reload
> ```
>
> [CentOS7]
>
> ```text
> $ systemctl start xxxxx
> $ systemctl stop xxxxx
> $ systemctl restart/status/reload sshd
> ```
>
> **网络信息**
>
> [CentOS6]
>
> ```text
> $ netstat
> $ netstat -I
> $ netstat -n
> ```
>
> [CentOS7]
>
> ```text
> $ ip n
> $ ip -s l
> $ ss
> ```
>
> **IP地址MAC地址**
>
> [CentOS6]
>
> ```text
> $ ifconfig -a
> ```
>
> [CentOS7]
>
> ```text
> $ ip address show
> $ ip addr
> ```
>
> **关闭**
>
> [CentOS6]
>
> ```text
> $ shutdown -h now 
> ```
>
> [CentOS7]
>
> ```text
> $ poweroff
> $ systemctl poweroff
> ```
>
> **重启**
>
> [CentOS6]
>
> ```text
> $ reboot
> $ shutdown -r now
> ```
>
> [CentOS7]
>
> ```text
> $ reboot
> $ systemctl reboot
> ```
>
> **常用命令**
>
> ```text
> ipconfig 变成了 ip addr
> service iptables restart 变成了 systemctl restart firewalld
> chkconfig  iptables  off 变成了 systemctl disable firewalld 
> ```

