---
title: docker本身遇到的一些问题
categories: docker
tags:
- docker
---

## 如何在Docker的构建上下文之外包括文件

* 使用-f独立于构建上下文指定Dockerfile。

```sh
# 例如，此命令将给ADD命令访问当前目录中的任何内容。
# 这个 . 就是在Dockerfle中的上下文 
docker build -f docker/Dockerfile .
```

## 如何批量删除已经挂掉的容器？

```sh

# 运行中的容器不会被删除掉
docker rm $(docker ps -a -q)

#根据容器的状态，删除Exited状态的容器
docker rm $(docker ps -a -qf status=exited))

```