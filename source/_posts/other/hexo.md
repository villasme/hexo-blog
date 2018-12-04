---
title: hexo 标签不显示问题
categories: other
tags: 
- hexo
---

## tags 标签不显示

* 新建一个页面，命名为 tags 。命令如下：

```bash
hexo new page "tags"
```

* 编辑刚新建的页面，将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：(type: "tags" 一定要加引号) 

    title: 标签
    date: 2018-09-07 11:45:56
    type: "tags"
    comments: false

* 在菜单中添加链接。编辑 主题配置文件 ，添加 tags 到 menu 中，如下:

``` yml
menu:
  home: /
  archives: /archives
  tags: /tags
```

* 基于scaffolds/post 中的模板创建新的 md文件
```bash
hexo new post yourname
```

* 创建分类配置
```bash
hexo new page categories
```

* 创建标签配置
```bash
hexo new page tags
```

## hexo 增加评论系统

* https://ryanluoxu.github.io/2017/11/27/Hexo-Next-%E6%B7%BB%E5%8A%A0-Gitment-%E8%AF%84%E8%AE%BA%E7%B3%BB%E7%BB%9F/   亲测可用
* 我的评论系统不可用问题 是因为 没有开启配置     ：  lazy: true #

## postman 启动爬虫

* https://www.getpostman.com/apps