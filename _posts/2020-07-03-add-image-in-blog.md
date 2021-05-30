---
layout: article
title: 在Jekyll博客中插入图片
key: 20207031
tags: Jekyll
pageview: false
modify_date: 2020-07-03
aside:
  toc: true
---

使用 Github 作为图床在博文中插入图片

<!--more-->

- 在博客根目录下创建一个储存图片的文件夹`pictures`（或任何名字）
- 把需要插入的图片保存到`pictures`文件夹里并push到github远程仓库
- 在github仓库中打开图片，复制url，如 https://github.com/Yuleii/Yuleii.github.io/blob/master/pictures/test.PNG
- 将URL中blob替换为raw，即 https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/test.PNG
- 使用markdown插入图片的语法即可显示图片

```
![test](https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/test.PNG) 
```
![test](https://github.com/Yuleii/Yuleii.github.io/raw/master/pictures/test.PNG) 