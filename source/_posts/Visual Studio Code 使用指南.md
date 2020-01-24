---
title: Visual Studio Code 使用指南
date: 2020-01-24 13:23:11
tags:
- 编译器
categories:
- tool
---

**下载地址**
https://code.visualstudio.com/

## 配置

### 中文汉化

1. 点击左侧的 扩展
2. 搜索 Chinese ，点击 Install

### 主题色配置

文件 - 首选项 - 颜色主题

### 菜单栏文件的缩进

文件 - 首选项 - 设置 - 搜索 Tree:Indent 修改树缩进即可

### 安装插件

快捷键 Ctrl + Shift + X

### Markdown 侧边预览

- Ctrl + Shift + P  
输入==Markdown==
- 先按Ctrl + K，然后放掉，紧接着再按 v

### 自定义代码片段（强推）

文件 - 首选项 - 用户代码片段


## 插件

### Auto Close Tag
> 自动闭合HTML标签

### Auto Rename Tag
> 自动同步修改标签 

### Path Autocomplete
> 路径自动补全

### eslint 集成ESLint检查
> 代码审查

### Prettier - Code formatter
> 代码格式规范

### Vetur
> 高亮 .vue 文件

在编辑器中集成 ESLint
检查，可以在开发过程中就发现错误，甚至可以在保存时自动修复错误，极大的增加了开发效率。

要在 VSCode 中集成 ESLint 检查，我们需要先安装 ESLint 插件，点击「扩展」按钮，搜索 ESLint，然后安装即可。

VSCode 中的 ESLint 插件默认是不会检查 .ts 后缀的，需要在「文件 => 首选项 => 设置 => 工作区」中（也可以在项目更目录下创建一个配置文件 .vscode/settings.json），添加以下配置：
```
{
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        "typescript"
    ],
    "typescript.tsdk": "node_modules/typescript/lib"
}
```

### SFTP

https://blog.csdn.net/sunny327/article/details/81866785


## FAQ

### typescript使用alias vscode提示找不到模块
> 在项目中使用alias功能，直接给了一个警告，虽然程序是可以正常运行的，但是无法通过点击跳转到文件

为了解决这个问题，需要借助tsconfig，尽管webpack已经配置好了alias， 可是ts并不认账。

webpack配置
```
{
    alias: {
        '@components': path.resolve(__dirname, 'src/components/'),
    }
}
```
tsconfig.json 配置如下
```
{
    "compilerOptions": {
        "paths": {
            "@components/*": ["src/components/*"],
        },
    }
}
```
如果不行可能需要重启vscode
