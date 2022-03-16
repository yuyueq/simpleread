---
title: 修改RedHat7的root用户密码
date: 2020-11-14 11:48:54.0
updated: 2022-01-21 11:50:14.199
url: /archives/xiu-gai-redhat7-de-root-yong-hu-mi-ma
categories: 安装配置 | Linux
tags: 问题记录 | Linux
---

# 前言

+ <font size=4>前段时间由于长时间没有使用虚拟机里面的一个操作系统，导致密码记得不是太清，登录不进去。今天想起还是做个小记录，以便以后参考。</font>

+ <font size=4>再一个是，当时网上也搜了很多解决问题的博客，但大部分都是同一个博客内容，没有多大的参考价值，所以导致当时试了很久才成功。所以当自己出问题了，还是先要把自身的所犯的错误找出来，这样搜索问题解决方法时才会游刃有余！</font>

# 操作环境

+ <font size=4>主机为window10(关系不大)</font>

+ <font size=4>虚拟机为vmware15pro(关系不大)</font>

+ <font size=4>操作系统为RedHat7(有一定的影响)</font>

# 个人解决步骤

## 第一步

<font size=4>在图片中的界面按下键盘“e”键，然后在**linux16**这一行最后面添加一行内容</font>

> <font size=5> rw rd.break init=/sysroot/bin/sh</font>
> ![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224027489-1459934973.png)
> <font size=4>网上大多数**linux16**那一行参数如图所示</font>
> ![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224123112-129615182.jpg)






<font size=4>但是，由于我用的不同版本的镜像，所以我的解决方法如图</font>

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224039552-209973203.png)
<font size=4>**找到linux16这一行起始地方，然后按end键到这一行最后，再加空格，然后添加这一条语句**</font>

> <font size=5> rw rd.break init=/sysroot/bin/sh</font>
> ![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224159738-1335275260.png)

## 第二步

<font size=4>按下 ctrl+x  进入命令行</font>

## 第三步

<font size=4>输入以下命令：</font>

<font size=4>1.输入 mount</font>

<font size=4>2. 查看是否为“rw”，如果没有则输入 mount –o remount,rw /sysroot</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224222992-1769348671.png)
<font size=4>3. 切换路径 输入 chroot /sysroot</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224310243-581275515.png)
<font size=4>4. 输入 passwd 修改root用户密码  ;此时会给你提一个警告，是因为密码强度太弱了，我们目前个人用的话不用管</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201114224318352-1489652040.png)
<font size=4>5. 输入touch /.autorelabel</font>

<font size=4>6. 输入 exit 退出</font>

<font size=4>7. 输入 reboot 或者不用exit退出，直接输入  exec /sbin/reboot</font>

<font size=4>最后，需要注意的是，可能部分人的问题，最后命令输完后无法自动重启，这时候你可以强行关机并且重启</font>

# 网上解决步骤

**<font size=4>CentOS 7&RHEL 7进入单用户方式和重置密码方式发生了较大变化，GRUB由b引导变成了ctrl+x引导。</font>**

## 重置密码主要有rd.break和init两种方法

## rd.break方法：

> <font size=4>1、启动的时候，在启动界面，相应启动项，内核名称上按“e”；</font>
>
> <font size=4>2、进入后，找到linux16开头的地方，按“end”键到最后，输入rd.break，按ctrl+x进入；</font>
>
> <font size=4>3、进去后输入命令mount，发现根为/sysroot/，并且不能写，只有ro=readonly权限；</font>
>
> <font size=4>4、mount -o remount,rw /sysroot/，重新挂载，之后mount，发现有了r,w权限；</font>
>
> <font size=4>5、chroot /sysroot/ 改变根；</font>
>
> <font size=4>（1）echo [RedHat](http://www.linuxidc.com/topicnews.aspx?tid=10)|passwd –stdin root 修改root密码为redhat，或者输入passwd，交互修改；</font>
>
> <font size=4>（2）还有就是先cp一份，然后修改/etc/shadow文件</font>
>
> <font size=4>6、touch /.autorelabel 这句是为了selinux生效</font>
>
> <font size=4>7、ctrl+d 退出</font>
>
> <font size=4>8、然后reboot</font>
>
> <font size=4>至此，密码修改完成</font>

## init方法：

> <font size=4>1. 启动系统，并在GRUB2启动屏显时，按下e键进入编辑模式。</font>
>
> <font size=4>2. 在linux16/linux/linuxefi所在参数行尾添加以下内容：init=/bin/sh</font>
>
> <font size=4>3. 按Ctrl+x启动到shell。</font>
>
> <font size=4>4. 挂载文件系统为可写模式：mount –o remount,rw /</font>
>
> <font size=4>5. 运行passwd,并按提示修改root密码。</font>
>
> <font size=4>6. 如何之前系统启用了selinux，必须运行以下命令，否则将无法正常启动系统：touch /.autorelabel</font>
>
> <font size=4>7. 运行命令exec /sbin/init来正常启动，或者用命令exec /sbin/reboot重启</font>

# 最后

<font size=4>网上的方法中init方法我试过，但另一种并未试过，但是从解决问题的过程中来看，两者区别不大；并且要注意以上仅仅是本人的解决步骤，有可能由于各种问题，每个人解决过程中会遇到不一样的错误，当然和我的一样更好，直接可以解决，如果不一样请仅当参考使用！</font>
<font size=4>一般按照以上我的**个人步骤**解决，基本不会出多余的问题，唯一的问题就是可能最后要自己强行重启！</font>
<font size=4>如果root用户可以登录，那种修改密码的方式就不在这记录了，主要找到passwd路径基本就可以解决了！</font>