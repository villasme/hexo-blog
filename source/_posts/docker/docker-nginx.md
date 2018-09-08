---
title: docker-nginx
categories: docker
---

# nginx

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