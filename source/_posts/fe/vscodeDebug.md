---
title: vscode debug
categories: FE
tags: 
- vscode
- debug
---

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