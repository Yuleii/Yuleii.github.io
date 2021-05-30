---
layout: article
title: Jekyll博客自定义页面类型
key: 2020708
tags: Jekyll
pageview: false
modify_date: 2020-07-08
aside:
  toc: true
---

制作除博客（post）以外的新页面类型

<!--more-->

## 需求
我想在头部导航栏里新增一项独立的页面导航`Plog`用来存放照片，具体要求：
- 与博文独立，即更新的文章不出现在主页或`Archive`里
- `Plog`点开后显示封面，不直接显示文章
- 通过侧边栏导航文章，按年和月分类
- 文章是「图片卡」的容器，一张图片卡由照片，拍摄时间和描述三部分组成


## 解决方法


### 修改配置文件

- 在根目录下的`_config.yml`文件中添加以下代码自定义页面类型集合

```bash
collections:
  plog:
    output: true
```

- 在根目录下的`_config.yml`文件中添加自定义页面类型默认元数据

```bash
defaults:
  - scope:
      path: "_plog"
    values:
      layout: article
      nav_key: plog
      sidebar:
        nav: plog
      license: true
      aside:
        toc: true
      show_edit_on_github: true
      show_date: false
```

### 新建文件

- 在根目录下创建`_plog`文件夹用于存储发布照片的文章

- 在根目录下创建`plog.md`的markdown文件作为`plog`的封面,然后在头信息中将定义的导航作为这篇页面的侧边栏导航栏：

```bash
sidebar:
    nav: plog
```

### 配置导航栏

- 在`_data`文件夹下`navigation.yml`中的`header`配置中中添加以下代码设置头部导航栏

```bash
  - title:      plog
    url:        /plog.html
    key:        plog
```

- 在`_data`文件夹下的`navigation.yml`添加以下代码设置侧边栏导航栏，注意要放在`header`配置的后面

```bash
plog:
  - title:      2020
    children:
      - title:  June
        url:    /plog/june
```

### 创建文章

- 首先创建「六月」的文章，在`_plog`文件夹新建markdown文件`1.1-june.md`, 头信息中将定义的导航作为这篇文章的侧边栏导航栏

```bash
sidebar:
    nav: plog
```

- 要添加「七月」的文章，在`_plog`文件夹新建markdown文件`1.2-july.md`, 头信息同「六月」。然后在`_data`文件夹下的`navigation.yml`文件中添加以下代码设置侧边栏导航栏。要创建「2021」年新的大类，就在`header`中添加一个与「2020」同级的title，将新建的文章命名为2.1-jan，2.2-feb...即可

```bash
plog:
  - title:      2020
    children:
      - title:  June
        url:    /plog/june
      - title:  July
        url:    /plog/july
```

### 文章内容

```
<div class="card">
  <div class="card__image">
    <img class="image" src="https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/test.PNG"/>
  </div>
  <div class="card__content">
    <div class="card__header">
      <h4>2020年7月8日</h4>
    </div>
    <p>
      创建一个图片卡。
    </p>
  </div>
</div>
```

<div class="card">
  <div class="card__image">
    <img class="image" src="https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/test.PNG"/>
  </div>
  <div class="card__content">
    <div class="card__header">
      <h4>2020年7月8日</h4>
    </div>
    <p>
      创建一个图片卡。
    </p>
  </div>
</div>


* * *

## 参考链接

- [合并 Jekyll 多种类型的页面](https://blog.walterlv.com/post/jekyll/jekyll-concat.html)
- [jekyll-TeXt-theme documentation](https://tianqi.name/jekyll-TeXt-theme/docs/en/card)


