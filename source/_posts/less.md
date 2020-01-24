---
title: less
date: 2020-01-23 9:58:36
tags:
- less
categories:
- css
---

> 一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展

### docs
http://lesscss.cn/

### Knowledge

#### @import (keyword) "filename"

为了在将Less文件编译生成CSS文件时，提高对外部文件的操作灵活性，还为@import指令提供了一些配置项。语法为：

选项 | 含义
---|---
reference | 使用文件，但不会输出其内容（即，文件作为样式库使用）
inline | 对文件的内容不作任何处理，直接输出
less | 无论文件的扩展名是什么，都将作为LESS文件被输出
css | 无论文件的扩展名是什么，都将作为CSS文件被输出
once | 文件仅被导入一次 （这也是默认行为）
multiple | 文件可以被导入多次
optional | 当文件不存在时，继续编译（即，该文件是可选的）

@import指令可以使用一个或多个配置项，当使用多个配置项时，各配置项之间用逗号隔开

```
@import (optional, reference) "foo.less";
```
