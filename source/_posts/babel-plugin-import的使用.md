---
title: 使用 babel-plugin-import 实现按需加载
date: 2020-01-23 9:49:23
tags:
- 按需加载
categories:
- babel
---

## 参考

https://www.npmjs.com/package/babel-plugin-import

https://github.com/ant-design/babel-plugin-import

#### 示例
{ "libraryName": "antd" }

```
import { Button } from 'antd';
ReactDOM.render(<Button>xxxx</Button>);

      ↓ ↓ ↓ ↓ ↓ ↓

var _button = require('antd/lib/button');
ReactDOM.render(<_button>xxxx</_button>);
```
{ "libraryName": "antd", style: "css" }

```
import { Button } from 'antd';
ReactDOM.render(<Button>xxxx</Button>);

      ↓ ↓ ↓ ↓ ↓ ↓

var _button = require('antd/lib/button');
require('antd/lib/button/style/css');
ReactDOM.render(<_button>xxxx</_button>);
```
{ "libraryName": "antd", style: true }

```
import { Button } from 'antd';
ReactDOM.render(<Button>xxxx</Button>);

      ↓ ↓ ↓ ↓ ↓ ↓

var _button = require('antd/lib/button');
require('antd/lib/button/style');
ReactDOM.render(<_button>xxxx</_button>);
```
备注 : 配置 style: true 则在项目编译阶段，可以对引入的 antd 样式文件进行编译，从而可以压缩打包尺寸；而配置style: "css", 则直接引入经过打包后的 antd 样式文件

<!-- more -->
#### 使用方式

```
npm install babel-plugin-import --save-dev
```
通过 .babelrc 配置文件或者 babel-loader 模块编程引入.

```
{
  "plugins": [["import", options]]
}
```

#### options
options can be object.

```
{
  "libraryName": "antd",
  "style": true,   // or 'css'
} 
```

```
{
  "libraryName": "lodash",
  "libraryDirectory": "", //表示从库的package.json的main入口；否则默认为lib文件夹
  "camel2DashComponentName": false,  // default: true，将引入的组件名转化为"-"连接的文件名
}
```



