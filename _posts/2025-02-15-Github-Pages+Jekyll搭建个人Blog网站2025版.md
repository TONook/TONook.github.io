---
layout: post
title: Github Pages+jekyll搭建个人Blog网站2025版
date: 2025-02-15 03:20 +0800
categories: [Tutorial]
tags: [Github Pages, jekyll，git]
pin: false
---

# 简单Blog搭建

2024Blog记录只进行了一次就草草结束，本文是再次从搭建Blog开始重新梳理，再启Blog之旅。且本次搭建Blog的方式相比2024版，采用Docker Desktop镜像并通过VSCode远程连接更加方便，虽然网络上已有诸多教程但还是为了记录这一过程写下这篇记录。

因笔者计算机基础知识薄弱，可能存在诸多低级错误，做此声明。

> 本文主要内容包括两部分，一是笔者不熟悉的一些基础概念的介绍聊作备忘，二是具体的实践步骤，只看具体过程请直接跳转[前期准备](#1-先决条件)。\
笔者采用[Chripy](https://github.com/cotes2020/jekyll-theme-chirpy/){: target="_blank"}，具体操作步骤也是和[官方教程En](https://chirpy.cotes.page/posts/getting-started/){: target="_blank"}、[官方教程zhCN](https://pansong291.github.io/chirpy-demo-zhCN/posts/getting-started/){: target="_blank"}一致。

需要注意的是，笔者在远程连接时总是出错，因此反复重新进行了好几遍才成功，其实关键非常简单，就是一定要保证网络环境的畅通，所以在操作前一定要确认这一点，再进行接下来的一系列copy操作就用不了几分钟啦！比如可以不用GitHub，改用Gitee。但笔者是个死脑筋所以还是继续在Github上尝试。。

## 0 概念学习

### 0.1 Github Pages和Jekyll是啥

### 0.2 Docker是啥

[如何优雅地删除Docker镜像和容器（超详细）](https://blog.csdn.net/u014282578/article/details/127866389){: target="_blank"}



## 1 先决条件

### 1.1 应用安装

- 根据官方教程[^ft1]，所需应用包括:
  1. [Docker Desktop](https://www.docker.com/products/docker-desktop/){: target="_blank"}
  2. [Ruby和Jekyll](https://jekyllrb.com/docs/installation/windows/){: target="_blank"}
  3. [GCC](https://blog.csdn.net/qq_45601448/article/details/109158588){: target="_blank"}
  4. [Make](https://blog.csdn.net/weixin_41896770/article/details/131262178){: target="_blank"}
  5. [git](https://blog.csdn.net/qq_29493173/article/details/113094143){: target="_blank"}

- 通过命令检查已经安装完毕\
  `ruby -v`, `gem -v`, `gcc -v`, `g++ -v`, `make -v`, `git -v`

- VSCode下载插件：Dev Containers


### 1.2 账号创建

- **配置Github仓库**：根据官方教程[^ft1]使用Starter新建仓库并命名为`username.github.io`，这样才能通过`https://username.github.io`的格式打开博客，其中username为GitHub账户名称
  > 如使用不是username命名，则可以通过`https://username.github.io/repositoryname`的格式进行访问

- **配置git**：因我之前有配置过另一个git账户，这次想换一个git账户并隐藏我的邮箱，则可以通过Github的[`noreply` email address](https://docs.github.com/zh/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address){: target="_blank"}且阻止会暴露个人电子邮件地址的命令行推送
  > 要查询及更改git配置的用户名及邮箱，使用如下命令配置私密邮箱
  > ```git
  > git config user.name
  > git config user.email
  > git config --global user.email "{ID}+{username}@users.noreply.github.com"
  > git config --global user.name "username"
  > ssh-keygen -t rsa -C "youxiang@xxx.com"
  > ```
  > 如允许使用个人电子邮箱则记得取消上面的勾选并在GitHub中同步邮箱的SSH，生成命令行时遇到输入密码等直接回车即可
  > ```git
  > ssh-keygen -t rsa -C "youxiang@xxx.com"
  > ```

## 2 配置

- **运行Docker Desktop**
- **启动VSCode并在容器卷中克隆仓库**[^ft2]
  - <kbd>fn</kbd>+<kbd>F1</kbd>：运行Dev Containers: Clone Repository in Container Volume...
  - 选择相应的仓库开始克隆
  - 保持网络畅通，等待一段时间，就能在VSCode里看到本网页的远程连接啦🎇

## 3 部署

- **本地部署**：在VSCode命令行输入`bundle exec jekyll s`，几秒后可通过`http://127.0.0.1:4000 `访问当前网页
- **Pages部署**：在`Settings -> Pages -> Build and deployment -> Source`中选择`Github Actions`，Github仓库中的代码同步好后就能自动构建，等待几秒，通过`https://username.github.io`就能访问，之后每次更新网页都会同步提醒update

## 4 更新

1. 在本地镜像进行的更改如何通过VSCode向远程仓库同步，可以参考：[[全网最详细]VS Code使用Git可视化管理源代码详细教程](https://blog.csdn.net/zls365365/article/details/125904062){: target="_blank"}
2. 具体如何更新当前站点内容可以参考：[Chirpy+Github](https://www.cnblogs.com/sprinining/p/18427216){: target="_blank"}


[^ft1]:[Jekyll安装指南](https://jekyllrb.com/docs/installation/){: target="_blank"}
[^ft2]:[仓库远程连接](https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume){: target="_blank"}
