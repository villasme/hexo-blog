---
title: git-command
categories: git
tags: git
---

## git

* 当被跟踪的文件里面有不想跟踪的文件时，使用命令git rm删除文件
```bash
git rm --cached abc.txt    abc.txt的跟踪，并保留在本地。

git rm --f abc.txt    abc.txt的跟踪，并且删除本地文件。
```

* 在git init的目录下建立.gitignore文件，使用如下语法进行填写文件即可。
    - /abc/ 过滤整个文件夹
    - *.zip 过滤所有.zip文件
    - /mtk/do.c 过滤某个具体文件

* 指定要将哪些文件添加到版本管理中 
    *** 开头多了一个感叹号，Git会将满足这类规则的文件添加到版本管理中 ***
    - !*.zip
    - !/abc/1.md

