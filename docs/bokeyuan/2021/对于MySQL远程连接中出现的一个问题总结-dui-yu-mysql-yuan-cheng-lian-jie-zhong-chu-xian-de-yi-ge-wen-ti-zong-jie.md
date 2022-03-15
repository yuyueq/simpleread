---
title: 对于MySQL远程连接中出现的一个问题总结
date: 2021-09-03 10:25:10.0
updated: 2022-01-20 17:44:51.463
url: /archives/dui-yu-mysql-yuan-cheng-lian-jie-zhong-chu-xian-de-yi-ge-wen-ti-zong-jie
categories: MySQL
tags: 问题记录
---

# 2021年9月3日更新补充

---

（**真的心累，本来是个小问题，但是网上帖子都基本差不多，基本都是相同的操作，导致搜了半个多小时才解决**）
**一、首先为什么要重新发一次呢，因为我发现上次写的这个记录是不完善甚至是错的，因为我忽略了一个操作，其次在今天再次去解决这个问题的时候，发现了一个比较正确的解决方法。下面我基本以上一次的内容为基础，因为上一次的内容仅仅完成了一部分的操作，并未解决真正的问题。也庆幸上次写的那篇随笔没有很多人去看，不然和网上的帖子一样会误导很多人，而且也成为了一篇没有用的帖子。**

**二、我会在每一个步骤上打上补充，避免误操作。而且希望一步步往下看，因为最后还会有一个根据这些网上普遍的操作总结出来的问题。**

---


**以下是上次文章内容，文章标题：记录"ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES/NO) ”错误**

---

# 前言

前段时间MySQL莫名的挂了，导致我数据都被清了，数据库也连不上；具体原因我也没去多看，今天顺便去搜了一下解决方法，没想到重置了一下密码竟然好了，但是数据还是被清了，有时间再去看看具体原因吧。
下面是我偶然搜到的一篇文章还是第一次这么顺利的解决了。

---

# 错误描述

首先这个问题我是在我的云服务器上遇见的，以前其实也遇到过，但经常是当时解决了，并未去记录，时间一长一些操作就忘了，但个人记得这个错误不管在Linux和Windows上都出现过，但是基本上相似，此篇记录主要针对Linux上的错误，在其中我也会提一些Windows上出现的问题。

---

# 解决方式
## 一、先停止mysql
```mysql
/etc/init.d/mysqld stop 
```
(如果已经查看了MySQL服务进程的话可以直接 kill -9 [PID] 杀死进程！）

## 二、执行以下命令，可以跳过登录验证

### 补充点
（补充一种方式，还是按照这个新方式来吧，也可以按照我上次写的方法来都行，就是第二种方式）：

可能有的人对下面的命令不理解，所以也可以采用这种方式
```
vim /etc/my.cnf                #输入这条命令去编辑这个文件
```
然后在文件中添加下面这段语句
```
[mysqld]
skip-grant-tables
```
**要注意的点来了，就是所有操作完毕后，记得把这句话给注释了（尽量是删除的时候给“skip-grant-tables”这句话之前添加一个“#”最为方便，不然每次都得重新输一遍这句话），不然你以为成功了，而我就是最傻的那个，原本以为成功了，今天才发现是这句话没有注释，直接让mysql跳过了验证，成功登录了，这种方式是极其不正确的！！！**

第二种方式：
```mysql
mysqld_safe --user=mysql --skip-grant-tables --skip-networking &
```

注意：如果在window上的话，我看很多文章去说找到“my.ini”文件，但对第一次使用mysql的人来说是大可能找不见的，如果可以的话可以去网上搜一下这个文件在哪。因为我当时是使用的解压缩的方式进行的安装，直接在文件夹中新建的这个文件，然后在当中去编辑以下内容,可以参考一下我的这篇记录：[MySQL巩固学习记录（一）](https://www.cnblogs.com/yuyueq/p/14626255.html "MySQL巩固学习记录（一）")
这是window上的安装配置文件内容：
```
[mysqld]
basedir=D:\Program Files\mysql-5.7\
datadir=D:\Program Files\mysql-5.7\data\
port=3306
skip-grant-tables #跳过登录验证
```

## 三、开始登录数据库(以root身份)

```mysql
mysql -u root -p
```

## 四、更新root用户密码

**MySQL5.7之前**
```mysql
UPDATE user SET Password=PASSWORD('你的密码') where USER='root';
```

**MySQL5.7之后（包括5.7）**
```mysql
UPDATE user SET authentication_string=PASSWORD('你的密码') where USER='root';
```
## 五、刷新权限

```mysql
FLUSH PRIVILEGES;
```

## 六、退出并重启

```mysql
mysql> exit

mysql> /etc/init.d/mysqld restart
```

## 七、重新登录

```mysql
mysql -uroot -p Enter password: <输入你刚才新设的密码>
```

## 八、结束

如果以上步骤如果不成功，多试一次，如果不行的话再换别的办法；至于window的话可能上面就跳过登录验证那块有点小问题，其他的话，我感觉window上解决问题比较容易一点，可以去博客园中搜搜看看，或者腾讯云社区搜搜看看，感觉这两个地方的解决方法稍微靠谱点。
**本文参考于**：https://cloud.tencent.com/developer/article/1188636

---


# 以上就是上次原文，重点来了
## 问题一：
你以为这就结束了，不不不，通常第一遍是忘了注释掉文件中的“skip-grant-tables”这句话，误以为成功了。
## 问题二：
当再次把这句话注释掉时，问题出来了，还是会和以前一样，出现“ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES/NO)”错误，当然在这里我也不知道和我情况一样的兄弟们有多少，所以下面我说说我的情况：问题再次出现，我去网上找解决方法，偶然看到有人说应该是mysql数据库中user表中缺数据着，也就是权限不够。所以我按着这条路下去，发现问题解决了。
## 具体解决方式如下：

## 一、去查看mysql数据库中user表
这是我安装的新的本地数据库中user的原始信息列之一也就是root用户
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210903151038809-1082567335.png)
那远程服务器上的怎么看？
**第一种方法**：把“skip-grant-tables”这句跳过权限验证在上面我提到的那个文件中加上，然后使用sql语句去查看。
**第二种方法**：依旧把上面这个语句加上，只不过这次我们在远程去看，也就是像Navicat这种图形化界面去看，看看到底自己表中信息是否缺失root用户信息。
## 二、把用户信息添加上
这里我直接使用的是我本地新装数据库中user表中的数据，root用户密码暂且设置为123456
sql文件直接放这了：https://files.cnblogs.com/files/yuyueq/user.zip
下面是源文件内容：
```sql
/*
 Navicat Premium Data Transfer

 Source Server         : wenxin.du
 Source Server Type    : MySQL
 Source Server Version : 50735
 Source Host           : localhost:3306
 Source Schema         : mysql

 Target Server Type    : MySQL
 Target Server Version : 50735
 File Encoding         : 65001

 Date: 03/09/2021 14:20:18
*/

SET NAMES utf8mb4;
SET FOREIGN_KEY_CHECKS = 0;

-- ----------------------------
-- Table structure for user
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user`  (
  `Host` char(60) CHARACTER SET utf8 COLLATE utf8_bin NOT NULL DEFAULT '',
  `User` char(32) CHARACTER SET utf8 COLLATE utf8_bin NOT NULL DEFAULT '',
  `Select_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Insert_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Update_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Delete_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Create_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Drop_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Reload_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Shutdown_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Process_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `File_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Grant_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `References_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Index_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Alter_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Show_db_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Super_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Create_tmp_table_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Lock_tables_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Execute_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Repl_slave_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Repl_client_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Create_view_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Show_view_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Create_routine_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Alter_routine_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Create_user_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Event_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Trigger_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `Create_tablespace_priv` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `ssl_type` enum('','ANY','X509','SPECIFIED') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT '',
  `ssl_cipher` blob NOT NULL,
  `x509_issuer` blob NOT NULL,
  `x509_subject` blob NOT NULL,
  `max_questions` int(11) UNSIGNED NOT NULL DEFAULT 0,
  `max_updates` int(11) UNSIGNED NOT NULL DEFAULT 0,
  `max_connections` int(11) UNSIGNED NOT NULL DEFAULT 0,
  `max_user_connections` int(11) UNSIGNED NOT NULL DEFAULT 0,
  `plugin` char(64) CHARACTER SET utf8 COLLATE utf8_bin NOT NULL DEFAULT 'mysql_native_password',
  `authentication_string` text CHARACTER SET utf8 COLLATE utf8_bin NULL,
  `password_expired` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  `password_last_changed` timestamp NULL DEFAULT NULL,
  `password_lifetime` smallint(5) UNSIGNED NULL DEFAULT NULL,
  `account_locked` enum('N','Y') CHARACTER SET utf8 COLLATE utf8_general_ci NOT NULL DEFAULT 'N',
  PRIMARY KEY (`Host`, `User`) USING BTREE
) ENGINE = MyISAM CHARACTER SET = utf8 COLLATE = utf8_bin COMMENT = 'Users and global privileges' ROW_FORMAT = Dynamic;

-- ----------------------------
-- Records of user
-- ----------------------------
INSERT INTO `user` VALUES ('localhost', 'root', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y', '', '', '', '', 0, 0, 0, 0, 'mysql_native_password', '*6BB4837EB74329105EE4568DDA7DC67ED2CA2AD9', 'N', '2021-08-30 11:57:05', NULL, 'N');
INSERT INTO `user` VALUES ('localhost', 'mysql.session', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'Y', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', '', '', '', '', 0, 0, 0, 0, 'mysql_native_password', '*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE', 'N', '2021-08-30 11:57:05', NULL, 'Y');
INSERT INTO `user` VALUES ('localhost', 'mysql.sys', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', '', '', '', '', 0, 0, 0, 0, 'mysql_native_password', '*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE', 'N', '2021-08-30 11:57:05', NULL, 'Y');

SET FOREIGN_KEY_CHECKS = 1;

```


## 三、解决最终问题
运行之后还是会发现一个问题，就是当把跳过权限验证语句注释掉之后，虽然远程服务器通过ssh连接操作时，mysql可以连接上不再出现那个问题，但是当远程连接服务器上的mysql时问题出现了，它没有远程连接的权限，这是因为我们刚才的文件中也是设置了。所以解决方法我找到了一篇博文：
> 解决Navicat 出错:1130-host . is not allowed to connect to this MySql server,MySQL
>1. 改表法。
可能是你的帐号不允许从远程登陆，只能在localhost。这个时候只要在localhost的那台电脑，登入mysql后，更改 "mysql" 数据库里的 "user" 表里的 "host" 项，从"localhost"改称"%"
![image](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210903153000890-371107942.png)
mysql -u root -p
mysql>use mysql;
mysql>update user set host = '%' where user = 'root';
mysql>select host, user from user;
注：个人觉得不太适用！

>2. 授权法。

>i.你想myuser使用mypassword从任何主机连接到mysql服务器的话。
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'%' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
FLUSH   PRIVILEGES;

>ii.如果你想允许用户myuser从ip为192.168.1.6的主机连接到mysql服务器，并使用mypassword作为密码
GRANT ALL PRIVILEGES ON *.* TO 'myuser'@'192.168.1.3' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
FLUSH   PRIVILEGES;

>iii.如果你想允许用户myuser从ip为192.168.1.6的主机连接到mysql服务器的dk数据库，并使用mypassword作为密码
GRANT ALL PRIVILEGES ON dk.* TO 'myuser'@'192.168.1.3' IDENTIFIED BY 'mypassword' WITH GRANT OPTION;
FLUSH   PRIVILEGES;

>我用的 i 方法,最后执行一个语句 mysql>FLUSH RIVILEGES 使修改生效.就可以了
另外一种方法,不过我没有亲自试过的,在csdn.net上找的,可以看一下.
在安装mysql的机器上运行：
1、d:/mysql/bin/>mysql   -h   localhost   -u   root  //这样应该可以进入MySQL服务器
2、mysql>GRANT   ALL   PRIVILEGES   ON   *.*   TO   'root'@'%'   WITH   GRANT   OPTION  //赋予任何主机访问数据的权限
3、mysql>FLUSH   PRIVILEGES  //修改生效
4、mysql>EXIT  //退出MySQL服务器
这样就可以在其它任何的主机上以root身份登录啦！



## 四、方法总结
最简单的错误就是，数据都在，然后单纯连接不上，通过修改密码可以连接。其次就是和我一样的错误，需要先跳过验证，然后重新修改表中缺失数据，然后给远程数据库授权可以远程连接，最后注释掉那跳语句，然后以后就可以通过正常的方式连接数据库了。

# 最后
篇幅也不算长，都是些个人话语，其实整体步骤很简单，只不过我想说的是，粗心大意有时候就是问题的所在，因为有时候原本一个很简单的问题，由于自己的疏忽导致迟迟未解决。还有就是CSDN中的解决错误的文章真的太水了，大多都是搬运，不加以修改，都是一模一样的，很难找到有效信息，所以还是建议像Stack Overflow、思否、博客园、这些论坛上去搜索问题，相对来说稍微比CSDN靠谱点。
