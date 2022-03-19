# 前言
首先会做这次记录，也是因为自己也是第一次去接触这个框架，以前总是听说，并没有去用过。这次出于实习的原因，去学习了一下Layui这个“面向后端开发者的框架”。其次，此篇记录仅供参考，毕竟我也不是开发者，所以不能保证文章引用的内容以及自己的理解是否正确，请自行决断一些内容的正确性。
前段时间看到一个不错的博客是个人写的关于前端面试的还是比较全面基础的（虽然个人是后端，但是如果有学前端的看到这篇随笔，可以当做参考一下）
在这里贴出来：
【**GitHub**】：https://github.com/WindrunnerMax/EveryDay
【**博客**】https://blog.touchczy.top/#/

---

# Layui

**官方文档**：https://www.layui.com/doc/
**官方示例**：https://www.layui.com/demo/
**Gitee**：https://gitee.com/sentsin/layui
**GitHub**：https://github.com/sentsin/layui

# 简介
做总结的时候才发现其实自己要总结的点还是比较少的，因为官方文档已经说的很详细了，所以在此我想说的是，目前个人用的多的还是像组件这类东西，毕竟现在基本都是封装之后的东西，而且这些封装过后的东西也是用的比较多比较爽的，还有就是Gitee上有一个开源模板"Layuimini",个人感觉作为后台BOSS的模板还是挺不错的，毕竟大部分人觉得layui比amazeui稍微好看一点点（不过还是出于真心，各有各的好，有的人也觉得amazeui更好看一点，至于官网地址自己可以搜搜看，我放文章后面了）。
像框架、工具这类的东西，感觉直接看官网文档是来的较快而且比较权威的。

**【开源仓库】Layuimini**：https://gitee.com/zhongshaofa/layuimini

---

>内容摘抄于官方文档中——入门指南篇

> layui（谐音：类 UI) 是一套开源的 Web UI 解决方案，采用自身经典的模块化规范，并遵循原生 HTML/CSS/JS 的开发方式，极易上手，拿来即用。其风格简约轻盈，而组件优雅丰盈，从源代码到使用方法的每一处细节都经过精心雕琢，非常适合网页界面的快速开发。layui 区别于那些基于 MVVM 底层的前端框架，却并非逆道而行，而是信奉返璞归真之道。准确地说，它更多是面向后端开发者，你无需涉足前端各种工具，只需面对浏览器本身，让一切你所需要的元素与交互，从这里信手拈来。

> layui 定义为「经典模块化」，并非是自吹她自身有多优秀，而是有意避开当下 JS 社区的主流方案，试图以尽可能简单的方式去诠释高效！她的所谓经典，是在于对返璞归真的执念，她以当前浏览器普通认可的方式去组织模块！我们认为，这恰是符合当下国内绝大多数程序员从旧时代过渡到未来新标准的绝佳指引。所以 layui 本身也并不是完全遵循于 AMD 时代，准确地说，她试图建立自己的模式

```javascript
//layui 模块的定义（新 js 文件）
layui.define([mods], function(exports){
  
  //……
  
  exports('mod', api);
});  
 
//layui 模块的使用
layui.use(['mod1', 'mod2'], function(args){
  var mod = layui.mod1;
  
  //……
  
}); 
```

> 没错，她具备早前 AMD 的影子，又并非受限于 CommonJS 的那些条条框框，layui 认为这种轻量的组织方式，比WebPack更符合绝大多数场景。所以她坚持采用经典模块化，也正是能让人避开工具的复杂配置，回归简单，安静高效地编织原生态的 HTML/CSS/JS。

> 但是 layui 又并非是 RequireJS 那样的模块加载器，而是一款 UI 解决方案，与 BootStrap 的不同又在于：layui 糅合了自身对经典模块化的理解。这使得你可以在 layui 组织的框架之内，以更具可维护性的代码、去更好的编织丰富的用户界面

---

# JavaScript模块化开发

> 早期的Javascript是作为浏览器的脚本语言，使用![image](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210902143703781-257805269.png)标签直接引入，没有所谓的模块化。也就是说如果我们需要一个js文件，我们就加一个![image](https://img2020.cnblogs.com/blog/2031154/202109/2031154-20210902143718425-469794106.png)标签，把需要的js引入进来。这种方式的特点在于：简单粗暴。
但是当项目越来越大，依赖越来越多时可能就会出现问题，比如逻辑越来越混乱，页面也越复杂，然后可维护性就变差了，除此之外还存在全局变量暴露、文件的引入顺序的问题。比如说一个文件引入另一个文件，另一个文件又依赖另一个文件，那么这三个加载数据就会很重要，如果第一个没有加载完，那么接下来就会出错。
实际上，在JavaScript的发展历史上，第一个真正模块化的是nodejs，nodejs就是使用了我们其中的一个模块化标准的规范，它就是common js。
有了这个模块化的概念后，便有了node，node的文件管理都是基于模块化的；我们可以从另一个角度来看，如果JavaScript想要进军服务端，在服务端没有模块化这是一个灾难，因此common js社区制定了一个commonjs规范，也就是模块化的规范；有了这个规范之后，node就出现了。

>JavaScript引入模块化解决了哪些问题：
避免了全局污染
模块复用，提高了开发效率和协作
模块功能单一职能方便维护
解决了文件依赖顺序
模块化的标准（有三个）：
CommonJs
AMD - 异步模块
CMD - 通用模块

>AMD (异步模块定义Asynchronous Module Definition)格式的最终目的是提供一个当前开发者能使用的模块化Javascript方案。它出自于Dojo用XHR+eval的实践经验，这种格式的支持者想在以后的项目中避免忍受过去的这些弱点
AMD是"Asynchronous Module Definition"的缩写，意思就是"异步模块定义"。由于不是JavaScript原生支持，使用AMD规范进行页面开发需要用到对应的库函数，也就是大名鼎鼎RequireJS，实际上AMD 是 RequireJS 在推广过程中对模块定义的规范化的产出
它采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。
RequireJS主要解决两个问题
多个js文件可能有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器
js加载的时候浏览器会停止页面渲染，加载文件越多，页面失去响应时间越长


> CommonJS模块建议指定一个简单的用于声明模块服务器端的API，并且不像AMD那样尝试去广泛的操心诸如io，文件系统，约定以及更多的一揽子问题。
这种形式为CommonJS所建议--它是一个把目标定在设计，原型化和标准化Javascript API的自愿者工作组。迄今为止，他们已经在模块和包方面做出了批复标准的尝试
根据CommonJS规范:
1.一个单独的文件就是一个模块。每一个模块都是一个单独的作用域，也就是说，在该模块内部定义的变量，无法被其他模块读取，除非定义为global对象的属性。
2.输出模块变量的最好方法是使用module.exports对象。
3.加载模块使用require方法，该方法读取一个文件并执行，返回文件内部的module.exports对象

> CMD 即Common Module Definition通用模块定义，CMD规范是国内发展出来的，就像AMD有个requireJS，CMD有个浏览器的实现SeaJS，SeaJS要解决的问题和requireJS一样，只不过在模块定义方式和模块加载（可以说运行、解析）时机上有所不同

**最后可参考这些文章（仔细甄别内容正确性，因为我也是做了个参考，并未保证这些文章百分百正确）：
[前端模块化](https://www.cnblogs.com/dolphinX/p/4381855.html "前端模块化")**，
[**谈谈我的理解-组件化/模块化**](https://www.jianshu.com/p/79e4df63f31f "谈谈我的理解-组件化/模块化")，
[**对前端工程化、模块化、组件化开发的理解**](https://blog.csdn.net/candyHZhou/article/details/108071230 "对前端工程化、模块化、组件化开发的理解")。



---

# 前端框架官方文档
##【[Vue.js](https://cn.vuejs.org/)】
```
https://vuejs.bootcss.com/guide/
https://cn.vuejs.org/
```
##【[ElementUI](https://element-plus.gitee.io/#/zh-CN "ElementUI")】
```
https://element-plus.gitee.io/#/zh-CN
```

##【[Layui](https://www.layui.com/ "Layui")】
```
https://www.layui.com/
```

####【[妹子UI（amazeui）](http://amazeui.shopxo.net/ "妹子UI（amazeui）")】
```
http://amazeui.shopxo.net/
```
##【[Semantic UI](https://semantic-ui.com/ "Semantic UI")】
```
https://semantic-ui.com/
```
##【[EasyUI](https://www.jeasyui.net/ "EasyUI")】
```
https://www.jeasyui.net/
```
##【[BootStrap](https://www.bootcss.com/ "BootStrap")】
```
https://www.bootcss.com/
```
##【[Bootstrap可视化布局](https://www.bootcss.com/p/layoutit/ "Bootstrap可视化布局")】
```
https://www.bootcss.com/p/layoutit/
```
