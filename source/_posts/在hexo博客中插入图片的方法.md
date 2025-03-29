---
title: 在hexo博客中插入图片的方法
date: 2025-03-29 23:03:20
tags:
   - hexo
---

# 背景

&emsp;&emsp;博客搭建完成之后，在我发布文章时，发现文章的图片不同于普通markdown文件中的图片可以简单地使用相对路径来展现，在查阅官方文档和其他博主的文章后，整理了几种插入图片的方法步骤。

# 如果图片文件在本地

## 方法一：全局资源文件夹

&emsp;&emsp;将所有的图片文件都存在hexo文件夹下的source目录下的某个文件夹内，我们且称为images（由你自己创建和命名），将所有的资源通过这一个文件夹来进行统一管理。好处是便于使用，多篇文章可以使用同一个图片文件。不便的是，在你文章资源量逐渐变大后，文件夹内的资源便无法简便地管理，于是我们有了方法二：文章资源文件夹，在下一节介绍。

### 使用全局资源文件夹的具体步骤：

&emsp;&emsp;首先在hexo文件夹下的source目录下创建images（自己随意命名）文件夹，在存入文章资源后，在md文件中可以使用`![图片](图片链接地址 "图片title")`，注意：在写相对路径时，根目录为source文件夹，并不是hexo项目文件夹，所以假如images文件夹下有一个name.jpg图片文件，那么圆括号内的文件地址就是(/images/name.jpg)。下面是例子：`![我的狗](/images/my_dog.jpeg)`

![我的狗](/images/my_dog.jpeg)

## 方法二：文章资源文件夹

&emsp;&emsp;所以，这种方法就是使用多个文件夹来分别管理各个文章的资源，相比于方法一，就是便于结构化管理，前提是要开启功能，在hexo文件夹根目录下_config.yml文件内增加如下字段：（来源于hexo官方文档）

```yaml
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

### 使用文章资源文件夹的具体步骤：

1. 首先是在`hexo new [layout] <title>`创建新文章，此时会在hexo文件夹的source目录下，自动创建一个.md文件和同名文件夹，文件夹内就是放置你的资源文件，我们可以将所有与该文章有关的资源（包括图片）放在这个同名文件夹中。
2. 之后写文章可以通过相对路径来引用图片资源，例如，将“1.jpeg”这个图片资源放在该文件夹中，并在.md文件中像这样引用图片：`![图片](1.jpeg)`，这个方法在资源较多时方便管理。

例子：同样是狗狗图片，使用`![我的狗](my_dog.jpeg)`

![我的狗](my_dog.jpeg)

# 如果图片文件是网络文件

- 这个与在写普通md文件时没有两样，我拿github的头像来验证，内容为：`![头像](https://avatars.githubusercontent.com/u/154865877?v=4)`

![头像](https://avatars.githubusercontent.com/u/154865877?v=4)

# 参考：

1. [hexo官方文档](https://hexo.io/zh-cn/docs/asset-folders)
2. [kathy-tx的csdn博客](https://blog.csdn.net/2301_77285173/article/details/130189857)
