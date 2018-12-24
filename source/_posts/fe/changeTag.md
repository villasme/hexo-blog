---
title: 监听浏览器标签页切换事件“visibilitychange”
date: 2018-12-24 10:12:58
categories: FE
tags:
- javascript
---

| 正如标题所示；当我们切换标签页时，可动态控制标题的切换；直接上code

```html
<!DOCTYPE html>
    <head>
        <meta charset="UTF-8">
        <title>测试</title>
    </head>
    <script>
        document.addEventListener('visibilitychange',function(){
        if(document.visibilityState=='hidden') {
        normal_title=document.title;
        document.title='(づ￣ 3￣)づ不要离开';
        }
        else
        document.title=normal_title;
        });
    </script>
    <body onbeforeunload="checkLeave()">
        测试
    </body>
</html>

```