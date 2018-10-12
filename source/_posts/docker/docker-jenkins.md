---
title: 使用docker部署jenkins与碰到的一些问题
categories: docker
tags:
- docker
- jenkins
---

# nginx

## docker-compose 安装nginx

* 安装docker环境

* 新建jenkin/docker-compose.yml

```yml
version: "3"

services:
  jenkins:
    restart: always
    image: jenkins/jenkins
    ports:
      - 18080:8080
    volumes:
      - /home/tong/demo/jenkins/jenkins_home:/var/jenkins_home
```
* 到目前为止我们已经可以用 ip:18080 来访问 jenkins了

## 我个人遇到的问题

* 如果新创建的任务使用gitlab库的时候，配置选项中的源码管理可以选择git,Repository URL	字段使用http时， 	Credentials： 可以配置账号加密码。 如果是 git@*****.git  Credentials：要配置公钥。

    ![](/images/docker/gitPage@2x.png)

* (我的gitlab,jenkins在一个服务器上面)我想通过jenkins构建功能 在服务器上面使用docker来部署前端环境或者使用nginx部署静态文件
    > 使用到了 Publish Over SSH 插件  需要在jenkins 中进行安装。
    ![](/images/docker/public-ssh.jpg)
    1. 使用docker-compose exec jenkins bash 进入容器内部
    2. 在容器内部ssh-keygen -t rsa  生成秘钥对
    3. 在服务器下（eg:我的服务就是10.165.1.28） ~/.ssh/authorized_keys 文件中 注入 上面容器中生成的 公钥（id_rsa.pub）
    4. 重启服务器的 ssh  ---   service sshd restart  我没有重启这个步骤可参考
    5. 下面是1.28 ssh 的设置
    ![](/images/docker/publish-ssh-set.jpg)