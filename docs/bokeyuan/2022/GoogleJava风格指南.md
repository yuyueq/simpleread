---
title: Google Java 风格指南(Google Java Style Guide)
date: 2022-01-18 19:08:16.0
updated: 2022-01-20 17:44:10.622
url: /archives/googlejavafeng-ge-zhi-nan-googlejavastyleguide
categories: Java
tags: 资源 | Java
---

**注**：文章由于在博客园上阅读页面带点卡顿，所以在此发了一下，可能是由于我在博客园的博客自定义设置影响整体页面的加载。

官方地址 [google.github.io](https://google.github.io/styleguide/javaguide.html#s4.8.8-numeric-literals)

本文档作为 Google 的 Java™ 编程语言源代码编码标准的完整定义。当且仅当它遵守此处的规则时，Java 源文件才被描述为 Google 风格。

# 前言
> 声明：在原文挡基础上做了一次翻译并总结了一下具体内容，换了一下排版样式等等。

在此也参考了另外一篇已经有很长时间的翻译版：https://hawstein.com/2014/01/20/google-java-style/

要提一点的是，国内的话可能更熟悉阿里的开发手册[📎Java开发手册（嵩山版）.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12423125/1642496086731-e0491cc2-72c4-44d0-a4db-8bf1e3591aa0.pdf)或者《Effective Java》
（Gitee：[https://gitee.com/lin-mt/effective-java-third-edition](https://gitee.com/lin-mt/effective-java-third-edition) 
在线网阅读的一个网站:[https://www.mianshigee.com/tutorial/effective-java-3rd-chinese/docs-readme.md](https://www.mianshigee.com/tutorial/effective-java-3rd-chinese/docs-readme.md)   ）

所以Google的开发规范可能不怎么熟悉，甚至和我一样有点感觉不习惯。毕竟只是一种形式而已，不能说用了Google规范，就可以进谷歌，甚至代码更流畅，只能说，相互参照一些内容，可以让代码更方便阅读以及维护吧。

（不过，个人可能还是习惯了国内的阿里，Effective java 这本书还没有看完，唉，还是太懒了）

------

## 一、简介

本文档作为 Google 的 Java™ 编程语言源代码编码标准的**完整定义。**当且仅当它遵守此处的规则时，Java 源文件才被描述为 *Google 风格。*

与其它的编程风格指南一样，这里所讨论的不仅仅是编码格式美不美观的问题， 同时也讨论一些约定及编码标准。然而，这份文档主要侧重于我们所普遍遵循的规则， 对于那些不是明确强制要求的，我们尽量避免提供意见。

### 1.1 术语说明

在本文件中，除非另有说明：

1. 术语 ***class\*** 包含地用于表示 “普通” 类、枚举类、接口或注解类型 ( `@interface`)。
2. 术语*成员*（of a class）包含性地用于表示嵌套的类、字段、方法*或构造函数*；也就是说，除了初始化程序和注释之外的类的所有顶级内容。
3. 术语comment只用来指代实现的注释(implementation comments)，我们不使用“documentation comments”一词，而是用Javadoc。

### 1.2 指导说明

本文档中的示例代码**是非规范的**。也就是说，虽然这些示例采用 Google 风格，但它们可能**无法说明表示代码的*****唯一\*****时尚方式**。示例中的可选格式选择**不应作为规则强制执行**。（不强制你使用这种规范）

------

# 二、源文件基础

## 2.1 文件名

源文件以其最顶层的类名来命名，大小写敏感，文件扩展名为.java。

## 2.2 文件编码：UTF-8

源文件以 **UTF-8** 编码。

## 2.3 特殊字符

### 2.3.1 空白字符

除了行终止符序列之外，**ASCII 水平空格字符** ( **0x20** ) 是唯一出现在源文件中任何位置的空白字符。这意味着：

1. 字符串和字符文字中的所有其他空白字符都被转义。
2. 制表符**不**用于缩进。

### 2.3.2 特殊转义序列

对于任何具有 [特殊转义序列](http://docs.oracle.com/javase/tutorial/java/data/characters.html) （`\b`、 `\t`、 `\n`、 `\f`、 `\r`、 和 ）的字符`\"`， 将使用该序列而不是相应的八进制（例如 ）或 Unicode（例如 ）转义。`\'``\\``\012``\u000a`

### 2.3.3 非 ASCII 字符

对于剩余的非 ASCII 字符，使用实际的 Unicode 字符（例如 `∞`）或等效的 Unicode 转义 符（例如 ） `\u221`。选择仅取决于使代码**更易于阅读和理解**的方式，尽管强烈建议不要使用 Unicode 转义字符串文字和注释。

**提示：**在 Unicode 转义情况下，有时甚至在使用实际的 Unicode 字符时，解释性注释也会很有帮助。

| 例子                                                     | 讨论                                                 |
| -------------------------------------------------------- | ---------------------------------------------------- |
| `String unitAbbrev = "μs";`                              | 最佳：即使没有注释也非常清楚。                       |
| `String unitAbbrev = "\u03bcs"; // "μs"`                 | 允许，但没有理由这样做。                             |
| `String unitAbbrev = "\u03bcs"; // Greek letter mu, "s"` | 允许，但尴尬且容易出错。                             |
| `String unitAbbrev = "\u03bcs";`                         | 很差：读者不知道这是什么。                           |
| `return '\ufeff' + content; // byte order mark`          | 好：对不可打印的字符使用转义符，并在必要时进行注释。 |

**提示：** 永远不要由于害怕某些程序可能无法正确处理非ASCII字符而让你的代码可读性变差。当程序无法正确处理非ASCII字符时，它自然无法正确运行， 你就会去fix这些问题的了。(言下之意就是大胆去用非ASCII字符，如果真的有需要的话)

------

# 三、源文件结构

源文件**按顺序**包括：

1. 许可或版权信息（如果需要）
2. 包装声明（package语句）
3. 导入语句（import语句）
4. 一个顶级类(只有一个)

**恰好一个空行**分隔存在的每个部分（以上每个部分之间用一个空行隔开）。

## 3.1 许可或版权信息（如果需要）

如果一个文件包含许可证或版权信息，那么它应当被放在文件最前面。

## 3.2 包装声明（package语句）

package语句不换行，列限制(4.4节)并不适用于package语句。(即package语句写在一行里)

## 3.3 导入语句（import语句）

### 3.3.1 import不要使用通配符

即，不要出现类似这样的import语句：import java.util.*;

### 3.3.2 无换行

import语句不换行，列限制(4.4节，列限制：100)并不适用于import语句。(每个import语句独立成行)

### 3.3.3 排序和间距

import的顺序如下。

1. 所有的静态导入在一个区块中。

2. 所有非静态进口在一个区块中。

如果同时有静态和非静态的导入，则用一个空行来分隔这两个块。在导入语句之间没有其他空行。

在**每个区块**中，导入的名字以ASCII排序方式出现。(**注意**：这与导入语句的ASCII排序不同，因为'.'排序在'；'之前）

### 3.3.4 没有静态导入的类

静态导入不用于静态嵌套类。它们是用普通的导入方式导入的。

关于静态导入可参考这篇文章：https://www.cnblogs.com/mengdd/archive/2013/01/23/2873312.html

百度知道 解释：

![img](https://img-blog.csdnimg.cn/img_convert/00007f1f90bd2be82fa37c0010d14e8e.png)

## 3.4 类声明

### 3.4.1 只有一个顶层类的声明

每个顶层类都驻留在一个自己的源文件中。

### 3.4.2 类内容的排序

你为你的类的成员和初始化器选择的顺序对可学习性有很大影响。然而，如何做到这一点并没有一个正确的秘诀；不同的类可能会以不同的方式排列其内容。

重要的是，每个类都使用一些逻辑顺序，如果有人问起，其维护者可以解释。例如，新的方法不会被习惯性地添加到类的末尾，因为这将产生 "按添加日期的时间顺序 "排序，而这并不是一个逻辑排序

#### 3.4.2.1 重载：从不拆分

当一个类有多个构造函数或多个同名方法时，这些方法会按顺序出现，中间没有其他代码（甚至没有私有成员）

------

# 四、格式化

术语说明：类块结构是指类、方法或构造函数的主体。请注意，根据第4.8.3.1节关于数组初始化器的规定，任何数组初始化器都可以选择性地被当作类块结构来处理

## 4.1 大括号

### 4.1.1 在可选的地方使用大括号

大括号用于if、else、for、do和while语句，即使主体为空或只包含一条语句``

### 4.1.2 非空块：K & R 风格

大括号遵循 Kernighan 和 Ritchie 样式（“ Egyptian 括号”），用于*非空*块和块状结构：

- 左大括号前不换行
- 左大括号后换行

- 右大括号前换行
- 如果右大括号是一个语句、函数体或类的终止，则右大括号后换行; 否则不换行。例如，如果右大括号后面是else或逗号，则不换行。

例子：

```java
return () -> {
  while (condition()) {
    method();
  }
};

return new MyClass() {
  @Override public void method() {
    if (condition()) {
      try {
        something();
      } catch (ProblemException e) {
        recover();
      }
    } else if (otherCondition()) {
      somethingElse();
    } else {
      lastThing();
    }
  }
};
```



枚举类的一些例外情况在第 4.8.1 节， [枚举](#s4.8.1-enum-classes)类中给出。

### 4.1.3 空块：可以是简洁的

一个空块或类似块的结构可以是K&R风格的（如4.1.2节所述）。另外，它可以在打开后立即关闭，中间没有字符或换行（{}），除非它是多块语句的一部分（直接包含多个块的语句：if/else或try/catch/finally）。

例子：

```plain
//这是可以接受的
void doNothing() {}

// 这也是可以接受的
void doNothingElse() {
}
```



```plain
// 这是不可以的。在一个多块语句中不能有简洁的空块
try {
    doSomething();
  } catch (Exception e) {}
```



## 4.2 块缩进：+2 个空格

每当一个新的区块或类似区块的结构被打开时，缩进就会增加两个空格。当区块结束时，缩进会恢复到之前的缩进水平。缩进程度适用于整个块中的代码和注释。(参见第4.1.2节中的例子，非空块：K & R风格）。

## 4.3 每行一个语句

每条语句后面都有一个换行符。

## 4.4 列数限制：100

Java代码有一个100个字符的列限制。一个 "字符 "是指任何Unicode代码点。除了下面提到的情况，任何超过这个限制的行都必须进行换行，如第4.5节 "换行 "所解释的。

每个Unicode码位都算作一个字符，即使它的显示宽度有大有小。例如，如果使用全宽字符，你可以选择在本规则严格要求的地方提前换行。

**例外：**

1. 不可能遵守列限制的行（例如，Javadoc中的长URL，或长的JSNI方法引用）。
2. package和import语句（见第3.2节package语句和3.3节import语句）。
3. 注释中的命令行，可以剪切并粘贴到shell中。

## 4.5 换行

**术语说明**：当本来可能合法地占用一行的代码被分成多行时，这种活动被称为换行。

没有一个全面的、决定性的公式能准确地显示在任何情况下如何换行。很多时候，对同一段代码有几种有效的换行方式。

**注意：**虽然换行的典型原因是为了避免超出列限制，但即使是实际上适合列限制的代码*也* 可以由作者自行决定换行。

**提示**：*提取方法或局部变量可以在不换行的情况下解决代码过长的问题(是合理缩短命名长度吧)*

### 4.5.1 在哪里断开

自动换行的基本准则是：更倾向于在更高的语法级别处断开，此外：

1.  当在*非赋值*运算符处断行时，断行出现在符号之前。（请注意，这与 Google 风格中用于其他语言（例如 C++ 和 JavaScript）的做法不同。） 

- 这也适用于以下 “类似运算符” 的符号： 

  - 点分隔符 ( `.`)

  - 方法引用的两个冒号 ( `::`)

  - 类型绑定 ( `<T extends Foo & Bar>`) 中的 & 符号

  - catch 块 ( `catch (FooException | BarException e)`) 中的管道。

2. 当在*赋值*运算符处断行时，断行通常出现在符号之后，但任何一种方式都是可以接受的。 

  - 这也适用于增强 `for`（“foreach”）语句中的 “类似赋值运算符” 的冒号。

3. 一个方法或构造函数的名称要与它后面的开放小括号 ( `(`) 相连。 

4. 逗号 ( `,`) 始终与它前面的标记相连。 

5. 在lambda的箭头附近永远不会断行，但如果lambda的主体是由单个非代数表达式组成，，则可以在箭头之后立即断行

例子：  

```plain
MyLambda<String, Long, Object> lambda =
    (String label, Long value, Object obj) -> {
        ...
    };

Predicate<String> predicate = str ->
    longExpressionInvolving(str);
```



**注意：**换行的主要目标是拥有清晰的代码，*而不一定*是适合最少行数的代码。

### 4.5.2 自动换行时缩进至少+4个空格

当换行时，第一行之后的每一行（每一个延续行）至少要从原行缩进+4。

当有多个延续行时，缩进可以根据需要超过+4。一般来说，两个延续行使用相同的缩进水平，当且仅当它们以语法上平行的元素开始时。

第4.6.3节 "水平对齐 "讨论了不鼓励的做法，即使用可变的空格数使某些标记与前几行对齐

## 4.6 空白

### 4.6.1 垂直空白

以下情况需要使用一个空行：

1. 在一个类的连续成员或初始化器之间：字段、构造函数、方法、嵌套类、静态初始化器、以及实例初始化器。 

  - **例外：**两个连续的字段之间的空行（它们之间没有其他代码）是可选的。这样的空行是用来创建字段的逻辑分组的。

  - **例外：**[第 4.8.1 节](#s4.8.1-enum-classes)介绍了枚举常量之间的空行。

2. 根据本文档其他部分的要求（例如第 3 节， [源文件结构](#s3-source-file-structure)和第 3.3 节， [导入语句](#s3.3-import-statements)）。

单独的空行也可以出现在任何可以提高可读性的地方，例如，在语句之间，将代码组织成合乎逻辑的小节。在类的第一个成员或初始化器之前，或最后一个成员或初始化器之后，既不鼓励也不反对出现空行。

允许有多个连续的空行，但从不要求（或鼓励）。

### 4.6.2 水平空白

除了语言或其他风格规则的要求外，除了字面意义、注释和Javadoc外，单个ASCII空格也**只**出现在以下地方。

1. 分隔任何保留字与紧随其后的左括号( ( )(如if, for catch等)。
2. 分隔任何保留字与其前面的右大括号( } )(如else, catch)
3.  在任何左大括号 ( `{`) 之前，有两个例外： 

  - `@SomeAnnotation({a, b})` （不使用空格）

  - `String[][] x = {{"foo"}};`（大括号间没有空格，见下面第八项）

4.  在任何二元或三元运算符的两侧。这也适用于以下 “类运算符” 的符号： 

  - 合取类型界限中的 & 符号： `<T extends Foo & Bar>`

  - 处理多个异常的 catch 块的管道： `catch (FooException | BarException e)`

  - 增强型 `for`（“foreach”）语句中的冒号 ( : )

  - lambda 表达式中的箭头： `(String str) -> str.length()`

但不是 

  - 方法引用的两个冒号 ( `::`)，写成`Object::toString`

  - 点分隔符 ( `.`)，写成 `object.toString()`

5. 在`,:;`或右括号 ( `)`) 
6.  在开始行末注释的双斜线（//）的两侧。这里，允许有多个空格，但不是必须的。 
7.  在一个声明的类型和变量之间： `List<String> list` 
8. 在数组初始值设定项的两个大括号内都是 *可选的* 

  - `new int[] {5, 6}`并且 `new int[] { 5, 6 }`都是有效的

   9.在类型注释和`[]`或`...`之间。 

Note：此规则永远不会被解释为要求或禁止在行首或行尾添加额外的空格；它只针对*内部*空间。

### 4.6.3 水平对齐：不做要求

**术语说明**：水平对齐是在你的代码中增加可变数量的额外空间，目的是使某些标记出现在前几行的某些其他标记的正下方。（水平对齐指的是通过增加可变数量的空格来使某一行的字符与上一行的相应字符对齐）

这种做法是允许的，但绝不是谷歌风格所要求的。在已经使用了水平对齐的地方，甚至不需要保持水平对齐。

下面是一个没有对齐的例子，然后使用对齐



```plain
private int x; // 这很好
private Color color; // 这个也可以

private int   x;      // 允许的，但将来会被编辑
private Color color;  // 可以不对齐
```



**只**考虑一个可能会出现的问题，但现在可能会**出现**未来的变化。更常见的是它会提示编码器（可能是现在）也调整这行的空白，可能触发更改行级联的重新定义。会导致没有任何意义的重要工作，但在最好的情况下，它仍然会显示历史信息，减少慢阅者的速度并混合破解。

**提示**：对齐可以提高可读性，但会给未来的维护带来问题。考虑到未来的变化，只需要触及一行。这种改变可能会使以前令人满意的格式被弄乱，这是被允许的。但更多的时候，它会促使编码者（也许是你）对附近几行的空白进行调整，可能会引发一连串的改写。这一行的变化现在有一个 "爆炸半径"。这在最坏的情况下会导致无意义的忙碌，但在最好的情况下，它仍然会破坏版本历史信息，拖慢审查人员的速度，加剧合并冲突。

## 4.7 分组括号：推荐

只有当作者和审查者一致认为没有小括号，代码就不会被误解，也不会使代码更容易阅读时，才会省略可选的分组小括号。假设每个读者都记住了整个Java操作符优先级表是不合理的

## 4.8 具体结构

### 4.8.1 枚举类

在枚举的后面也允许有引号的空格，换行符是可选的。

```plain
private enum Answer {
  YES {
    @Override public String toString() {
      return "yes";
    }
  },

  NO,
  MAYBE
}
```

一个没有方法也没有常量文档的枚举类可以选择性地被格式化为数组初始化器（参见第4.8.3.1节关于数组初始化器），

```plain
private enum Suit { CLUBS, HEARTS, SPADES, DIAMONDS }
```

因为枚举类是类，所以所有其他用于格式化类的规则都适用。

### 4.8.2 变量声明

#### 4.8.2.1 每个声明只有一个变量

每个变量声明（字段或局部）只声明一个变量：不使用诸如int a, b;的声明。

**例外：**在for循环的头部可以接受多个变量的声明。

#### 4.8.2.2 在需要时声明

局部变量不习惯于在其包含的块或块状结构的开始处声明。相反，局部变量会在靠近它们第一次使用的地方被声明（在合理范围内），以最小化它们的范围。局部变量的声明通常有初始化器，或者在声明后立即被初始化。

### 4.8.3 数组

#### 4.8.3.1 数组初始化：可写成块状结构

任何数组的初始化器都可以有选择地被格式化为 "类块结构"。例如，下面这些都是有效的（不是一个详尽的列表）。

```plain
new int[] {           new int[] {
  0, 1, 2, 3            0,
}                       1,
                        2,
new int[] {             3,
  0, 1,               }
  2, 3
}                     new int[]
                          {0, 1, 2, 3}
```

#### 4.8.3.2 没有C语言风格的数组声明

方括号构成类型的一部分，而不是变量的一部分。String[] args，而不是String args[]。

### 4.8.4 switch语句

**术语说明：**switch语句的大括号内是一个或多个语句组。每个语句组由一个或多个switch标签（either case FOO: or default:）组成，后面是一个或多个语句（或者，对于最后一个语句组，是零个或多个语句）

#### 4.8.4.1 缩进

与其他块一样，switch块的任何内容缩进+2。

在切换标签之后，会有一个换行，并且缩进程度会增加+2，就像一个块被打开一样。接下来的切换标签会回到之前的缩进水平，就像一个区块被关闭一样。(每个switch标签后新起一行，再缩进2个空格，写下一条或多条语句。)

#### 4.8.4.2 Fall-through：注释

在switch块中，每个语句组要么突然终止（用break、continue、return或抛出的异常），要么用注释来表示执行将或可能继续到下一个语句组。任何能传达 "穿越 "概念的注释都是足够的（通常是//穿越）。这个特殊的注释在switch块的最后一个语句组中是不需要的。

例子：

```plain
switch (input) {
  case 1:
  case 2:
    prepareOneOrTwo();
    // fall through
  case 3:
    handleOneTwoOrThree();
    break;
  default:
    handleLargeNumber(input);
}
```



注意，在case 1:之后不需要注释，只需要在语句组的末尾注释。

#### 4.8.4.3`default`是存在的

每个switch语句都包括一个default语句组，即使它不包含任何代码。

**例外：**枚举类型的switch语句可以省略默认语句组，如果它包括涵盖该类型所有可能值的明确案例。这使得IDE或其他静态分析工具能够在遗漏任何案例时发出警告

### 4.8.5 注解(Annotations)

适用于类、方法或构造函数的注解紧接着出现在文档块之后，每个注解都被列在自己的一行中（也就是说，每行一个注解）。这些换行并不构成换行（第4.5节，换行），所以缩进程度不会增加。

例子：

```plain
@Override
@Nullable
public String getNameIfPresent() { ... }
```

**例外：**一个单一的无参数注解反而可以和签名的第一行一起出现，比如说。

```plain
@Override public int hashCode() { ... }
```

适用于一个字段的注释也紧随在文档块之后，但在这种情况下，多个注解（可能是参数化的）可以列在同一行；例如。

```plain
@Partial @Mock DataLoader loader;
```

对于参数、局部变量或类型上的注释的格式化，没有特定的规则。

### 4.8.6 注释

本节讨论实现注释。 Javadoc 在 Javadoc 第7节中单独讨论。

任何断行都可以在任意的空白处，然后是一个执行注释。这样的注释使该行成为非空行。

#### 4.8.6.1 区块注释风格

区块注释的缩进程度与周围的代码相同。它们可以是/* ... */风格或//...风格。对于多行的/* ... */ 注释，后面的行必须以*开头，与前一行的*对齐。

```plain
/*
 * This is          // And so           /* Or you can
 * okay.            // is this.          * even do this. */
 */
```

注释不包括在用星号或其他字符绘制的方框内

**提示：**当写多行注释时，如果你想让自动代码格式化器在必要时重新包装行，请使用/* ... */ 样式，如果你想让自动代码格式化器在必要时重新包装这些行（段落样式）。大多数格式化器不会在// ... 样式的注释块中重新换行。

### 4.8.7 修饰语

类和成员的修饰语，如果存在的话，就按照《Java语言规范》推荐的顺序出现。

```plain
public protected private abstract default static final transient volatile synchronized native strictfp
```

### 4.8.8 数字字符

长值整数字使用大写的L后缀，而不是小写的（以避免与数字1混淆）。例如，3000000000L而不是3000000000l。

------

# 五、命名约定

## 5.1 所有标识符的共同规则

识别符只使用ASCII字母和数字，在下面提到的少数情况下，还有下划线。因此，每个有效的标识符名称都由正则表达式\w+匹配。

在谷歌风格中，**不**使用特殊的前缀或后缀。例如，这些名称不是Google Style：name_、mName、s_name和kName。

## 5.2 按标识符类型划分的规

### 5.2.1 包名

包的名称都是小写的，连续的单词简单的连接在一起（没有下划线）。例如，com.example.deepspace，而不是com.example.deepSpace或com.example.deep_space。

### 5.2.2 类名

类的名称用UpperCamelCase书写。

类名通常是名词或名词短语。例如，Character或ImmutableList。

接口名称也可以是名词或名词短语（例如，List），但有时可能是形容词或形容词短语（例如，可读）。

对于注解类型的命名，没有具体的规则，甚至没有完善的惯例。

测试类的命名以它们所测试的类的名称开始，并以Test结束。例如，HashTest或HashIntegrationTest。

### 5.2.3 方法名称

方法名称以小写字母（lowerCamelCase）书写。

方法名称通常是动词或动词短语。例如，sendMessage或stop。

JUnit测试方法名称中可以出现下划线，以分隔名称中的逻辑组件，每个组件用小写的CamelCase书写。一个典型的模式是<methodUnderTest>_<state>，例如 pop_emptyStack。没有一个正确的方法来命名测试方法。

### 5.2.4 常量名

常量名称使用CONSTANT_CASE：全部为大写字母，每个字之间用一个下划线分开。但究竟什么是常量？

常量是静态的最终字段，其内容是不可改变的，其方法没有可检测的副作用。这包括基元、字符串、不可变类型和不可变类型的不可变集合。如果实例的任何可观察状态可以改变，那么它就不是常量。仅仅打算不改变对象是不够的。例子：

```plain
// 常量
static final int NUMBER = 5;
static final ImmutableList<String> NAMES = ImmutableList.of("Ed", "Ann");
static final ImmutableMap<String, Integer> AGES = ImmutableMap.of("Ed", 35, "Ann", 32);
static final Joiner COMMA_JOINER = Joiner.on(','); // because Joiner is immutable
static final SomeMutableType[] EMPTY_ARRAY = {};
enum SomeEnum { ENUM_CONSTANT }

// 不是常量
static String nonFinal = "non-final";
final String nonStatic = "non-static";
static final Set<String> mutableCollection = new HashSet<String>();
static final ImmutableSet<SomeMutableType> mutableElements = ImmutableSet.of(mutable);
static final ImmutableMap<String, SomeMutableType> mutableValues =
    ImmutableMap.of("Ed", mutableInstance, "Ann", mutableInstance2);
static final Logger logger = Logger.getLogger(MyClass.getName());
static final String[] nonEmptyArray = {"these", "can", "change"};
```



这些名称通常是名词或名词短语。

### 5.2.5 非常量字段名

这些名字通常是名词 非恒定字段名（静态或其他）用小写的CamelCase书写。

这些名称通常是名词或名词短语。例如，computedValues或index.或名词短语。

### 5.2.6 参数名

参数名称以小写字母（lowerCamelCase）书写。

应避免在公共方法中使用一个字符的参数名。

### 5.2.7 局部变量名

局部变量的名字是用小写的CamelCase写的。

即使是最终的和不可改变的，局部变量也不被认为是常量，也不应该被写成常量。

### 5.2.8 类型变量名

每个类型变量有两种命名方式:

- 一个大写字母，后面可以选择一个数字（比如E、T、X、T2）。
- 用类的形式命名（见第5.2.2节，类名），后面是大写字母T（例子：RequestT，FooBarT）。

## 5.3 驼峰式命名法(CamelCase)

有时，将一个英文短语转换为驼峰大小写的合理方式不止一种，例如当缩写或不寻常的结构如 "IPv6 "或 "iOS "出现时。为了提高可预测性，Google Style规定了以下（近乎）确定性的方案。

从名称的散文形式开始：

1. 将短语转换为普通ASCII码，并去掉任何撇号。例如，"Müller's algorithm "可能变成 "Muellers algorithm"。
2. 将这一结果分成几个词，在空格和任何剩余的标点符号（通常是连字符）上进行分割。

- - 建议：如果任何一个词在常用的情况下已经有了传统的骆驼大写的外观，就把它分成它的组成部分（例如，"AdWords "变成 "ad words"）。请注意，像 "iOS "这样的词本身并不是真正的驼峰大写；它违背了任何惯例，所以这一建议并不适用。

3. 现在，所有的东西都小写（包括首字母缩写），然后只将第一个字符大写。

- - 每个单词的第一个字母都大写，来得到大驼峰式命名。
  - 除了第一个单词，每个单词的第一个字母都大写，来得到小驼峰式命名。

4. 最后，将所有的词连接成一个单一的标识符。

请注意，原始单词的大小写几乎被完全忽略了。例子。

| **形式**                | **正确**                         | **不正确**        |
| ----------------------- | -------------------------------- | ----------------- |
| "XML HTTP request"      | XmlHttpRequest                   | XMLHTTPRequest    |
| "new customer ID"       | newCustomerId                    | newCustomerID     |
| "inner stopwatch"       | innerStopwatch                   | innerStopWatch    |
| "supports IPv6 on iOS?" | supportsIpv6OnIos                | supportsIPv6OnIOS |
| "YouTube importer"      | YouTubeImporter YoutubeImporter* |                   |

*可以接受，但不推荐

注意：有些词在英语中是模糊的连字符：例如 "nonempty "和 "non-empty "都是正确的，所以方法名称checkNonempty和checkNonEmpty也同样都是正确的。

------

# 六、编程实践

## 6.1 @Override: 始终使用

只要一个方法是合法的，就会用@Override注解来标记。这包括覆盖超类方法的类方法、实现接口方法的类方法、以及重新指定超接口方法的接口方法。

例外。当父方法是@Deprecated时，@Override可以被省略。

## 6.2 捕获的异常：不被忽视

除了下面提到的情况，很少有对捕获的异常不做任何反应的情况。(典型的反应是记录它，或者如果它被认为是 "不可能的"，将它作为AssertionError重新抛出）。

当真正适合在捕获块中不采取任何行动时，将在注释中解释这样做的理由。

```java
try {
  int i = Integer.parseInt(response);
  return handleNumericResponse(i);
} catch (NumberFormatException ok) {
  // it's not numeric; that's fine, just continue
}
return handleTextResponse(response);
```

**异常**：在测试中，如果一个被捕获的异常的名字是或以预期开头，可以不加注释而被忽略。下面是一个非常常见的习惯，用来确保被测试的代码确实抛出了一个预期类型的异常，所以这里不需要注释。

```java
try {
  emptyStack.pop();
  fail();
} catch (NoSuchElementException expected) {
}
```

## 6.3 静态成员：使用类的限定

当对静态类成员的引用必须被限定时，它被用该类的名称来限定，而不是用该类的类型的引用或表达式来限定。

```java
Foo aFoo = ...;
Foo.aStaticMethod(); // good
aFoo.aStaticMethod(); // bad
somethingThatYieldsAFoo().aStaticMethod(); // very bad
```

## 6.4 Finalizers: 禁用

覆盖Object.finalize是极为罕见的。

**提示**：不要这样做。如果你一定要这么做，首先要仔细阅读并理解**Effective Java**第7项 "避免使用最终处理器"，然后不要这么做。

------

# 七、Javadoc

## 7.1格式

### 7.1.1一般形式

Javadoc块的基本格式如本例所示

```java
/**
 * 多行Javadoc文本写在这里。
 * 正常包装...
 */
public int method(String p1) { ... }
```

或者在这个单行的例子里:

```java
/** An especially short bit of Javadoc. */
```

基本形式总是可以接受的。当Javadoc块的全部内容（包括注释标记）可以放在一行中时，可以用单行形式代替。请注意，这只适用于没有诸如@return这样的块标记的情况。。

### 7.1.2 段落

段落之间有一个空行--即只包含对齐的前导星号（*）的行，如果有块状标签组，则在块状标签组之前出现。除第一段外，每个段落的第一个词前都有<p>，后面没有空格。

### 7.1.3 块标签

任何使用的标准 "块标记 "都是按照@param, @return, @throws, @deprecated的顺序出现的，这四种类型永远不会以空的描述出现。当一个块状标签不适合在一行中出现时，延续行会从@的位置缩进四个（或更多）空格。

## 7.2 摘要片段

每个Javadoc块都以一个简短的摘要片段开始。这个片段非常重要：它是文本中唯一出现在某些上下文中的部分，比如类和方法的索引。

这是一个片段--名词短语或动词短语，不是一个完整的句子。它不是以A {@code Foo} 是一个......开始，或者这个方法返回......，也不是构成一个完整的命令句，如Save the record......。然而，该片段被大写，并使用标点符号，就像它是一个完整的句子一样。

**提示**：一个常见的错误是把简单的Javadoc写成/** @return the customer ID */，这是不正确的。它应该写成/** Returns the customer ID. */。

## 7.3 使用Javadoc的地方

至少，每个公有类，以及公有类中的每个公有或受保护的成员都要有Javadoc，但下面提到的几个例外情况。

额外的Javadoc内容也可以出现，如第7.3.4节 "非必需的Javadoc "所解释。

### 7.3.1 例外：不言而喻的方法

Javadoc对于像getFoo这样的 "简单、明显 "的方法来说是可选的，在这种情况下，除了 "getFoo"，确实没有其他值得说的东西。

**重要的是**：如果有一些相关信息是需要读者了解的，那么以上的例外不应作为忽视这些信息的理由。例如，对于方法名getCanonicalName， 就不应该忽视文档说明，因为读者很可能不知道词语canonical name指的是什么。

### 7.3.2  例外：重写

Javadoc并不总是出现在重写超类型方法的方法上。

### 7.3.3 可选的Javadoc
对于包外不可见的类和方法，如有需要，也是要使用Javadoc的。如果一个注释是用来定义一个类，方法，字段的整体目的或行为， 那么这个注释应该写成Javadoc，这样更统一更友好

其他的类和成员根据需要或需要有Javadoc。

每当一个实现注释被用来定义一个类或成员的整体目的或行为时，该注释被写成Javadoc（使用/**）。

非必要的Javadoc并不严格要求遵循第7.1.2节、7.1.3节和7.2节的格式规则，但是当然推荐使用它。