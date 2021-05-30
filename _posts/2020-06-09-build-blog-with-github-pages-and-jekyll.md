---
layout: article
title: 用 Github pages 和 Jekyll 搭建博客
key: 20200609
tags: Jekyll Github
pageview: false
modify_date: 2020-06-12
aside:
  toc: true
---


搭建本博客的经验

<!--more-->


## 创建gitpage仓库
在github上创建一个新的仓库，Repository name 填your_user_name.github.io, 例如我的仓库名是 Yuleii.github.io。创建成功后，在浏览器里输入 https://Yuleii.github.io/ 这个url就可以访问了。

## 选一个主题
### 主题网站
[jekyllthemes](http://jekyllthemes.org/)有很多免费主题可以挑选。我最喜欢[jekyll-TeXt-theme](https://github.com/kitian616/jekyll-TeXt-theme)这个主题，页面简洁，有很多个性化的配置，还有非常详细的中英文档。

### 主题下载
我的办法是把主题克隆到本地，删除原有的git文件，再与自己的仓库关联起来，但建议用[jekyll-TeXt-theme中文文档](https://tianqi.name/jekyll-TeXt-theme/docs/zh/quick-start)推荐的fork方式。

## 安装Jekyll本地编译环境
### 安装 RubyGems

一般macos已经有RubyGems环境了，所以只需要检查一下版本

```bash
$ ruby -v
```
如果检查到没有就安装
```bash
$ brew install ruby
```

### 安装Jekyll

```bash
$ sudo gem install jekyll
$ sudo gem install jekyll bundler
```
### 安装bundler
```bash
$ sudo bundle install
```
## 开启本地实时预览
```bash
$ cd {local repository} // {local repository}替换成你的本地仓库的目录
$ bundle exec jekyll serve
```
这个命令可以生成一个站点：http://127.0.0.1:4000/, 即目前的博客站点。只要 jekyll serve 服务开着，你的本地仓库文件有任何更新，本地网站刷新都能马上看到。

## 编辑模版
### Jekyll 目录结构
jekyll目录结构主要包含如下目录：
- _posts 博客内容
- _pages 其他需要生成的网页，如About页
- _layouts 网页排版模板
- _includes 被模板包含的HTML片段，_config.yml中修改位置assets 辅助资源 css布局 js脚本 图片等
- _data 动态数据
- _sites 最终生成的静态网页
- _config.yml 网站的一些配置信息
- index.html 网站的入口


建议再新建一个_drafts，没写完的文章可以先放这里，编写完成后再拖到_posts。

### 修改配置文件
在_config.yml根据自己的需求修改配置数据。[jekyll TeXt 配置文档](https://tianqi.name/jekyll-TeXt-theme/docs/zh/configuration)列出了非常详细的步骤。


## 撰写博客
### 编辑器
推荐vscode，因为可以一边写markdown一边预览。
### 创建文章
在_post文件夹新建一个markdown格式的文件，命名格式为：
```md
年-月-日-标题.MARKUP
```
例如：
```md
2011-12-31-new-years-eve-is-awesome.md
2012-09-12-how-to-write-a-blog.markdown
2020-06-09-build-blog-with-github-pages-and-jekyll.md

```

### YAML头信息
头信息必须在文章的开始部分：
```
---
layout: article
title: Document - Writing Posts
mathjax: true
---
```
在这两行的三虚线之间，可以设置在_config.yml预定义的变量或创建一个自己定义的变量。

### 选择文章布局方式
除去Jekyll自定义的变量和布局外，TeXt也提供了不同的布局可以选择: [TeXt page layout samples](https://tianqi.name/jekyll-TeXt-theme/samples.html)，使用时改变头信息即可。本文采用的是Page-Aside格式。

### 发布文章
文章保存到_post后，push到github远程仓库即可。


## 参考链接
- [jekyll中文文档](http://jekyllcn.com/)
- [jekyll-TeXt-theme中文文档](https://tianqi.name/jekyll-TeXt-theme/docs/zh/quick-start)  
- [Github Pages + Jekyll 独立博客一小时快速搭建&上线指南](https://www.jianshu.com/p/7593508666f8)  
- [Github+Jekyll 搭建个人网站详细教程](https://www.jianshu.com/p/9f71e260925d)  
- [Jekyll 博客系列 - 01 快速入门(Youtube)](https://youtu.be/Zt_QzSbyDcw)

## 我遇到的问题（持续更新）
> **Q:** 如何调大代码字体？  
>  **A:** 找到 _sass\common_reset.scss ，将里面 code 中 font-size-sm 改成 font-size

> **Q:** 怎么控制显示在主页的摘要内容？  
  **A:** 在文章摘要和正文中间加上 `<!--more-->` 

> **Q:** 我的两篇post点开怎么是同一篇的内容？  
> **A:** 把头信息里的 permalink 删除

> **Q:** 如何隐藏pageview  
> **A:** 在头信息里添加变量：`pageview: false`   

> **Q:** 为什么在_config.yml修改了配置不在本地实时预览时显示   
> **A:** 修改了_config.yml的内容需要重启实时预览才能显示