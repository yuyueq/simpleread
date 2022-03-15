---
title:  记Centos7和RHEL连接不上网络
date: 2020-07-10 12:03:11.0
updated: 2022-01-21 11:04:00.515
url: /archives/ji-centos7-he-rhel-lian-jie-bu-shang-wang-luo
categories: 安装配置 | Linux
tags: 问题记录 | Linux
---



# 一 、前言

1. **我是把Linux系统安装在虚拟机中的，用的是VMware。**
2. **在终端工具和操作界面中。**

1. **VMware里面采用的网络适配器是NAT技术。**

```
ping不通域名和IP地址；并且ifconfig命令回车之后并不会出来正确的IP地址。
ip address 这个命令也不会出来正确的结果
```



# 第一步：

```
输入 “ifconfig”  或者输入 “ifconfig -a”命令功能；或者 ping 地址
```



## 关于ifconfig命令：

```
功能：
ifconfig 命令用来查看和配置网络设备。当网络环境发生改变时可通过此命令对网络进行相应的配置。

命令参数：
up                启动指定网络设备/网卡。

down              关闭指定网络设备/网卡。该参数可以有效地阻止通过指定接口的IP信          息流，如果想永久地关闭一个接口，我们还需要从核心路由表中将该接口的路由信息全部删除。

arp               设置指定网卡是否支持ARP协议。

-promisc           设置是否支持网卡的promiscuous模式，如果选择此参数，网卡将接收网络中发给它所有的数据包

-allmulti          设置是否支持多播模式，如果选择此参数，网卡将接收网络中所有的多播数据包

-a                 显示全部接口信息

-s                  显示摘要信息（类似于 netstat -i）

add                 给指定网卡配置IPv6地址

del                 删除指定网卡的IPv6地址

                  <硬件地址> 配置网卡最大的传输单元

mtu<字节数>           设置网卡的最大传输单元 (bytes)

netmask<子网掩码> 设置网卡的子网掩码。掩码可以是有前缀0x的32位十六进制数，也可以是用点分开的4个十进制数。如果不打算将网络分成子网，可以不管这一选项；
如果要使用子网，那么请记住，网络中每一个系统必须有相同子网掩码。

tunel                 建立隧道

dstaddr               设定一个远端地址，建立点对点通信

-broadcast<地址> 为指定网卡设置广播协议

-pointtopoint<地址> 为网卡设置点对点通讯协议

multicast             为网卡设置组播标志

address               为网卡设置IPv4地址

txqueuelen<长度>         为网卡设置传输列队的长度

```



# 第二步：

### 以下仅仅为个人问题解决方法

```
一、打开终端
二、输入命令            cd  /etc/sysconfig/network-scripts/
                     （接着输入命令 ls 查看文件夹下的东西）                   
三、继续输入命令         vi ifcfg-eno16777736
                     （ eno 后面的数字并非都一致；可以采用 Tab 键自动补全）
四、更改文件内容                                  
```

​                          

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642733982280-11cbb0f1-8d1f-45c5-9d1a-159db9b315f7.png)

```
五、保存退出之后输入 “service network restart”  重启网络服务
```



***此时，问题应该解决了！你可以通过远程工具连接，也可以ping通网络地址了！***



# 三、后记

***因为上述所说的方法是针对于我个人所遇到的问题，所以此方法是有局限性的；如果你也是和我一样遇到的上述问题，但是通过这种方法未解决的话，你可以参考一下下面的两篇文章。***

转载：

Centos7网络配置及静态IP配置： https://my.oschina.net/calmsnow/blog/3002952

Centos7修改网卡类型为ifcfg-eth0: https://my.oschina.net/calmsnow/blog/3000435

















