> 通过短链生成二维码并上传七牛云(Java)

# 前言

网上这种帖子其实也是很多，大部分搜出来的是CSDN的，然后点进去一看都几乎一样；所以这次给个自己实践的例子记录。
这次也是通过搜索得到的一部分能实现这个功能的代码，其实大体差不多，本地上传比较简单，但是上传服务器需要新的参数传递。
随笔最后再附上一些分享的内容

---


## 参考部分

**1、首先通过传过来的长链接去生成短链，然后通过短链去生成二维码，将生成的二维码存储到七牛云，然后将图片地址存放到数据库中**。
**2、生成二维码方式：**
**I.引用外部包qrcode.jar实现**
**II.以见最多的com.google.zxing这个包去实现**
**III.以Hutool这个工具包去实现（参见官网：https://www.hutool.cn/docs/#/）**

**3、参考文章**：
I.[**二维码生成并上传至七牛云 返回图片URL**](https://blog.csdn.net/wub116/article/details/86555193?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-5.control&spm=1001.2101.3001.4242)
II.[**Java使用QRCode.jar生成与解析二维码demo**](https://www.cnblogs.com/bigroc/p/7496995.html)
III.[**Java 生成二维码上传第三方平台（详解）**](https://blog.csdn.net/qq_36537546/article/details/88525214?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_title~default-0.control&spm=1001.2101.3001.4242)


---

# 长短链转换

这块的话网上解释较多实现也较为容易，在这提供一些参考内容
**短链接服务系统开发：https://www.javadoop.com/post/url-shortener#toc_1**
（最基本的实现方式，随机生成；具体去做这么一个模块的话，就得自己去写了，理是这么个理！）
**Gitee参考开源代码：https://gitee.com/tinyframework/urlshorter**

---

# 代码
## 生成二维码
在这里采取第二种方式实现（zxing包），当然也可以采用hutool工具包中的生成方法，它的生成方法也有很多种可以被我们使用。
## pom.xml(部分代码)
```xml
   <!--七牛云-->
        <dependency>
            <groupId>com.qiniu</groupId>
            <artifactId>qiniu-java-sdk</artifactId>
            <version>7.2.9</version>
        </dependency>
        <!-- 二维码生成-->
        <dependency>
            <groupId>com.google.zxing</groupId>
            <artifactId>core</artifactId>
            <version>3.3.3</version>
        </dependency>

        <dependency>
            <groupId>com.google.zxing</groupId>
            <artifactId>javase</artifactId>
            <version>3.3.3</version>
        </dependency>
```

## QrCodeUtils.java（生成二维码）

```java
import cn.hutool.extra.qrcode.QrCodeUtil;
import com.google.zxing.BarcodeFormat;
import com.google.zxing.EncodeHintType;
import com.google.zxing.MultiFormatWriter;
import com.google.zxing.WriterException;
import com.google.zxing.common.BitMatrix;
import net.liangyihui.shorturl.exception.ShortUrlException;
import org.apache.commons.lang3.StringUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.ByteArrayOutputStream;
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;

/**
 * <p>
 *
 * </p>
 *
 * @author wenxin.du
 * @since 2021/9/6
 */

@Component
public class QrCodeUtils {

    @Autowired
    private static QiniuUploadUtils qiniuUploadUtils;

    private static final Logger logger = LoggerFactory.getLogger(QrCodeUtils.class);

    private static final int BLACK = 0xFF000000;

    private static final int WHITE = 0xFFFFFFFF;

    public String qrCodeCreate(String text) {

        Map<EncodeHintType, String> his = new HashMap<EncodeHintType, String>();

        his.put(EncodeHintType.CHARACTER_SET, "utf-8");
        try {
            BitMatrix encode = new MultiFormatWriter().encode(text, BarcodeFormat.QR_CODE, 300, 300, his);
            int codeWidth = encode.getWidth();
            int codeHeight = encode.getHeight();
            BufferedImage image = new BufferedImage(codeWidth, codeHeight, BufferedImage.TYPE_INT_RGB);
            for (int i = 0; i < codeWidth; i++) {
                for (int j = 0; j < codeHeight; j++) {
                    image.setRGB(i, j, encode.get(i, j) ? BLACK : WHITE);
                }
            }
            image.flush();
            ByteArrayOutputStream os = new ByteArrayOutputStream();
            ImageIO.write(image, "jpg", os);
            String result = qiniuUploadUtils.uploadFilesViaServer(os); 
            //通过七牛云工具类调用上传方法，将定义的这个流传给它
            //返回结果通过定义一个参数接收，判断它是否空白，不是则返回结果给这个二维码创建方法
            if (StringUtils.isNotBlank(result)) {
                return result;
            } else {
                logger.info("QrCodeUtils.generateQrCodeThenUpload ======== 二维码生成错误，请稍后重试！========");
                throw new ShortUrlException("二维码生成错误，请稍后重试！");
            }
        } catch (WriterException e) {
            e.printStackTrace();
            System.out.println("二维码生成失败");
        } catch (IOException e) {
            e.printStackTrace();
            System.out.println("生成二维码图片失败");
        }
        return null;
    }
}
```



## AppConfig.java(采用配置文件方式)

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;


@Component
public class AppConfig {

    @Value("${qiniu.access.key}")
    private String QINIU_ACCESS_KEY;

    @Value("${qiniu.secret.key}")
    private String QINIU_SECRET_KEY;

    @Value("${qiniu.bucket.key}")
    private String QINIU_BUCKET_KEY;

    @Value("${qiniu.bucket.image.url}")
    private String QINIU_BUCKET_IMAGE_URL;

    public String getQINIU_ACCESS_KEY() {
        return QINIU_ACCESS_KEY;
    }

    public String getQINIU_SECRET_KEY() {
        return QINIU_SECRET_KEY;
    }

    public String getQINIU_BUCKET_KEY() {
        return QINIU_BUCKET_KEY;
    }

    public String getQINIU_BUCKET_IMAGE_URL() {
        return QINIU_BUCKET_IMAGE_URL;
    }
}
```

## application-dev.yml

```yaml
## ---------------七牛相关配置，自行配置-----------------
qiniu:
  access: 
    key: 
  secret:
    key: 
  bucket:
    key: 
    image.url: 
```



## QiniuUploadUtils.java(七牛云上传)

```java
import com.google.gson.Gson;
import com.qiniu.common.QiniuException;
import com.qiniu.common.Zone;
import com.qiniu.http.Response;
import com.qiniu.storage.Configuration;
import com.qiniu.storage.UploadManager;
import com.qiniu.storage.model.DefaultPutRet;
import com.qiniu.util.Auth;
import net.liangyihui.shorturl.common.constant.AppConfig;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import java.io.ByteArrayInputStream;
import java.io.ByteArrayOutputStream;
import java.io.InputStream;
import java.util.UUID;


/**
 * <p>
 * 上传七牛云
 * </p>
 *
 * @author wenxin.du
 * @since 2021-09-07
 */
@Component
public class QiniuUploadUtils {

    @Autowired
    private AppConfig appConfig;

    public String uploadFilesViaServer(ByteArrayOutputStream os) {
        String retKey = "";
        Configuration cfg = new Configuration(Zone.zone2());
        UploadManager uploadManager = new UploadManager(cfg);
        String uuid = UUID.randomUUID().toString();
        String key = uuid.replace("-", "") + ".jpg";
        Auth auth = Auth.create(appConfig.getQINIU_ACCESS_KEY(), appConfig.getQINIU_SECRET_KEY());
        String upToken = auth.uploadToken(appConfig.getQINIU_BUCKET_KEY());
        InputStream byteInputStream = new ByteArrayInputStream(os.toByteArray());
        try {
            Response response = uploadManager.put(byteInputStream, key, upToken, null, null);
            DefaultPutRet putRet = new Gson().fromJson(response.bodyString(), DefaultPutRet.class);
            System.out.println("key: " + appConfig.getQINIU_BUCKET_IMAGE_URL() + putRet.key);
            System.out.println("hash: " + putRet.hash);
            retKey = appConfig.getQINIU_BUCKET_IMAGE_URL() + putRet.key;
        } catch (QiniuException ex) {
            Response r = ex.response;
            System.err.println(r.toString());
            try {
                System.err.println(r.bodyString());
            } catch (QiniuException ex2) {
                //ignore
            }
        }
        return retKey;
    }
}

```

---

## 数据库、controller层

像这两个层面就比较好办了，都是通过方法的调用去实现，不管是用的什么框架，只能说框架越流行越新，那它实现起来较为比以前的方式更为方便点。
个人感觉框架就是为了业务开发的方便性，以及解耦；但基础没打稳，框架只能是会用，但不知道原理，也体会不到框架的意义。

---

# 分享

也是在学习的时候，发现有些网站内容还不错，可以作为java学习的参考；还有就是以下没有打广告的嫌疑，毕竟人家也不需要我这种菜鸟打广告，只是单纯觉得好用！

**程序员导航（有各类网站）：http://tooool.org/**

![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908135938484-1504738874.png)

**面试哥（各种资源贼全）：http://www.mianshigee.com/**
里面还有很多内容
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908140105360-654328977.png)

**帅地玩编程（一个比较不错面试问题集合）：https://www.iamshuaidi.com/**
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908140353331-1416312786.png)


**JavaGuide（从B站上看到的，也算是自己长期看的一个网站了）：https://snailclimb.gitee.io/javaguide/#/**
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908141041560-2105207494.png)


**也是一个学习网站：http://www.cyc2018.xyz/**
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908141131733-169834376.png)

**学习网站加一：https://veal98.gitee.io/cs-wiki/#/README?id=%e5%85%ac%e4%bc%97%e5%8f%b7**
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908141154800-736339264.png)

**一个人的博客（还可以）：https://www.javadoop.com/**
![](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210908141101534-968191951.png)
