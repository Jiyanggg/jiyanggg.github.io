---
layout: post  
title: Obsidian 对接 Github Page
subtitle: 将 Obsidian 上的文档自动发布到 Github Page 上
cover-img: /assets/img/mountain.jpg  
thumbnail-img: /assets/img/hello-world.png  
share-img: /assets/img/mountain.jpg  
tags: [Obsidian]  
---  

## 基于 Github + Jekyll 搭建静态博客网站

我选择的是 [beautiful-jekyll](https://github.com/daattali/beautiful-jekyll) 模板，比较简洁而且支持添加文章缩略图



## 更改博客目录结构 & .gitgnore 文件

1、 Fork & Clone 到本地计算机，对 index.html 等个性化文件及配置进行修改。

2、 在根目录下新建 `obsidian` 文件夹作为我们将要下载安装的笔记软件 `Obsidian` 的 `WorkSpace` 

3、 然后在 `obsidian` 目录下建立子文件 `_posts`

4、 修改根目录中的 `.gitignore` 文件，添加以下命令（即仅发布 /obsidian/_posts/*.md 至 Github Page，很关键!）

```
/obsidian/*  
!/obsidian/_posts  
/obsidian/_posts/*  
!/obsidian/_posts/*.md
```

目录结构参考

``` 
├── .github
├── _data
├── _includes
├── _layouts
├── _posts
├── assets
├── dosc
├── obsidian
│ ├── _posts
│ ├── daily
│ ├── weekly
│ ├── unsorted
│ ├── xxxx
├── .gitignore
├── _config.yml
├── index.html
├── xxxx
```

## 安装 Obsidian 

去 [官网](https://obsidian.md/download) 下载安装 `Obsidian`。安装完成后在客户端左侧选择打开其他库，选择上一步创建的 `obsidian` 文件夹作为 `WorkSpace`


## 安装 Obsidian Git 插件

在 `Obsidian` 客户端左侧点击设置，然后第三方插件 `Obsidian Git`，配置你想要的自动 Push & Pull 频率（我的选择是 10 分钟自动 Pull，手动 Push）

NOTE: 如果你的 Github 博客项目是 Private 的，你需要在 Github Setting 配置本地电脑的 SSH Keys

## 整理发布笔记

将你想要发布的文章放到 `obsidian/_posts` 文件夹下，在 Obsidian 客户端 `Ctrl + P` -> `Git Commite all changes` -> `Ctrl + P` -> `Git Push`，接着你会发现你的 Github Page 出现你新发布的文章

  


