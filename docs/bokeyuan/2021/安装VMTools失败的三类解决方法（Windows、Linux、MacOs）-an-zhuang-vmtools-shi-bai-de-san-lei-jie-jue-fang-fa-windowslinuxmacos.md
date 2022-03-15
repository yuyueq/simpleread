---
title: 安装VMTools失败的三类解决方法（Windows、Linux、MacOs）
date: 2020-07-31 17:14:48.0
updated: 2022-01-21 11:16:27.635
url: /archives/an-zhuang-vmtools-shi-bai-de-san-lei-jie-jue-fang-fa-windowslinuxmacos
categories: 安装配置 | 计算机 | Linux
tags: 问题记录 | Windows
---

# 前言 

写这篇笔记的原因，是前几天在虚拟机 ***Vmware*** 中重新安装了几个操作系统，突然发现 ***VMTools*** 这个工具成了一个特殊的问题，以前还没有发现，因为通常它就给你自动安装了。但是大多数时候也是需要手动安装的，不管是 ***VirtualBox*** 还是 ***VMware*** 虚拟机，对于云上的虚拟机那就不必了，你直接用就行了。 

说一点我使用这两个虚拟机的想法： 

前两个虚拟机软件也是我使用比较多的，个人感觉 ***VirtualBox*** 轻巧（而且我觉得 ***VirtualBox*** 和 ***windows自带的Hyper-V*** 虚拟功能是很像的），便携，就比较适合一些小内存的计算机，比如一些 **8GB** 的低压笔记本，虽然使用 **VMWare** 比较好一点点，但是两者差得也不是太多，要注重内容，那对于 **VirtualBox** 一般你按正常步骤走的话，“ ***增强工具*** ”一般是很容易安装的， 但是这个 ***Vmware*** 上我感觉不怎么友好，经常性的会出一些问题，这仅仅是对于这个虚拟机的“ ***增强工具*** ”而言的，说起虚拟机本身相比于 ***VirtualBox*** 还是有很多的优点的，比如：性能优化、系统配置、易管理性、界面美观等等。 

---

反正还是要记录一下这次在 ***VmWare*** 上 ***增强性工具VMTools*** 的安装，以后也会搜集一些资料关于 ***VirtualBox*** 的内容。 
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731174747605-672043918.jpg)


# 一、Windows上出现的问题 

**要注意！！！** 

**安装之后必须重启才有效** 

# 官方步骤即解决方法 

>**前提条件** 
>1、 开启虚拟机。 
>
>>2、确认客户机操作系统正在运行。 
>>3、如果您在安装操作系统时将虚拟机的虚拟 CD/DVD 驱动器连接到了 ISO 映像文件，请更改设置，将虚拟 CD/DVD 驱动器配置为自动检测物理驱动器。自动检测设置能让虚拟机的第一个虚拟 CD/DVD 驱动器检测并连接到 VMware Tools 安装的 VMware Tools ISO 文件。您的客户机操作系统会将该 ISO 文件检测为一张物理 CD。使用虚拟机设置编辑器将 CD/DVD 驱动器设置为自动检测物理驱动器。 
>>4、如果您使用的不是旧版的 Windows 操作系统，请以管理员身份登录。任何用户都可以在 Windows 95、Windows 98 或 Windows ME 客户机操作系统中安装 VMware Tools。如果您的操作系统版本高于上述版本，则必须以管理员身份登录。 
>>5、AppDefense 组件不会默认安装。您必须进行自定安装并加入该组件。 
>>**过程** 
>>1、在主机上，从 VMware Fusion 菜单栏中选择 **虚拟机 > 安装 VMware Tools** 。 
>>如果安装了早期版本的 VMware Tools，则菜单项是 **更新 VMware Tools** 。 
>>2、如果首次安装 VMware Tools，请在“安装 VMware Tools”信息页中点按 **好** 。 
>>如果在客户机操作系统中为 CD-ROM 驱动器启用了自动运行，则会启动 VMware Tools 安装向导。 
>>如果未启用自动运行，要手动启动向导，请点按 **开始 > 运行** ，然后输入 **D:\setup.exe** ，其中 **D:** 是第一个虚拟 CD-ROM 驱动器。对于 64 位 Windows 客户机操作系统，请使用 **D:\setup64.exe** 。 
>>3、按照屏幕上的提示进行操作。 
>>4、如果显示新硬件向导，请按照提示进行操作并接受默认选项。 

---


# 网上的解决方法 

---

*关于上述的方法，就是我们常会忽略的“帮助内容”，上面的东西可以说是正常情况，所以说80%没什么卵用，所以主要还是* ***注意特殊问题*** *！* 

# Windows7 

## 问题一：安装程序无法继续，本程序需要您将此虚拟机上安装的操作系统更新到SP1 

： *下面这张图是网上找的，因为我当时的问题也解决了但没截屏，如果本人看到，如需删除，请联系本人立马删除！* 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173517044-1539852809.png)



对于这个问题我当时也是搜了很多资料，但最后得出的唯一结论：不要折腾了， **直接换windows镜像源** 来的快一点，毕竟是个虚拟机嘛，搞几个都可以，如果有自己的兴趣可以自行搜索解决。 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173558810-602250816.png)



# Windows7 镜像 

也可以使用一些我放这的链接（注意：都是64位的）： 

**家庭高级版** 

>**文件名** cn_windows_7_home_premium_with_sp1_x64_dvd_u_676691.iso 
>**SHA1** BB5A8A1480FE54C497601AA1DC7BE698A784BE1C 
>**文件大小** 3.19GB 
>**发布时间** 2011-05-12 
>
>>ed2k://|file|cn_windows_7_home_premium_with_sp1_x64_dvd_u_676691.iso|3420557312|1A3CF44F3F5E0BE9BBC1A938706A3471|/ 

**企业** **版** 

>**文件名** cn_windows_7_enterprise_with_sp1_x64_dvd_u_677685.iso 
>**SHA1** 9BA5E85596C2F25BE59F7E96139D83D4CB261A62 
>**文件大小** 3.04GB 
>**发布时间** 2011-05-12 
>
>>ed2k://|file|cn_windows_7_enterprise_with_sp1_x64_dvd_u_677685.iso|3265574912|E9DB2607EA3B3540F3FE2E388F8C53C4|/ 

**专业版** 

>**文件名** cn_windows_7_professional_with_sp1_x64_dvd_u_677031.iso 
>**SHA1** 9B57E67888434C24DD683968A3CE2C72755AB148 
>**文件大小** 3.19GB 
>**发布时间** 2011-05-12 
>
>>ed2k://|file|cn_windows_7_professional_with_sp1_x64_dvd_u_677031.iso|3420557312|430BEDC0F22FA18001F717F7AF08C9D5|/ 

**最终版本** 

>**文件名** cn_windows_7_ultimate_with_sp1_x64_dvd_u_677408.iso 
>**SHA1** 2CE0B2DB34D76ED3F697CE148CB7594432405E23 
>**文件大小** 3.19GB 
>**发布时间** 2011-05-12 
>
>>ed2k://|file|cn_windows_7_ultimate_with_sp1_x64_dvd_u_677408.iso|3420557312|B58548681854236C7939003B583A8078|/ 

---


## 问题二、VMTools工具栏是灰色的 

*关于这个问题我感觉是很容易解决的，可以参考下面的这篇文章，进行解决。* 

[     ](https://zhuanlan.zhihu.com/p/67964401)[https://zhuanlan.zhihu.com/p/67964401](https://zhuanlan.zhihu.com/p/67964401)

[https://blog.csdn.net/weixin_44251723/article/details/100537943](https://blog.csdn.net/weixin_44251723/article/details/100537943)

---

*一般就这两个问题，如果有别的问题，一般都是虚拟机硬件没设置合适的缘故* 

# Windows10 

## 问题一、安装程序无法继续。Microsoft Runtime。安装程序未能安装 

***可以参考下面这篇博文：*** 

[https://blog.csdn.net/qq_26462567/article/details/102459725](https://blog.csdn.net/qq_26462567/article/details/102459725)
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173712428-1829042213.png)



**然后按照步骤做** 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173725793-1581259317.png)



**在打开的文件窗口中，找到末尾为 “~setup”的文件夹，一般在第一个** ： 

>以下作为参考（来源网络）： 
>1、在弹出的窗体中找到一个文件名中含‘{132E3257-14F1-411A-BC6C-0CA32D3A9BC6}~setup’的文件夹，打开里面会看到有 xxx.msi的，运行就开始vmware的安装了 
>
>>2、找到{ADC3121A-3EBA-4016-AF64-00B8FE017080}~setup结尾是~setup(在打开运行时不要管了安装界面，看一下当时的时间，很容易找到的，关闭找不到) 

---


## 问题二、您无权输入许可证密钥。请使用系统管理员帐户重新尝试。 

*这个我具体没碰到过，但看这个错误应该是又系统造成的* 

*以下是网上的解决方案，如侵权，联系删！* 

[https://blog.csdn.net/zl0601/article/details/84065575](https://blog.csdn.net/zl0601/article/details/84065575)

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173809540-1663468543.png)
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173828394-1992391800.png)
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173839482-1099101911.png)


---


# 二、MacOS上出现的问题 

# 问题： 

---

## 无法在更新服务器上找到组件。请联系VMware技术支持或您的系统管理员。 

# 官方步骤即解决方法 

>**前提条件** 
>开启虚拟机。 
>确认客户机操作系统正在运行。 
>**过程** 
>在主机上，从 VMware Fusion 菜单栏中选择 **虚拟机 > 安装 VMware Tools** 。 
>如果安装了早期版本的 VMware Tools，则菜单项是 **更新 VMware Tools** 。 
>在 VMware Tools 虚拟光盘上打开 **安装 VMware Tools** ，按照安装程序助理的提示进行操作，然后点按 **好** 。 
>**结果** 
>将重新启动虚拟机以使 VMware Tools 生效。 

---

## 

# 网上的解决方法 

对于这个官方的解决方法，其实大多数时候，对我们只是初步性的指示，而并没有收集各种问题，俗话说的好“高手在民间”，所以 **多利用搜索引擎** 给你想要的答案，前提是你会用，会找“答案”。 

如果不会用，可以看看我的这一篇笔记： 

[如何（正确）使用搜索引擎？使用搜索引擎的高效技巧（例如：百度、谷歌）](https://www.cnblogs.com/unleashed/p/13301955.html)

**进入正题：** 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173900892-935543484.png)



# 重点： 

**这个问题的出现，应该是因为 darwin.iso 文件** **，而这时候问题救出现了：darwin 是什么？来参考一下维基百科上的内容** 
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173910603-1601283178.png)



**再来百度一下：** 
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173918439-491170883.png)



具体也就是这个样子，所以接下来你要 **手动安装** 这个文件 

（建议参考以下两篇博文： **为你的VMware 15.5 MacOS手动安装VMware Tools：** 

[https://qianfanguojin.github.io/2020/01/12/%E4%B8%BA%E4%BD%A0%E7%9A%84VMware-15-5-MacOS%E6%89%8B%E5%8A%A8%E5%AE%89%E8%A3%85VMware-Tools/](https://qianfanguojin.github.io/2020/01/12/%E4%B8%BA%E4%BD%A0%E7%9A%84VMware-15-5-MacOS%E6%89%8B%E5%8A%A8%E5%AE%89%E8%A3%85VMware-Tools/)

---

[VMWare15.0手动为Mac OS10.14虚拟机安装VMWare Tools](https://www.cnblogs.com/MakeView660/p/11273999.html)**；里面的内容是很详细的！** **）** 

里面比较重要的是： 

**找好相对合适的darwin文件** 
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173933432-1156501279.png)



**虽然网上步骤说的是直接添加这个darwin.iso文件，但是我并没用添加成功，而且桌面也没有弹出来，可能最好的效果就是弹出来VMTools安装界面；如果没有弹出来，我们也可以进行添加** 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731173958405-1687753160.png)



**重启，** 

那最后要注意的是：在VMTools安装过程中，会弹出来有关 **安全的设置** ，这时候 **记得不能点”好“** 

**然后进去下图界面，选择”允许“** 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731174017698-1021391541.png)



**基本按照此步骤，90%的问题可以解决** 

---


# 三、Linux上出现的问题 

首先，肯定有人说”虚拟机上玩LInux没有灵魂“，但是一般到头来只能说“真香”，因为实在是太方便了！便于我们学习与开发；还有想说的是，个人感觉Linux上出问题其实比我们常用的这两种操作系统好解决一点，其次感觉Liunx和开源精神会蓬勃发展。 

那进入正题（主要是安装方式不同导致出的问题）： 

# 官方步骤即解决方法 

>**前提条件** 
>1、开启虚拟机。 
>2、确认客户机操作系统正在运行。 
>3、因为 VMware Tools 安装程序是使用 Perl 编写的，请确认已在客户机操作系统中安装 Perl。 
>**过程** 
>1、在主机上，从 Workstation Pro 菜单栏中选择 **虚拟机 > 安装 VMware Tools** 。 
>如果安装了早期版本的 VMware Tools，则菜单项是 **更新 VMware Tools** 。 
>2、在虚拟机中，打开终端窗口。 
>3、运行不带参数的 mount 命令，以确定 Linux 发行版是否已自动挂载 VMware Tools 虚拟 CD-ROM 映像。 
>如果已挂载 CD-ROM 设备，则将采用类似于以下输出的形式列出 CD-ROM 设备及其挂载点： 
>/dev/cdrom on /mnt/cdrom type iso9660 (ro,nosuid,nodev) 
>
>>4、如果未挂载 VMware Tools 虚拟 CD-ROM 映像，请挂载 CD-ROM 驱动器。 
>>如果挂载点目录尚不存在，请创建该目录。 
>>mkdir /mnt/cdrom 
>>某些 Linux 发行版使用不同的挂载点名称。例如，一些发行版的挂载点是 /media/VMware Tools，而不是 /mnt/cdrom。修改该命令以反映您的发行版所使用的约定。 
>>挂载 CD-ROM 驱动器。 
>>mount /dev/cdrom /mnt/cdrom 
>>某些 Linux 发行版使用不同的设备名称或采取不同的方式组织 /dev 目录。如果 CD-ROM 驱动器不是 /dev/cdrom，或者如果 CD-ROM 的挂载点不是 /mnt/cdrom，请修改该命令以反映您的发行版所使用的约定。 
>>5、转到工作目录，例如 /tmp。 
>>`cd /tmp` 
>>6、（可选）在安装 VMware Tools 之前，删除以前的任何 vmware-tools-distrib 目录。 
>>此目录的位置取决于在先前安装期间指定的位置。通常情况下，此目录位于 /tmp/vmware-tools-distrib 中。 
>>7、列出挂载点目录的内容，并记下 VMware Tools tar 安装程序的文件名。 
>>ls mount-point 
>>8、解压缩安装程序。 
>>tar zxpf /mnt/cdrom/VMwareTools-x.x.x-yyyy.tar.gz 
>>值 x.x.x 是产品版本号，yyyy 是产品版本的内部版本号。 
>>9、如有必要，请卸载 CD-ROM 映像。 
>>umount /dev/cdrom  
>>如果 Linux 发行版已自动挂载 CD-ROM，则不需要卸载该映像。 
>>10、运行安装程序并以 root 用户身份配置 VMware Tools。 
>>cd vmware-tools-distrib 
>>sudo ./vmware-install.pl 
>>通常，在安装程序文件结束运行后，将运行 vmware-config-tools.pl 配置文件。如果尝试在 RPM 安装的基础上执行 tar 安装，或者在 tar 安装的基础上执行 RPM 安装，安装程序将检测到先前的安装，并且必须转换安装程序数据库格式，然后才能继续。 
>>**注：** 
>>对于较新的 Linux 发行版，系统会提示用户选择集成的 open-vm-tools。 
>>11、如果适合您的配置，请按照提示接受默认值。 
>>12、按照脚本结尾处的说明进行操作。 
>>根据使用的功能，这些说明可能包括重新启动 X 会话、重新启动网络连接、重新登录以及启动 VMware 用户进程。或者，也可以重新引导客户机操作系统以完成所有这些任务。 
>>**后续步骤** 
>>如果虚拟机具有新的可用虚拟硬件版本，请升级虚拟硬件。 

---


# **我的解决方法：** 

可以将VMtools移动到桌面，然后进行解压 

![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731174034275-1645885810.png)



或者你可以直接用命令行 
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731174042626-539191847.png)



然后输入命令 

| 因为这第一种方式是利用了图形界面，所以文件也被我们提取到桌面了，接下来就开始输入命令 |
| :----------------------------------------------------------- |
| 1、输入     cd Desktop/                  进入桌面（注意书写时的空格） |
| 2、输入      ls                                   会发现有解压的那个文件 |
| 3、输入     cd Vm+Tab键                 进入到解压的文件里   |
| 4、输入      sudo ./vmware-install.pl           开始安装（一路回车加yes） |

---

要提醒的是：  操作以 **root用户** 权限进行；如果未更换镜像源或者更新软件，请参考我的这篇笔记 [https://www.cnblogs.com/unleashed/p/13193852.html](https://www.cnblogs.com/unleashed/p/13193852.html)当中有提到具体方法 

# 网上的解决方法 

*网上主要是在命令行中安装以及运行* 

**<1> 以root身份登陆计算机** 

**<2> 开始安装Vmware** 

选择VM-->install VMware Tools 

**<3> 输入如下命令** 

```plain
mkdir /mnt/cdrom         书写时注意空格 
mount /dev/cdrom /mnt/cdrom/ 
```

**<4>进入目录** 

```plain
cd /mnt/cdrom/  
ls 
```

**<5>将文件拷贝至根目录下的tmp这个临时目录下** 

```plain
可以复制粘贴 右击 
cp VMwareTools-10.3.10-13959562.tar.gz /tmp  
```

**<6>进入tmp文件夹** 

```plain
 cd /tmp/ 
 tar zxvf VMwareTools-10.3.10-13959562.tar.gz  进行解压文件 
```

**<7>** **安装** 

```plain
 cd vmware-tools-distrib 
 ls 
 ./vmware-install.pl   
```

其次呢，还会出现 **安装失败的问题** ，应该是系统已经有了一个，可以利用 **命令** 把原来的 **删除了** 。 

---

再者就是和MacOS里面出现的问题一样， **缺少Linux.iso。** 

# 最后 

**通过这次总结，其实我发现可能每个人遇到的问题差不多，就看一个人解决问题的态度，所以不要害怕有问题，有问题才说明成功不是很容易的事。还有就是，解决问题的方法是相对问题而言的，所以常常就会忽略一个隐藏的问题：我们每个人往往会用不同操作方式，这导致我们的问题没法解决，所以还是当问题出现时，先排查掉自己所犯的所有错误，再来寻找解决问题的方法，这样高效又容易留印象！** 
**再附张动漫唯美艺术美图**
![](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/2031154-20200731174628229-238772322.jpg)