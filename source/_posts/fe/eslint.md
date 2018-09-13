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