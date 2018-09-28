---
title: docker-gitlab
categories: docker
tags:
- docker
- gitlab
---

## 在docker中 下载 gitlab

```bash
$ docker pull gitlab/gitlab-ce
```

## 创建docker-compose

```yml
version: '3'
services:
  gitlab:
    container_name: gitlab
    image: gitlab/gitlab-ce:latest
    restart: always
    ports:
      - "10080:80"
      - "443:443"
      - "2224:22"
    volumes:
      - "/srv/gitlab/config:/etc/gitlab"
      - "/srv/gitlab/logs:/var/log/gitlab"
      - "/srv/gitlab/data:/var/opt/gitlab"

```

## docker-compose 启动

```bash
# gitlab

docker-compose up -d
## 启动以后不要着急 要等一会才能访问的到
```

## 访问

* 如过不是80端口 访问ip:端口
