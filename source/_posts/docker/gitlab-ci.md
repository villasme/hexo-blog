---
title: docker-gitlab-ci
categories: docker
tags:
- docker
- gitlab-ci/cd
---


## 安装gitlab-runner

```bash
docker pull gitlab/gitlab-runner
```

## 启动gitlab-runner

```bush
docker run -d --naner gitlab_runner gitlab/gitlab-runner
```

## exec gitlab-runner

```bash
docker exec -it gitlab_runner /bin/bash
```

## register gitlab-runner

```bash
$ gitlab-ci-multi-runner register
Running in system-mode.                            
                                                   
Please enter the gitlab-ci coordinator URL (e.g. https://gitlab.com/):
$ http://10.165.1.28:10080/
Please enter the gitlab-ci token for this runner:
$ wy1GDVZzCDghXp9pT_zP
Please enter the gitlab-ci description for this runner:
$ [8e4616616295]: gitlab-ci
Please enter the gitlab-ci tags for this runner (comma separated):
$ test,demo
Registering runner... succeeded                     runner=wy1GDVZz
Please enter the executor: virtualbox, docker+machine, kubernetes, docker-ssh, shell, ssh, docker, parallels, docker-ssh+machine:
$ shell
Runner registered successfully. Feel free to start it, but if it's running already the config should be automatically reloaded!
```

## 查看runner

```bash
gitlab-ci-multi-runner list
```

## gitlab操作

* 创建工程
* 查看 ci/cd （含有 gitlab-runner-ip&&hash）
* 创建.gitlab-ci.yml

```yml
# 定义stages
stages: 
    - build
    - test
    - deploy
# 定义jobs
job1:
    stage: test
    tags:
        - demo
    script:
        - echo "I am job1"
        - echo "I am in test stage"
job2:
    stage: build
    tags:
        - demo
    script:
        - echo "I am job2"
        - echo "I am in build stage"
job3:
    stage: deploy
    tags:
        - demo
    script:
        - echo "I am job3"
        - echo "I am in deploy stage"

```

## 不是必备的修改- 修改gitlab 域名

```bash
# 我是docker 创建的
# 进入容器
docker-compose exec gitlab bash

# 修改配置文件
vi /opt/gitlab/embedded/service/gitlab-rails/config/gitlab.yml

# 配置文件修改的位置
 production: &base¬
   #¬
   # 1. GitLab app settings¬
   # ==========================¬
 ¬
   ## GitLab settings¬
   gitlab:¬
    ## Web server settings (note: host is the FQDN, do not include http://)¬
     host: xxxxxxx.cn¬ // 原域名
     port: 81¬
     https: false


# 重启gitlab
gitlab-ctl restart
```

