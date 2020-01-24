---
title: 使用docz写ReactUI文档
date: 2019-12-03 12:58:07
tags:
- doc
- 交互式文档
categories:
- doc
---

> 使用简单，目前只支持 React

- [官网](https://www.docz.site/)
- [Github](https://github.com/doczjs/docz)

## 使用

1. 安装

```
$ yarn add docz
```

2. 在你项目中的任何位置新增 `.mdx` 文件
<!-- more -->

```
---
name: Button
route: /
---

import { Playground, Props } from 'docz'
import Button from './Button'

# Button

<Props of={Button} />

## Basic usage

<Playground>
  <Button type="submit">Click me</Button>
  <Button>No, click me</Button>
</Playground>
```

3. And a Button component Button.jsx:

```
import React from 'react'
import t from 'prop-types'

const Button = ({ children, type }) => <button type={type}>{children}</button>

Button.propTypes = {
  /**
   * This is a description for this prop.
   * Button type.
   */
  type: t.oneOf(['button', 'submit', 'reset']),
}
Button.defaultProps = {
  type: 'button',
}
export default Button
```

4. 运行

```
yarn docz dev
```

This will start a local development server and open your documentation site in the browser.


## 常用配置项

项目下新建 `doczrc.js`，更多配置项参考：https://www.docz.site/docs/project-configuration

```
export default {
    typescript: true,
    title: 'docz',
    ignore: ['README.md', 'CHANGELOG.md'],
    port: '3000',
    dest: './docs',
};

```

### typescript

This option is used if you need to import Typescript components inside your .mdx files.

### port

启动服务端口

### ignore

Option used to ignore files to be parsed by docz.

### dest

设置打包路径，默认值`.docz/dist`


## FAQ

### Using Docz parsing CSS with LESS
> 参考 https://github.com/doczjs/docz/tree/master/examples/less

1. 安装 `gatsby-plugin-less`

```
yarn install gatsby-plugin-less -D
```

2. 根目录下新建 `gatsby-config.js`，并写入

```
module.exports = {
  plugins: ['gatsby-plugin-less'],
}
```

3. 执行 `yarn docz dev`


### 自定义样式

在项目根目录下新建 `src` 文件夹.

在`docz`目录下新建`gatsby-theme-docz/wrapper.js`，`gatsby-theme-docz/global.css`.

**wrapper.js**

```
import React from 'react';
import './global.css';

export default function Wrapper(props) {
    return <div>{props.children}</div>;
}

```
**global.css**

```
p {
    margin: 0;
}
```


### Writing a function or Class in mdx 

参考：

https://github.com/doczjs/docz/issues/918

Example with a React component

```
<Playground>
  {class Example extends React.Component {
    constructor (props) {
      super(props)

      this.state = { show: false }
    }

    handleClick () {
      this.setState({ show: true })
    }

    render () {
      return (
        <React.Fragment>
          {this.state.show &&
            <div>
              <p>
                Lorem ipsum dolor sit amet, consetetur sadipscing elitr,
                sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua.
                At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren,
                no sea takimata sanctus est Lorem ipsum dolor sit amet. Lorem ipsum dolor sit amet,
                consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat,
                sed diam voluptua. At vero eos et accusam et justo duo dolores et ea rebum. Stet clita kasd gubergren,
                no sea takimata sanctus est Lorem ipsum dolor sit amet.
              </p>
            </div>
          }
          <button onClick={() => this.handleClick()}>Show</button>
        </React.Fragment>
      )
    }
  }}
</Playground>
```

Example with a JS function

```
<Playground>
  {() => {
    console.log('docz')
  }}
</Playground>
```
