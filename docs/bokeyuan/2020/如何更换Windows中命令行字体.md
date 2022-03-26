



# 前言

CMD（命令提示符），全称“Command Prompt”；对于这个东西我相信大部分用电脑的人基本都知道，因为常常会用到一些基本的DOS命令进行一些电脑的基本查看处理；但是我相信一些用这个东西的人其实有一种苦恼，那就是“**字体**”；这个“**字体**”不管是在win7还是win10中，它的样子仅仅只有那么几种，而且大部分的字体都还是**中文体；比如：**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793098-fa426e09-5a1d-4490-b5ea-e250fbe1f817.png)

**图中可以看出对于英文还是差不多的，但是在第二个黄框中我敲得是一个冒号和一个分号**

***你确定你不仔细看得话能看出来？***

可能有些人不觉得什么，但对于一些编程人员或者对字体这方面有自己独特感觉的人来说是真的难受（当然像开发人员、搞编程的人他们都有自己独有的终端工具，一般不会用windows自带的这种）；那总体来说的话，这它自带的这个字体是真的有它自己的缺陷！**那么怎样简单的解决这个问题呢？跟我来，仅仅只需三步！**



# **步骤一：**

**方法一：在win10任务栏中，点击“搜索框”按钮，输入“regedit”**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793035-1a2d2fd2-d4f3-419f-8d0f-309182265fc8.png)

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793114-452103a5-ec97-4087-aaec-474f711cad32.png)

**方法二、使用快捷键“win+R”键，然后输入“regedit”，打开注册表**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793123-194df865-dabf-49fc-8b4e-0de549c46c80.png)![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793114-8e295cc9-fb53-425e-8f2d-9a378b4529fb.png)

# 步骤二：

☛HKEY_CURRENT_USER\Console\%SystemRoot%_system32_cmd.exe

修改二进制项CodePage的值为十进制437（十六进制1b5）；

修改字符串值FaceName可以设置默认的字体。![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793705-9ca70556-ebbb-43c7-a705-c1887f89ddf1.png)



2.☛再进入注册表，按此路径再进行设置

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVesion\Console\TrueTypeFont

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793728-d82a928e-1642-4859-b40a-816104d043cb.png)



要增加字体其实也很简单，在注册表中[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\Console\TrueTypeFont]项下增加一项名字为000的字符串值，并将其值设置为你想要用的字体的名字，如果要增加更多字体只要再增加一项字符串值，并将其命名为0000，也就是多加一个0即可。上图中我增加了一个名为Consolas的字体（数值数据），你可以选择任何你想用的字体，当然了必须是系统中已经有的。

# 步骤三：

**使用快捷键“win+R”键，输入“cmd”；**

**进入命令提示符窗口；**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793706-520d10ce-b62f-4136-92c7-68c76756b61a.png)![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793750-24edda32-9680-4367-a2d8-92dd63c14a53.png)



**有没有发现使用编程字体的话，是不是更好的进行操作了！**



# **最后**

**分享一款微软等宽字体：** ***Cascadia Code PL***

下载地址： https://dwx-frank.lanzous.com/ifZYFed2wgh

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672793952-e2dafb80-2770-4cf6-ac99-da23b2ae13a4.png)



![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672794170-2d0cd910-2604-47c9-b4ac-e45652127abc.png)



![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672794371-386ed175-6f24-41b4-b5cb-7b488d872989.png)





**这款字体也可以添加到CMD中的字体选项栏哦！具体方法同上！**





# 题外话：

**我自己呢，使用的终端工具也是很常见的两种工具**

**第一个：XShell**

**这个我就具体不多说了，方便Linux操作的一款终端工具，大多数人都知道；要下载的话可以直接去官网上下载。**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672794439-47a976c3-e05d-4477-99a6-857480947497.png)

**第二个：Cmder；具体样子如下图，喜欢折腾的人可以试着用一下，我个人觉得还行。**

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642672794515-3a773243-0ed5-4091-b0ae-70dc51f9106c.png)