---
title: docker-nginx
categories: docker
tags:
- docker
- nginx
---

# nginx

## docker-compose 安装nginx

* 安装docker环境

* 新建nginx/docker-compose.yml

```yml
version: "3"
services:

  nginx:
    restart: always
    image: nginx
    ports:
      - 80:80
    volumes:
      - ./conf.d:/etc/nginx/conf.d
      - ./log:/var/log/nginx
      - ./www:/var/www
      - /etc/letsencrypt:/etc/letsencryp
```
-------------
[参数说明---docker-compose使用](https://www.jianshu.com/p/1f6232d787d9)

- version：版本号，好像我这上面2和2.0有区别，不能写成2，写成2的话，docker-compose up -d 时会报错，提示版本号要写成2.0的样子，不过有的地方我看着直接写成2也是可以的，可能是我的docker-compose版本不一致。
- service：就是要定义的docker容器
- nginx:容器的名称
- restart：设置为always，表明此容器应该在停止的情况下总是重启，比如，服务器启动时，这个容器就跟着启动，不用手动启动，服务器启动之后，进入到docker-compose.yml文件路径下，执行docker-compose ps可以看到，该容器正在运行。
- image：这个是需要依赖的容器，也就是nginx软件，可以到docker官方镜像上找到最新版的镜像。
- ports：这个是容器自己运行的端口号和需要暴露的端口号。比如： - 8080:80，表示容器内运行着的端口是80，把端口暴露给8080端口，从外面访问的是8080端口，就能自动映射到80端口上。
- volumes:这个是数据卷。表示数据、配置文件等存放的位置。（- . 这个表示docker-compose.yml当前目录位置开始创建这个文件）

## 使用docker-compose 启动 nginx

* docker-compose up -d
* 在docker-compose.yml 目录下

## 拷贝默认conf.d 中的文件 与 www 文件

* 上面步骤完成后 ，在当前文件夹下面会创建出 www/ conf.d
* 在www/下创建 index.html
* 把下面配置拷贝到 conf.d/default.conf 中
* 注意： docker-compose.yml 中把静态目录挂在到了 /var/www 上; nignx的默认 (/) 根目录是 /usr/share/nginx/html

```conf
server {
    listen       80;
    server_name  localhost;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /var/www;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
    #
    #location ~ \.php$ {
    #    root           html;
    #    fastcgi_pass   127.0.0.1:9000;
    #    fastcgi_index  index.php;
    #    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
    #    include        fastcgi_params;
    #}

    # deny access to .htaccess files, if Apache's document root
    # concurs with nginx's one
    #
    #location ~ /\.ht {
    #    deny  all;
    #}
}
```

## 挂载数据

```
# 初始化 docker nginx 内部文件配置 进行迭代配置
docker cp nignx:/etc/nginx/conf.d/default.conf ${PWD}/conf.d/default.conf

# 启动nginx 服务
docker run --name nginx -p 10000:80 -d -v ${PWD}/html:/usr/share/nginx/html -v ${PWD}/conf.d:/etc/nginx/conf.d  nginx
```

## docker cp 命令
``` 
将主机/www/runoob目录拷贝到容器96f7f14e99ab中，目录重命名为www。

docker cp /www/runoob 96f7f14e99ab:/www
将容器96f7f14e99ab的/www目录拷贝到主机的/tmp目录中。

docker cp  96f7f14e99ab:/www /tmp/
```

## guwen.conf 

``` config
server {
    listen       80;
    server_name  a1.demo.com;

    #charset koi8-r;
    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    location /a {
        proxy_pass http://tomcat_guwen_cluster;
    }
}
```

## upstream_guwen.conf 

```
  # 这里可以做扩展 负载均衡
  upstream tomcat_guwen_cluster {
        server 10.165.1.17:8080;
  }
```
