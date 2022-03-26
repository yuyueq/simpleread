> Git的一些操作
参考自狂神说Git视频，如果需要简单入门的话，看他的那个视频我感觉够了。

---

**2021年9月3日 新增学习Git文档网站**

**Progit**：https://www.progit.cn/#_pro_git

**Gitbook**: https://git-scm.com/book/zh/v2

**CSNote：http://www.cyc2018.xyz/%E5%85%B6%E5%AE%83/%E7%BC%96%E7%A0%81%E5%AE%9E%E8%B7%B5/Git.html**

**在线实践网站：https://learngitbranching.js.org/?locale=zh_CN**

**JavaGuide：https://snailclimb.gitee.io/javaguide/#/docs/tools/Git**

---




# 一、相关配置文件

```
\etc\gitconfig  ：Git 安装目录下的 gitconfig     --system 系统级
C:\Users\Administrator\ .gitconfig    只适用于当前登录用户的配置  --global 全局
```
**注意**：这里的Administrator是当前用户名，也就是你开机用户名，有的人可能设置了自己的用户名，所以路径有所不同,不然有的人找不到。
一般你的“用户”文件夹都是这些内容：

![image](https://unleashed.oss-cn-beijing.aliyuncs.com/win10yuyueq/2031154-20210901135546560-49197056.png)

---

# 二、查看配置

## 查看系统config
```
 git config --system --list
 ```

## 查看当前用户（global）配置

```
 git config --global --list
 ```

## 查看配置

```
git config -l
```
## 查看不同级别的配置
```
git config --global user.name "yuyueq" #名称
git config --global user.email 123456789@qq.com #邮箱
```

---

# 三、操作命令

## 克隆一个项目和它的整个代码历史(版本信息)
```
git clone [url]
```
## 查看指定文件状态
```
git status [filename] 
```
## 查看所有文件状态
```
git status 
```
## 添加所有文件到暂存区
注意“add”后面的小点
```
 git add .
 git commit -m "消息内容"    提交暂存区中的内容到本地仓库 -m 提交信息
```

## 列出所有本地分支
```
git branch 
```
## 列出所有远程分支
```
git branch -r 
```
## 新建一个分支，但依然停留在当前分支
```
git branch [branch-name] 
```
## 新建一个分支，并切换到该分支
```
git checkout -b [branch] 
```
## 合并指定分支到当前分支
```
git merge [branch] 
```
## 删除分支
```
git branch -d [branch-name] 
```
## 删除远程分支
```
git push origin --delete [branch-name] 
git branch -dr [remote/branch]
```
---

# 四、生成密钥

进入 C:\Users\Administrator\.ssh 目录(注意上面说的文件路径问题)
生成公钥
```
ssh-keygen
```
---

# 五、忽略文件

> 有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等
在主目录下建立 ".gitignore" 文件，此文件有如下规则：
1.忽略文件中的空行或以井号（#）开始的行将会被忽略。
2.可以使用 Linux 通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。
3.如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。
4.如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。
5.如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）


---

# 六、Idea操作
可以去看看这篇文章：https://www.cnblogs.com/tomingto/p/11727920.html

其实基本都是比较简单的操作，基本是commit和push。而且每次需要代码的更新也都是些这些操作

# 最后
像这些内容其实网上也有很多文章去解释，而且比较全面，我这里仅做一个基本命令的记录，避免有时候记不起来找不到相关命令。
贴一张图（**如有侵权，联系立删！**）：
![image](https://unleashed.oss-cn-beijing.aliyuncs.com/win10yuyueq/2031154-20210901140009211-1526956693.png)
