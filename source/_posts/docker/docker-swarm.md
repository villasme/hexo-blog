---
title: 容器编排与集群
categories: docker
tags:
- docker
- swarm
---
## 准备环境
> vagrant + VirtualBox + centos7.box
```sh
# 全新centos7环境
1  sudo yum install docker 
2  sudo docker pull nginx
3  sudo service docker start // 启动docker 服务
9  sudo systemctl list-unit-files   // 查看自启服务列表
10  sudo systemctl list-unit-files  | grep docker // 查看docker是否自启
12  sudo systemctl enabled  docker.service 
13  sudo systemctl enable docker.service   // 开机自启docker
15  sudo groupadd  docker   // 添加docker组
16  cat /etc/group          // 查看有哪些组
17  sudo usermod -a -G docker ${USER}  // 把当前用户添加到docker组中(为了不用sudo)
20  sudo yum install curl   // 安装下载工具
21  sudo systemctl stop firewalld.service // 关掉防火墙
22  sudo systemctl disable firewalld.service // 禁止防火墙自启
23  sudo docker images  // 查看docker镜像
24  sudo docker pull nginx // 下载nginx
71  docker swarm init --advertise-addr 192.168.33.10 // 建立manager

```
* 安装docker-compose

```sh
sudo yum install curl
sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

```

* 使用docker-compose up 报错解决方案

```sh
[vagrant@ip10 nginx]$ docker-compose up
Creating network "nginx_default" with the default driver
Creating nginx_nginx_1 ... 
Creating nginx_nginx_1 ... error

ERROR: for nginx_nginx_1  Cannot create container for service nginx: error creating overlay mount to /var/lib/docker/overlay2/5391707b6a2981cfac84efb738e70ab1b82e90700eb7acd926a7a9df232618f9-init/merged: invalid argument

ERROR: for nginx  Cannot create container for service nginx: error creating overlay mount to /var/lib/docker/overlay2/5391707b6a2981cfac84efb738e70ab1b82e90700eb7acd926a7a9df232618f9-init/merged: invalid argument
ERROR: Encountered errors while bringing up the project.
```
1. 修改存储类型
```sh
#停止docker服务
vi /etc/sysconfig/docker-storage
# 把空的DOCKER_STORAGE_OPTIONS参数改为overlay:
DOCKER_STORAGE_OPTIONS="--storage-driver overlay"
```
<!-- 2. 禁用selinux 可以不用
```sh
vi /etc/sysconfig/docker
# 去掉option的--selinux-enabled
``` -->
2. 
```启动docker
systemctl restart docker
```