---
title: 如何使用docker 搭建 私服npm
categories: docker
tags:
- docker
- npm
---

# 使用verdaccio 搭建 私服 Npm

## 首先安装 verdaccio/verdaccio

```bash
$ docker pull verdaccio/verdaccio
```

## 编写 docker-compose.yml 文件

```yml
version: '3'

services:
    npm:
      restart: always
      image: verdaccio/verdaccio
      ports:
        - 4873:4873

```
完成 启动即可

## 使用

1. 进入容器

```sh
docker-compose exec npm sh
```
2. 查看全局包的位置如下名：

```sh
npm root -g
```

3. 以上步骤可以忽略

4. 初始没有用户 - 但是我们可以注册（刚开始我还以为有初始用户与密码呢）

```sh
## 其实界面有提示的
# login
npm adduser --registry  http://*****:4873
# publish
npm publish --registry http://******:4873

# ok 啦 
```