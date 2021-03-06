---
title: vscode 插件与功能使用
categories: FE
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
|Import Cost|检测导入文件的大小|
|Version Lens|显示package 软件包版本信息|
|Package watcher| package.json修改后 可以自动下载删除包 （单层目录才可以）|
|Debugger for chrome|谷歌调试debug|
## prettier - code formatter 自定义格式化文件

* 需要在工程中配置 .prettierrc 参数解释参考：https://segmentfault.com/a/1190000012909159

``` json

   {
    "eslintIntegration": true,
    "stylelintIntegration": true,
    "tabWidth": 2,
    "singleQuote": true,
    "semi": false
}
```

## Debugger for chrome - 谷歌调试debug

### vscode 调试 TS react 项目
1. 先安装vscode插件 Debugger for chrome
2. 配置launch 文件

   ```json
   {
     // 使用 IntelliSense 了解相关属性。 
     // 悬停以查看现有属性的描述。
     // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
     "version": "0.2.0",
     "configurations": [
       {
         "type": "chrome",
         "request": "launch",
         "name": "Launch Chrome against localhost",
         "url": "http://qci1.aliyun.com/userMarketing/",
         // 本地项目中的路径
         "webRoot": "${workspaceFolder}/src",
         // 一定要false 为了在当前文件中调试，而不是跳到 “源映射中的只读内联内容”
         "sourceMaps": false,
         // 未了解
         "skipFiles": ["node_modules/**"],
         // 加载webpack中的脚本资源
         "sourceMapPathOverrides": {
           "webpack:///src/*": "${webRoot}/*"
         }
       }
     ]
   }
   ```
3. 命令窗口中优先启动本项目
4. vscode中打开debug
5. 打断点，成功