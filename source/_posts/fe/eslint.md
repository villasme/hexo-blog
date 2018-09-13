---
title: vscode-eslint配置
date: 2018-09-11 16:57:58
categories: FE
tags:
- eslint
- vscode
---
##  vscode配置

- [eslint vscode 使用](https://segmentfault.com/a/1190000009077086)

- [要求或禁止函数圆括号之前有一个空格 (space-before-function-paren)](http://eslint.cn/docs/rules/space-before-function-paren)

- 安装 eslint 插件
- npm install -D eslint 
- 新建 .eslintrc.js
- 下载私人 eslint 包
- 修改配置文件 继承配置
```js
module.exports = {
    "env": {
        "browser": true,
        "commonjs": true,
        "es6": true
    },
    "extends": "eslint-config"
};
```
- 根据 [eslint vscode 使用](https://segmentfault.com/a/1190000009077086) 进行 vscode 用户设置

## eslint不识别html文件顶部<!DOCTYPE html>
```bash
Parsing error: Unexpected token <
```

* 在相对应的工程中安装 eslint eslint-plugin-html

```bash
npm i -D  eslint eslint-plugin-html 
```

```json
{
    "plugins":[
        "html"
    ]
}
```

## vscode代码保存时自动格式化成ESLint风格（支持VUE）

* 用户配置
    - eslint.autoFixOnSave 用来进行保存时自动格式化，但是默认只支持 javascript .js 文件
    - "eslint.validate": [ "javascript", "javascriptreact", "html" ] 不生效 使用以下配置
```json
{
  "eslint.autoFixOnSave": true,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "vue",
      "autoFix": true
    }
  ]
}
```
    