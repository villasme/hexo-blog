---
title: vscode 插件与功能使用
tags: 
- vscode
---

## 插件区

|插件名|作用|
| :----- | :------- |
|Markdown Preview Enhanced | markdown的视图工具|
|gitlens | git每一行提示信息与分支|
|vscode -fileheader |　文件头部信息 (ctre+alt+i使用)|
|auto close tag| 自动合并html|
|bracket pair colorizer |括号变色|
|power Mode  ***  | 超绚丽的 代码特效|
|path intellisense  | 找到相对路径中的文件|
|prettier - code formatter | 代码自动格式化 |
|vetur | vue格式化工具 （格式化 html"vetur.format.defaultFormatter.html": "" ）|
|vim  | 使用 vim|

## prettier - code formatter 自定义格式化文件

* 需要在工程中配置 .prettierc 

``` json

   {
    "eslintIntegration": true,
    "stylelintIntegration": true,
    "tabWidth": 2,
    "singleQuote": true,
    "semi": false
}
```