# 我的博客日记！ http://blog.liujiantong.cn

## 启动
* yarn
* hexo server

## 生成一个文本
* hexo new post 自定义名字 

## 部署
* 任意一个即可

```sh
hexo generate --deploy
hexo deploy --generate

# 简写
hexo g -d
hexo d -g
```

## tree

```sh
sudo apt-get install tree
tree -L 3 -d -h -I "node_modules|public|themes"
-L 2层
-d 展示文件夹
-h 展示可读的大小
-I 过滤匹配的字符
```

## 目录
```sh
├── [4.0K]  scaffolds
└── [4.0K]  source
    ├── [4.0K]  categories
    ├── [4.0K]  images
    │   └── [4.0K]  docker
    ├── [4.0K]  _posts
    │   ├── [4.0K]  docker
    │   ├── [4.0K]  fe
    │   ├── [4.0K]  git
    │   ├── [4.0K]  linux
    │   └── [4.0K]  other
    └── [4.0K]  tags



```


## 主题
* git clone https://gitlab.com/newHotCat/hexo-next-page.git   到 hexo-blog/themes/next
* https://hexo.io/zh-cn/docs/deployment


## gitment 不能登陆问题

* https://sjq597.github.io/2018/05/18/Hexo-%E4%BD%BF%E7%94%A8Gitment%E8%AF%84%E8%AE%BA%E5%8A%9F%E8%83%BD/