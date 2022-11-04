---
title: 在hexo中无痛使用本地图片
top: false
cover: false
toc: true
mathjax: true
date: 2022-11-04 09:57:08
password:
summary: 在hexo中使用本地图片是件非常让人纠结的事情
tags:
    hexo
categories:
    - hexo
---

## 1 起因 

在 hexo 中使用本地图片是件非常让人纠结的事情，在 markdown 里的图片地址似乎永远无法和最后生成的网页保持一致。

这些问题使得我一度不愿意使用本地图片而选择用图床，但被移动运营商无耻的横条广告逼得打算上 https，图床只支持 http 就成了问题。

hexo 下插入图片现在大概有几个方案

### 1.1 放在根目录 

早期大部分的方案是把图片放在 `source/img` 下，然后在 markdown 里写 `![img](/source/img/img.png)` 。显然这样在本地的编辑器里完全不能正确识别图片的位置。

### 1.2 asset-image 

在 hexo 2.x 时出现的插件，后来被吸纳进 `hexo 3 core` ，用法的介绍见 [资源文件夹 | Hexo][_ Hexo] 。比较尴尬的是，这种方法直接放弃了 markdown 原来的语法，使用类似 ``的语法，。markdown 本来有插入图片的语法不好好支持，专门用一个新的语法来插入本地图片，让我这种强迫症不太能接受。

## 2 解决方案 

[CodeFalling/hexo-asset-image][CodeFalling_hexo-asset-image]

### 2.1 使用 

首先确认 `_config.yml` 中有 `post_asset_folder:true` 。

在 hexo 目录，执行

```java
npm install https://github.com/CodeFalling/hexo-asset-image --save
```

假设在

```java
MacGesture2-Publish
├── apppicker.jpg
├── logo.jpg
└── rules.jpg MacGesture2-Publish.md
```

这样的目录结构（目录名和文章名一致），只要使用 `![logo](MacGesture2-Publish/logo.jpg)`就可以插入图片。

生成的结构为

```java
public/2015/10/18/MacGesture2-Publish
├── apppicker.jpg
├── index.html
├── logo.jpg
└── rules.jpg
```

同时，生成的 html 是

```java
<img src="/2015/10/18/MacGesture2-Publish/logo.jpg" alt="logo">
```

而不是愚蠢的

```java
<img src="MacGesture2-Publish/logo.jpg" alt="logo">
```

值得一提的是，这个插件对于 [CodeFalling/hexo-renderer-org][CodeFalling_hexo-renderer-org] 同样有效。