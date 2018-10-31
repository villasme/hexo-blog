---
title: python Scrapyd 爬虫日记
categories: other
tags: 
- python
- scrapyd
---

## 爬虫部署管理控制台 开始学习的步骤

1. 新建项目。
2. 新建爬虫、
3. 编写配置文件。
4. 打包部署。
5. 到平台上检查

## Anaconda完全入门指南

* 很多学习python的初学者甚至学了有一段时间的人接触到anaconda或者其他虚拟环境工具时觉得无从下手, 其主要原因就是不明白这些工具究竟有什么用, 是用来做什么的, 为什么要这么做, 比如笔者一开始也是不明白为啥除了python之外我还需要这么一个东西, 他和python到底有啥联系和区别, 为啥能用来管理python.
* 参考： https://www.jianshu.com/p/eaee1fadc1e9

## 开始使用
* 新建一个名为ljt 的 scrapy 项目 

```sh
scrapy startproject ljt

cd ljt
```
* 修改cfg 将 url 指向 http://porters.vip

```conf

# Automatically created by: scrapy startproject
#
# For more information about the [deploy] section see:
# https://scrapyd.readthedocs.io/en/latest/deploy.html

[settings]
default = ljt.settings

[deploy:locals]
url = http://porters.vip:6800/
project = ljt

```
* 通过命令将 ljt 项目打包并部署到服务上

```bash
scrapyd-deploy locals -p ljt
```

## 创建爬虫

```bash
scrapy genspider -t basic csdn csdn.com
```

## 如启动指定爬虫

```bash
curl http://localhost:6800/schedule.json -d project=SMTaobao -d spider=smtb
```


## 记录一下conda,brew,pip的安装位置
* /Users/zj_macbook/anaconda/envs/python3/lib/python3.6/site-packages
* https://blog.csdn.net/machinezj/article/details/60466962