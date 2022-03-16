---
title: Windows下的Linux子系统
date: 2020-06-06 17:40:17.0
updated: 2022-01-20 17:41:45.321
url: /archives/windows-xia-de-linux-zi-xi-tong
categories: 安装配置
tags: 问题记录 | Windows | Linux
---



**强调！！！必须是Windows专业版！！！**

**一、安装运行过程**

## **第一步**：打开***开发人员模式***

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642668088823-ea0d81a2-56f7-4b0e-8428-6193c073838c.png)

## **第二步**：

进入 ’控制面板 ‘——>’程序‘——>’启用的Windows功能‘——>勾选Linux子系统（***根据提示进行重启计算机***）

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642668088848-7685043b-a966-4115-ac35-1c34ab0bc41a.png)

## **第三步**：

在Windows商店中下载**Ubuntu18.04**，进行安装。

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642668088889-342e3727-8b16-4297-9aae-764348054b97.png)

## **第四步**：**需要提醒的问题**

**第二步**中可能会出现重启之后，查看“*启用的功能*”时，*Linux子系统* 这个功能并未勾选上，这个**原因**可能是因为

**1、中途出现错误，所以你再重复勾选一遍进行安装组件，再重启一遍。2、可能是由于你的*****window运行库*****出现问题，这时候就需要利用软件修复一下计算机或者换个版本号（注意：是*****版本号*****不是*****版本*****，进行更新或者还原**）



## **第五步**：如果未出现上述问题，

大概这个过程是很顺利的；**重启之后，**你需要将你下载好的操作系统打开，根据运行框里面的步骤**输入用户名、密码。**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642668088873-01b7ba7c-0db1-4727-940d-6f189be4dc51.png)

## 第六步：通过cmd命令提示符打开

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642668088853-13686039-65ab-4e2a-af9a-7104c116ff95.png)

二、进行一些相关操作

**接下来会提一些少许Linux操作命令**

### **基础命令**

```
cd ~                      返回根目录
cd + 空格                  也可以返回根目录
cd + '..'                 返回上级目录
ls                        查看当前文件夹下有什么内容
掌握TAB键的一些使用
```



### 镜像源

```
准备镜像源，我这以阿里云镜像源做示范
阿里云镜像源：Ubuntu18.04
deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse


deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse


deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse


deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse


deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

```





### 更换镜像源

```
更换镜像源
sudo cp sources.list sources.list.bak      备份源文件（copy）   
cd /etc/apt/                                进入该文件目录下
ls                                          查看内容
vim sources.list                            用vim编辑器编辑镜像源
进入之后，通过快捷键进行操作
1、按下“G”                                    鼠标自动到第一行
2、接着按下“D”     
3、最后按下“shift + g”                        全盘清除
4、按下键键盘 “insert”                        进行输入内容
5、右击鼠标将复制的镜像源粘贴上去
6、按  “ESC”  键                              退出输入模式
7、输入 “ :wq ”                                 保存
8、cat sources.list                           查看镜像源
9、sudo apt-get update                        更新镜像源
10、sudo apt-get upgrade
     这个命令，会把本地已安装的软件，与刚下载的软件列表里对应软件进行对比，如果发现已安装的软件版本太低，就会提示你更新。如果你的软件都是最新版本，会提示：
     
```



### 编写你的C程序

```
如何运行C程序
进入你的操作系统界面
1、mkdir 名字                                    创建一个目录
2、cd  目录名                                    进入目录
3、touch demo.c                                 创建一个demo的c文件
使vim编辑器显示行号
4、cd ~                                          返回根目录
5、vim ~/.vimrc                          进入之后，开始输入set number保存
6、source ~/.vimrc                          
7、vim demo.c                                    编写c程序
安装编译器
8、sudo apt-get install gcc                      gcc编译插件
9、gcc -o demo demo.c                              编译
10、./demo                                        运行
```





### 后续还待探索…………………………
