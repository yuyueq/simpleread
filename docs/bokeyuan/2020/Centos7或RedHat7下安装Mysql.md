
# 一次简单的Mysql安装记录

## 前言

<font size =4>由于网上安装Mysql的方式有很多种，但有些方式并未安装成功，比如用Yum源，还待后续查看具体是哪一步出了问题</font>

---

## 以rpm包的形式安装Mysql

### 第一步：yum install wget -y		

<font size =4>//安装wget工具</font>

---

### 第二步: 以tar包形式拉取下载并进行解压

<font size =4>1.用wget拉取下载：</font>

<font size =4>wget http://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.12-1.el6.x86_64.rpm-bundle.tar</font>

<font size =4>2.进行解压（个人是解压在/usr/local/src/mysql目录下）：</font>

<font size =4>tar -xvf mysql-5.7.12-1.el6.x86_64.rpm-bundle.tar</font>

<font size =4>图片参考：</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201102223925339-1063831368.png)

---

### 第三步：安装

<font size =4>**注意：在结尾加上 --nodeps --force  该字段，该功能为取消依赖安装。且按以下顺序安装！！**</font>

<font size =4>1.rpm -ivh mysql-community-common-5.7.12-1.el6.x86_64.rpm --nodeps --force</font>

<font size =4>2.rpm -ivh mysql-community-libs-5.7.12-1.el6.x86_64.rpm --nodeps --force</font>

<font size =4>3.rpm -ivh mysql-community-client-5.7.12-1.el6.x86_64.rpm --nodeps --force</font>

<font size =4>4.rpm -ivh mysql-community-server-5.7.12-1.el6.x86_64.rpm --nodeps –force</font>

---

### 第四步：启动mysql服务，并且查看服务状态

<font size =4>1.启动：systemctl start mysqld</font>

<font size =4>2.查看状态：systemctl status mysqld</font>

<font size =4>3.成功之后：图片参考</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201102223948449-1163660151.png)

---

### 第五步：查看Mysql默认密码

<font size =4>1.查看Mysql日志</font>

<font size =4>grep 'temporary password' /var/log/mysqld.log</font>

<font size =4>2.图片参考</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201102224009180-497761200.png)

---

### 第六步：修改默认密码

<font size =4>1.修改密码sql语句（修改用户名为‘root‘的密码为’123456‘）</font>

<font size =4>ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';</font>

<font size =4>2.假如修改失败，出现如下提示信息“ERROR 1819 (HY000): Your password does not satisfy the current policy requirements”，请继续以下两条sql语句，如果修改成功可忽略以下两条sql语句</font>

<font size =4>2.1设置 validate_password_policy 的全局参数为 LOW  :  set global validate_password_policy=LOW;</font>

<font size =4>2.2 设置全局参数为 6 ： set global validate_password_length=6;</font>

<font size =4>2.3 重新更改 ALTER USER 'root'@'localhost' IDENTIFIED BY '123456';</font>

---

### 第七步：登录Mysql 

### 最后:学会查看错误日志

<font size =4>由于个人原因，在第二次查看mysql服务和启动服务时，出现错误提示。特此记录!</font>

<font size =4>1.查看错误日志：cat  /var/log/mysqld.log</font>

<font size =4>2.如出现图中错误可以采用以下方式解决</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201102224026603-715614475.png)


<font size =4>2.1  mkdir -p /var/run/mysqld</font>

<font size =4>2.2  chown mysql.mysql /var/run/mysqld</font>

<font size =4>2.3 最后，重启mysql服务</font>

<font size =4>3.虽然服务启动成功了，但是当连接mysql时又出现一个错误，如下图</font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201103082828484-619563504.png)


<font size =4>3.1 先查询自己的mysql.sock:  find / -name mysql.sock  (个人参考图) </font>
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201103083424017-129992276.png)
<font size =4>3.2 然后在 my.cnf 中添加指定 mysql.sock文件 ，在最后一行加入以下内容。（该路径为个人路径）</font>
`[mysql]`
`no-auto-rehash`
`socket = /var/lib/mysql/mysql.sock`

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20201103083618108-558073854.png)

---

<font size =4>**4.总结：如果未出现图中错误，要学会查看错误日志并且解决它！！并且要注意每个人遇到的问题不一样，一定先要冷静下来仔细分析错误，然后再寻找解决问题的方案。**</font>