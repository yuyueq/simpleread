> Elasticsearch、XXLJob以及最近的学习记录

---

# 前言
在这九月的最后一周，来总结一下最近的学习记录，主要是对于Elasticsearch、XXLjob的初步学习，想着还是多记录点，以便后面去看看，具体的错误认知点在哪，以及找到一些自己的认识点。
  
---
 
# 后台数据脱敏

## 一、普通方式
首先该功能是基于Spring Boot项目做的，所以这是一个简单的流程。
具体实现：首先设定一个角色code，比如 “涉密人员” “secret”；
通过登录时获取token中的用户名然后通过用户名去获取他的角色code，同时去动态的获取涉密人员的角色code（即做判断的时候不能写死，从数据库中获取），
然后将他们的code做判断；

  ```java
import cn.hutool.core.util.StrUtil;
import com.baomidou.mybatisplus.core.conditions.query.LambdaQueryWrapper;
import lombok.extern.slf4j.Slf4j;
import org.apache.commons.lang3.StringUtils;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import javax.servlet.http.HttpServletRequest;
import java.util.List;

/**
 * <p>
 *
 * </p>
 *
 * @author yuyueq
 * @since 2021/9/13
 */
@Component
@Slf4j
public class JudgeSecret {
    //TODO
    @Autowired
    private BosuserIdentityService bosuserIdentityService;

    @Autowired
    private BosRoleService bosRoleService;

    public Boolean judgingSecret(HttpServletRequest servletRequest) {
        boolean flag = false;
        String token = JwtTokenUtil.getToken(servletRequest);
        String username = JwtUtil.getUsername(token);
        //做角色code获取并进行判断
        for (*:*) {
            if (role.getId().equals(sRole.getId())) {
                flag = true;// 是涉密员
                break;
            }
        }
        return flag;
    }

    public String mobileReplace(String mobile) {
        if (StrUtil.isNotBlank(mobile)) {
            return mobile.replaceAll("(\\d{3})\\d{4}(\\d{4})", "$1****$2");
        } else {
            return "-";
        }
    }

    public String nameReplace(String name) {
        if (StrUtil.isNotBlank(name)) {
            return StringUtils.rightPad(StringUtils.left(name, 1), StringUtils.length(name), "*");
        } else {
            return "-";
        }
    }

}
  ```
 
## 二、Spring AOP实现
只需要给serviceImpl加EncryptMethod注解，以及在需要加密的字段加上EncryptMobileField、EncryptNameField注解

```java

package net.liangyihui.dhbos.aspect;

import cn.hutool.core.util.ReflectUtil;
import com.baomidou.mybatisplus.extension.plugins.pagination.Page;
import lombok.extern.slf4j.Slf4j;
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.context.request.RequestAttributes;
import org.springframework.web.context.request.RequestContextHolder;

import javax.servlet.http.HttpServletRequest;
import java.beans.PropertyDescriptor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

/**
 * @ClassName : ServiceAspect
 * @Author : yuyueq
 * @Date: 2021/9/18 14:23
 * @Description :
 */
@Slf4j
@Configuration
@Aspect
public class ServiceAspect {

    private final String ExpGetResultDataPoint = "@annotation(位置)";

    @Autowired
    private JudgeSecret judgeSecret;

    @Pointcut(ExpGetResultDataPoint)
    public void EncryptMethod() {

    }

    @Around("EncryptMethod()")
    public Object doAroundAdvice(ProceedingJoinPoint proceedingJoinPoint) {
        log.info("环绕通知的目标方法名：" + proceedingJoinPoint.getSignature().getName());
        processInputArg(proceedingJoinPoint.getArgs());
        try {//obj之前可以写目标方法执行前的逻辑
            Object obj = proceedingJoinPoint.proceed();
            processOutPutObj(obj);
            return obj;
        } catch (Throwable throwable) {
            throwable.printStackTrace();
        }
        return null;
    }

    /**
     * 处理返回对象
     */
    private void processOutPutObj(Object object) {
        RequestAttributes requestAttributes = RequestContextHolder.getRequestAttributes();
        HttpServletRequest servletRequest = (HttpServletRequest) requestAttributes.resolveReference(RequestAttributes.REFERENCE_REQUEST);
        boolean flag = !judgeSecret.judgingSecret(servletRequest);
        if (flag) {
            if (object instanceof Page) {
                //page
                Page page = (Page) object;
                page.getRecords().forEach(o -> {
                    try {
                        Field[] fields = o.getClass().getDeclaredFields();
                        for (Field field : fields) {
                            encrypt(field, o);
                        }
                    } catch (Exception e) {
                        log.info("反射错误" + e);
                    }
                });
            } else {
                try {
                    Class clazz = object.getClass();
                    Field[] fields = ReflectUtil.getFieldsDirectly(clazz, true);
                    for (Field field : fields) {
                        field.setAccessible(true);
                        String proType = field.getGenericType().toString();
                        if (proType.contains("class java.lang")
                                || proType.contains("class java.math.")
                                || proType.contains("class java.util")) {
                            encrypt(field, object);
                        } else if ("byte".equals(proType) || "short".equals(proType) || "int".equals(proType) || "long".equals(proType) || "double".equals(proType) || "float".equals(proType) || "boolean".equals(proType)) {
                            encrypt(field, object);
                        } else if (proType.startsWith("java.util")) {
//                            if (field.getGenericType() instanceof ParameterizedType) {
//                                Class newClazz = (Class) ((ParameterizedType) field.getGenericType()).getActualTypeArguments()[0];
//                                Object obj = newClazz.newInstance();
//                                processOutPutObj(obj);
//                            }
                        } else if (field.getType().isArray()) {
                            //属性是数组类型则遍历

                        } else {
                            //class类型的遍历
                            PropertyDescriptor descriptor = new PropertyDescriptor(field.getName(), clazz);
                            Method method = descriptor.getReadMethod();
                            Object obj = method.invoke(object);
                            if (null != obj) {
                                processOutPutObj(obj);
                            }
                        }
                    }
                } catch (Exception e) {
                    e.printStackTrace();
                    log.info("脱敏加密失败" + e);
                }
            }
        }
    }

    private Field encrypt(Field field, Object obj) {
        try {
            if (field.isAnnotationPresent(EncryptMobileField.class)) {
                field.setAccessible(true);
                Object value = field.get(obj);
                if (value instanceof Long || value == null) {
                    field.set(obj, null);
                } else {
                    field.set(obj, judgeSecret.mobileReplace(value.toString()));
                }
            }
            if (field.isAnnotationPresent(EncryptNameField.class)) {
                field.setAccessible(true);
                Object value = field.get(obj);
                if (value != null) {
                    field.set(obj, judgeSecret.nameReplace(value.toString()));
                } else {
                    field.set(obj, null);
                }
            }
        } catch (IllegalAccessException e) {

        }
        return field;
    }

    /**
     * 处理输入参数
     *
     * @param args 入参列表
     */
    private void processInputArg(Object[] args) {
//        for (Object arg : args) {
//            System.out.println("ARG原来为:" + arg);
//        }
    }
}

```

### 以上根据以下文章学习所得

[Springboot（二十一）@Aspect 切面注解使用](https://blog.csdn.net/u012326462/article/details/82529835)

[注解Annotation实现原理与自定义注解例子](https://www.cnblogs.com/acm-bingzi/p/javaAnnotation.html)

[什么是反射机制？反射机制的应用场景有哪些?](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/%E5%8F%8D%E5%B0%84%E6%9C%BA%E5%88%B6)

[代理模式详解：静态代理+JDK/CGLIB 动态代理实战](https://snailclimb.gitee.io/javaguide/#/docs/java/basis/%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F%E8%AF%A6%E8%A7%A3)

---
 
 
# Elasticsearch学习

## 参考笔记链接

这块的话是简单入了个门，所以我是在B站上找的“狂神说”的视频，至于视频中的笔记，网上也是一搜一大堆
这里的话贴一个比较全面的笔记链接：https://blog.csdn.net/qq_21197507/article/details/115076913

## 体会

初次安装运行体验，感觉整体很像数据库，所以比较好上手，然后目前是未感受到它的魅力，毕竟还未在
实际项目中使用，但是感觉这个技术还是挺强的。

RestfulApi:https://restfulapi.cn/

MVP：https://choerodon.io/zh/blog/mvp/

图图图图图图图
 
---
 
# ES仿京东搜索Demo

我的仓库地址：https://gitee.com/yuyueq/esjd



---

# XXLJob学习 

这块的话还是分享我所看到的文章，毕竟我也是根据这些文档跟着学的

### 了解xxljob
[再见 Spring Task，这个定时任务框架真香！](https://mp.weixin.qq.com/s/dXXAukYdfyU-U1KSSdQLsg)
正巧还是今天发的

[在Spring Boot中优雅的实现定时任务](https://zhuanlan.zhihu.com/p/79644891)

### 入门xxljob
[Spring Job？Quartz？XXL-Job？年轻人才做选择，艿艿全莽~](https://mp.weixin.qq.com/s/jqN4noo5NazckPCehWFgpA)

[官方文档](https://www.xuxueli.com/xxl-job/#%E3%80%8A%E5%88%86%E5%B8%83%E5%BC%8F%E4%BB%BB%E5%8A%A1%E8%B0%83%E5%BA%A6%E5%B9%B3%E5%8F%B0XXL-JOB%E3%80%8B)




---

# 最近看到的一些文章分享

[羊哥最近看了上百封简历，发现很多小可爱技术词汇都乱拼](https://mp.weixin.qq.com/s/q5gPSIiJqVvbI6Xa4dMXwA)

[Layui的落幕，是否预示一个时代的结束？](https://www.cnblogs.com/mqingqing123/p/15329717.html)

其实看到官网通知很及时，因为我当时正在看文档，没想到出了事，个人还是很意外吧，毕竟自己才刚开始
打算去学着用，因为是感觉挺方便的，虽然没有vue和elementUI的好，但各有各的好处吧，只不过就是有点遗憾
没有早接触作者这么优秀的技术作品。


[java学成什么样子可以出去实习？](https://www.zhihu.com/question/324692823/answer/1995317884)

[熟练掌握 MyBatis-Plus，这一篇就够了！](https://mp.weixin.qq.com/s/fnoRa3zNcTp_3wFC3UENXw)

[Spring最常用的7大类注解，史上最强整理！](https://mp.weixin.qq.com/s/6XIYt6GrU81RD7chOxf5ow)

[何为架构？](https://www.cnblogs.com/wyq178/p/12151160.html)

[简单说一下Kafka](https://mp.weixin.qq.com/s/v72-lh5W_L34sd3OtCrvlg)

[简单吹一下微服务](https://mp.weixin.qq.com/s/rFHLt_jKLIsKTpP1OcxY6w)



# 最后
基本上也就这些内容了，所以接下来，还要通过一些的实践内容去体会这些技术，不然仅仅只是看过而已。
共勉！
“他乡纵有当头月，不及家乡一盏灯”


