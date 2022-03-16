# 给网站装上SSL证书

# 前言

主要是因为自己的阿里云快过期了，自己的博客也重新用了一下Halo，重新安装SSL的时候有些地方忘了，所以在此留个记录！

# 关于SSL

**阮一峰《图解图解SSL/TLS协议》**：https://www.ruanyifeng.com/blog/2014/09/illustration-ssl.html

## SSL证书是什么？

> SSL 证书是一个数字证书，用于认证网站的身份并启用加密连接。SSL 代表安全套接字层，这是一个安全协议，可在 Web 服务器和 Web 浏览器之间创建加密链接。
>
> 公司和组织需要在其网站上添加 SSL 证书，以保护在线交易并保持客户信息的私密性和安全性。
>
> 简而言之：SSL 可确保互联网连接的安全，并防止犯罪分子读取或修改两个系统之间传输的信息。如果您在地址栏中的 URL 旁看到一个挂锁图标，则表示 SSL 在保护您正在访问的网站。
>
> 自 SSL 协议在约 25 年前发布以来，已经有多个版本问世，所有这些版本在某些时候都会遇到安全性方面的难题。随后出现了经过修改和重命名的版本 - TLS（传输层安全性），至今仍在使用。但是，首字母缩写 SSL 早已深入人心，因此该协议的新版本通常仍在使用这一旧名称

## 为什么需要 SSL 证书

> 网站需要 SSL 证书来确保用户数据的安全，验证网站的所有权，防止攻击者创建虚假网站版本，以及将信任传达给用户。
>
> 如果网站要求用户登录、输入个人详细信息（例如其信用卡号）或查看机密信息（例如，健康福利或财务信息），则必须对数据保密。SSL 证书有助于保持在线互动的私密性，并向用户保证该网站是真实可靠的，可以与其共享私密信息。
>
> 与企业更相关的事实是，HTTPS Web 地址需要 SSL 证书。HTTPS 是 HTTP 的安全形式，这意味着 HTTPS 网站的流量通过 SSL 进行了加密。大多数浏览器将 HTTP 网站（没有 SSL 证书的网站）标记为“不安全”。这向用户发出了一个明确的信号，即该网站可能不值得信任，这有助于敦促尚未迁移到 HTTPS 的企业执行迁移。
>
> SSL 证书有助于保护信息，例如：
>
> - 登录凭据
> - 信用卡交易或银行账户信息
>
> - 个人身份信息 - 例如全名、地址、出生日期或电话号码
> - 法律文档和合同
>
> - 病历
> - 专有信息

## SSL 证书如何工作？

>SSL 的原理是确保用户和网站之间或两个系统之间传输的任何数据始终无法被读取。它使用加密算法对传输中的数据进行加密，从而防止黑客读取通过连接发送的数据。该数据包括潜在的敏感信息，例如姓名、地址、信用卡号或其他财务详细信息。
>
>该过程如下所示：
>
>浏览器或服务器尝试连接到使用 SSL 保护的网站（即 Web 服务器）。
>
>浏览器或服务器请求 Web 服务器证明自己的身份。
>
>作为响应，Web 服务器向浏览器或服务器发送它的 SSL 证书的副本。
>
>浏览器或服务器检查以了解是否信任 SSL 证书。如果信任，它将向 Web 服务器发出信号。
>
>然后，Web 服务器返回经过数字签名的确认，以启动 SSL 加密会话。
>
>加密数据在浏览器或服务器与 Web 服务器之间共享。
>
>此过程有时称为“SSL 握手”。虽然这个过程听起来似乎很漫长，但实际发生时只有几毫秒。
>
>
>
>当网站具备 SSL 证书保护时，首字母缩写 HTTPS（代表安全超文本传输协议）会显示在 URL 中。如果没有 SSL 证书，则只会显示字母 HTTP（即没有代表安全的 S）。URL 地址栏中也会显示一个挂锁图标。这表示信任，并向那些访问该网站的人提供了保证。
>
>
>
>要查看 SSL 证书的详细信息，可以单击浏览器栏中的挂锁符号。SSL 证书中通常包括的详细信息包括：
>
>针对其颁发证书的域名
>
>颁发给哪个人、组织或设备
>
>哪个证书颁发机构颁发了证书
>
>证书颁发机构的数字签名
>
>关联的子域
>
>证书的颁发日期
>
>证书的到期日期
>
>公钥（不公开私钥）

引用：《什么是 SSL 证书 – 定义和解释》：https://www.kaspersky.com.cn/resource-center/definitions/what-is-a-ssl-certificate

------

# 开始安装

**参考自水哥的公众号**：https://mp.weixin.qq.com/s/IaIGnFmfRZ8ODOCJuiLciQ

B站搜“不高兴就喝水”，水哥的公众号中的文章还是很肝的！目前没有沦陷！


## 1、进入阿里云点击立即购买，选择免费的

对于购买可以参考官方文档：https://help.aliyun.com/document_detail/156645.html

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642666628533-11061f37-ec78-4a9b-ba87-b41f26ddcb97.png)

## 2、审核通过后，进入控制台下载

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642666876600-55cb245f-cc93-4341-b500-80b98ec9bbd0.png)

得到两个文件

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642667032924-471f107d-4b12-4df2-a6ee-fb4a2a90405c.png)

## 3、上传文件

```java
#进入Nginx默认安装目录。如果您修改过默认安装目录，请根据实际配置进行调整。
cd /usr/local/nginx/conf
#创建证书目录，命名为cert。然后把证书丢里头
mkdir cert
```

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642667255063-b3931668-44ab-47a8-9f01-d33ebccce735.png)

## 4、在nginx.conf中加入以下内容

（不要改原有的sever，这只不过是新加的一个模块，注意看原有文件中注释的内容，方便理解），输入“vim nginx.conf”进行编辑，写完后按键盘“ESC”健输入“:wq”即完成保存退出。

关于Vim可以看一下我以前做的一些记录：

https://www.cnblogs.com/yuyueq/p/14022693.html (文末有一些vim操作)

https://www.cnblogs.com/yuyueq/p/13193852.html （Vim设置行号）

```java
server {
    listen 443 ssl;
    #配置HTTPS的默认访问端口为443。
    #如果未在此处配置HTTPS的默认访问端口，可能会造成Nginx无法启动。
    #如果您使用Nginx 1.15.0及以上版本，请使用listen 443 ssl代替listen 443和ssl on。
    server_name www.yzfree.com;
    #把www.yzfree.com替换成你自己的域名
    #需要将yourdomain.com替换成证书绑定的域名。
    root html;
    index index.html index.htm;
    ssl_certificate cert/5452872_www.yzfree.com.pem;  #需要将cert-file-name.pem替换成已上传的证书文件的名称。
    ssl_certificate_key cert/5452872_www.yzfree.com.key; #需要将cert-file-name.key替换成已上传的证书密钥文件的名称。
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    #表示使用的加密套件的类型。
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2; #表示使用的TLS协议的类型。
    ssl_prefer_server_ciphers on;
    location / {
        proxy_pass  http://localhost;
      }
    }
```

## 5、进行编译重启

如果最后失败，要注意nginx.conf配置文件的正确性，以及下面1到5的步骤，不成功则重复1到5这个步骤

```java
1.切换到源码包下

# cd /usr/local/src/nginx-1.18.0

2.生成makefile(如果你的目录下没有“configure”是不成功的)：

# ./configure --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module

3.配置完成后，运行命令编译：

# make

make命令执行后，不要进行make install，否则会覆盖安装。

4.备份原有已安装好的nginx：

# cp /usr/local/nginx/sbin/nginx /usr/local/nginx/sbin/nginx.bak

5.停止nginx状态：

# /usr/local/nginx/sbin/nginx -s stop

6.将编译好的nginx覆盖掉原有的nginx：

# cd /usr/local/src/nginx-1.18.0

# cp ./objs/nginx /usr/local/nginx/sbin/

7.提示是否覆盖，输入yes即可。

8.然后启动nginx：

# /usr/local/nginx/sbin/nginx

9.进入nginx/sbin目录下，通过命令查看模块是否已经加入成功：

# cd /usr/local/nginx/sbin/

# ./nginx -V

10.显示以下信息，则证明已经编译成功：
nginx version: nginx/1.6.2
built by gcc 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC) 
TLS SNI support enabled
configure arguments: --prefix=/usr/local/nginx --with-http_stub_status_module --with-http_ssl_module
```

## 6、最后

网站改用https便可成功访问，至于以上步骤对于初学者来说一般会有问题，所以可以参考一些这些文章

**nginx: [emerg] the "ssl" parameter requires ngx_http_ssl_module in /usr/loc**：https://www.cnblogs.com/ghjbk/p/6744131.html

jar包后台启动：

https://cloud.tencent.com/developer/article/1722069

window和Linux关闭端口：

https://www.cnblogs.com/yuyueq/p/14787857.html


# 我的网站

![img](https://unleashed.oss-cn-beijing.aliyuncs.com/picgo/1642668847062-e6099e6a-44f3-4e27-bb58-f892fdcead4c.png)













