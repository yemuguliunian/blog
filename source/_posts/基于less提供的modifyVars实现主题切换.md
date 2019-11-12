---
title: 基于less提供的modifyVars实现主题切换
date: 2019-11-12 16:35:31
tags:
---

## 参考

https://github.com/ElemeFE/element/issues/3054

https://blog.csdn.net/weixin_30872671/article/details/98286899 - 使用 css/less 动态更换主题色（换肤功能）

https://www.cnblogs.com/starof/p/5226739.html - less 简单入门

## 实现方式

使用 less 提供的 modifyVars 的方式来实现。  
http://lesscss.org/usage/#using-less-in-the-browser-modify-variables

modifyVars 方法是是基于 less 在浏览器中的编译来实现。所以在引入 less 文件的时候需要通过 link 方式引入，然后基于 less.js 中的方法来进行修改变量。

[代码实现](https://github.com/yemuguliunian/notes/tree/master/practice/theme-preview)
<!-- more -->
### index.html 引入主题色文件 和 less.js

less 样式文件一定要在引入 less.js 前先引入。

```
// color.less
@backgroud-color: #108ee9;

.ant-btn {
    background-color: @backgroud-color;
}

// index.html
<head>
    <link rel="stylesheet/less" type="text/css" href="./resources/style/color.less" />
    <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.3/less.min.js"></script>
</head>
```

### 更改主题色事件

```js
less.modifyVars({
    '@backgroud-color': #000
});
```

### 原理

通过 less modifyVars 修改变量来达到换主题的效果。其本质上是样式覆盖。

less.js 会 把 color.less 浏览器编译成 行内样式 即 F12 查看 index.html 可发现

```html
<head>
    <link rel="stylesheet/less" type="text/css" href="./resources/style/color.less" />  
    <style type="text/css" id="less:resources-style-color">
        .ant-btn {
            background-color: #108ee9;
        }
    </style>
    <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.3/less.min.js"></script>       
</head>
```

调用 modifyVars 后重新编译为

```html
<head>
    <link rel="stylesheet/less" type="text/css" href="./resources/style/color.less" />
    <style type="text/css" id="less:resources-style-color">
        .ant-btn {
            background-color: #000;
        }
    </style>
    <script src="//cdnjs.cloudflare.com/ajax/libs/less.js/2.5.3/less.min.js"></script>
</head>
```

本质上是对页面 `ant-btn` 类属性 `background-color` 一个覆盖操作。

**`index.html` 行内样式中的 `ant-btn` 类属性 `background-color` 覆盖页面中的 `ant-btn` 类属性 `background-color`**

```
// demo.html
<button class="ant-btn"></button>

// demo.css
.ant-btn {
    background-color: #108ee9;
}
```

注：执行 modifyVars 时， color.less 文件本身没有任何变更，编译时传入修改变量所对应的值
