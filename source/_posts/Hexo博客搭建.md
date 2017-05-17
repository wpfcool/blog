---
title: Hexo博客搭建
date: 2016-04-17 11:08:26
tags: [Hexo]
---


## 1. 安装 Homebrew

```
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```
## 2. 安装nodejs

```
brew install node

```
## 3. 安装hexo

```
npm install -g hexo
hexo init
```

## 4.  修改hexo根目录下_config.yml文件（xxx为你的github账户名称）

```
deploy:
type: github
repo: git@github.com:xxx/xxx.github.io.git
branch: master
```
## 5.  注册github账号，新建名为xxx.github.io的repository
## 6.  到这，Hexo博客搭建已经完成了，并且可以git提交到github上，通过访问xxx.github.io就可以访问本博客

