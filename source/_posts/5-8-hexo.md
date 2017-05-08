---
title: 使用hexo搭建静态博客
date: 2017-05-08 21:43:34
tags: blog
categories: blog
---

之前的博客因为域名和主机到期未续费的原因挂了，作为一个前端程序猿，没有一个个人博客实在是说不过去,所以花了一些时间用hexo搭建了一个简单的静态博客，因为本人记忆不太好为了避免以后忘了再去找教程，也为了方便各位同仁就简单的写了一个教程，当然也可以参考Hexo官网。

---
## 配置环境
1. 安装[NodeJs](https://nodejs.org/en/)。
2. 安装[Git](https://git-scm.com/downloads)。
3. 申请(Github)[https://github.com/] 账号。

---
## 安装hexo
使用 npm 安装 Hexo:
```bash
$ npm install -g hexo-cli
```
进入指定目录，初始化:
```bash
$ cd your_project
$ hexo init
```
生成静态文件:
```bash
$ hexo generate
```
启动本地服务:
```bash
$ hexo server
```
访问https://localhost:4000, 在启动本地可能会报错，可执行：
```bash
$ npm install
```

---
## 发布文章
```bash
$ hexo new "Name"
```
文章默认在source_posts\Name.md,然后就可以使用Markdown写文章了，可参照Markdown语法。文章编写完成后，执行以下操作,访问https://localhost:4000 预览：
```bash
$ hexo generate
$ hexo server
```

---
## 配置到Github
### 建立Repository
在github建立与你用户名对应的仓库，仓库名必须为your_user_name.github.io。

找到_config.yml：
```
deploy:
  type:
  repository:
  branch:
```
修改为：
```
deploy:
  type: git
  repository: https://github.com/your_user_name/your_user_name.github.io.git
  branch: master
```
最后执行：
```bash
$ hexo deploy
```
这里我使用的是https,会要求你输入github的username和password。当然也可以使用SSH Keys就不做过多介绍，具体请google。

当最后出现:
```
INFO  Deploy done: git
```
恭喜你！！！你的博客已经发布成功，可以访问http://your_user_name.github.io/ 查看了。

---
## hexo 主题
hexo拥有很多优秀的主题，具体可以访问[themes官网](https://hexo.io/themes/)，这里就不做推荐了，免得被吐槽我的审美23333。
