---
title: hexo笔记
date: 2025-03-14 23:20:55
tags: 
    - hexo
---

# 功能

- 创建新的页面：hexo new page “路径”，e.g: hexo new page “/about”
- 创建新的笔记：hexo new “文件名”

# 使用命令

- hexo init
    
    `hexo init` 命令用于初始化本地文件夹为网站的根目录
    
    ```bash
    $ hexo init [folder]
    
    folder 可选参数，用以指定初始化目录的路径，若无指定则默认为当前目录
    ```
    
- hexo new
    
    `hexo new` 命令用于新建文章，一般可以简写为 `hexo n`
    
    ```bash
    $ hexo new [layout] <title>
    layout 可选参数，用以指定文章类型，若无指定则默认由配置文件中的 default_layout 选项决定
    title 必填参数，用以指定文章标题，如果参数值中含有空格，则需要使用双引号包围
    ```
    
- hexo server
    
    `hexo server`命令用于启动本地服务器，一般可以简写为 `hexo s`
    
    ```bash
    $ hexo server
    -p 选项，指定服务器端口，默认为 4000
    - i 选项，指定服务器 IP 地址，默认为 0.0.0.0
    - s 选项，静态模式 ，仅提供 public 文件夹中的文件并禁用文件监视
    ```
    
    **说明** ：运行服务器前需要安装 hexo-server 插件
    
    ```
    $ npm install hexo-server --save
    ```
    
    - 详细信息请参考：https://hexo.io/docs/server.html
- hexo generate
    
    `hexo generate` 命令用于生成静态文件，一般可以简写为 `hexo g`
    
    ```bash
    $ hexo generate
    -d 选项，指定生成后部署，与 hexo d -g 等价
    ```
    
    详细信息请参考：https://hexo.io/docs/generating
    
- hexo deploy
    
    `hexo deploy` 命令用于部署网站，一般可以简写为 `hexo d`
    
    ```bash
    $ hexo deploy
    -g 选项，指定生成后部署，与 hexo g -d 等价
    ```
    
    说明 ：部署前需要修改 _config.yml 配置文件，下面以 git 为例进行说明
    
    ```bash
    deploy:
    	type: git
    	repo: <repository url> #例如git@github.com:1van-w/1van-w.github.io.git
    	branch:	master
    	message: 自定义提交消息，默认为Site updated: {{ now('YYYY-MM-DD HH:mm:ss') }}
    
    ```
    
    详细信息请参考：https://hexo.io/docs/deployment.html
    
- **hexo clean**
    
    `hexo clean` 命令用于清理缓存文件，是一个比较常用的命令
    
    ```
    $ hexo clean
    ```
    
    **网站显示异常时可尝试此操作**
    
- Option
    1. hexo --safe
    
    `hexo --safe` 表示安全模式，用于禁用加载插件和脚本
    
    ```bash
    $ hexo --safe
    ```
    
    安装新插件时遇到问题可尝试此操作
    
    2. hexo --debug
    
    hexo --debug 表示调试模式，用于将消息详细记录到终端和 debug.log 文件
    
    ```bash
    $ hexo --debug
    ```
    
    3. hexo --silent
    
    hexo --silent 表示静默模式，用于静默输出到终端
    
    ```bash
    $ hexo --silent
    ```
    

# 异地同步

## 原电脑操作：

- 在原电脑上操作，给 username.github.io 博客仓库创建hexo分支，并设为默认分支。（可从github docs查看 [创建和修改分支](https://docs.github.com/zh/repositories/configuring-branches-and-merges-in-your-repository)）
- 随便一个目录下，命令行执行 `git clone git@github.com:username/username.github.io.git` 把仓库(hexo分支) clone 到本地。 显示所有隐藏文件和文件夹，进入刚才 clone 到本地的仓库，删掉除了 .git 文件夹以外的所有内容。
- 命令行 cd 到 clone 的仓库，`git add -A` ，`git commit -m "--"`，`git push origin hexo`，把刚才删除操作引起的本地仓库变化更新到远程，此时刷新下 github 端博客hexo分支，应该已经被清空了。
- 将上述 .git 文件夹复制到本机本地博客hexo根目录下（含有 themes、source 等文件夹），这样本机博客目录已经变成可以和 hexo 分支相连的仓库了。
- 将博客目录下 themes 文件夹下每个主题文件夹里面的 .git .gitignore 删掉。（无需删除博客根目录下的.gitignore）
- cd 到博客根目录，`git add -A` ，`git commit -m "--"`，`git push origin hexo`，将博客目录下所有文件更新到 hexo 分支。(如果上一步没有删掉 .git .gitignore，主题文件夹下内容将传不上去)。

**一个hexo分支用来存放网站的原始文件，一个master分支用来存放生成的静态网页。**

## 新电脑操作：

- 先把新电脑上环境安装好，node.js、git、hexo，ssh key 也创建和添加好。可以使用`node -v`，`git -v` ，`hexo -v` 查看相关配置是否安装成功。
- 选好博客安装的目录， `git clone git@github.com:username/username.github.io.git`。
- cd 到博客目录，(1)`npm install`、`hexo g`、`hexo s`，安装依赖，生成和启动博客服务。正常的话，浏览器打开 localhost:4000 可以看到博客了。(2)`npm install` 、`hexo clean` 、`hexo d -g`，完成依赖安装，重新生成、部署上线到GitHub Pages。

**原始文件的提交**

&emsp;&emsp;以后无论在哪台电脑上，更新以及提交博客，依次执行，`git pull`，`git add -A` ，`git commit -m "--"`，`git push origin hexo`，`hexo clean && hexo g && hexo d` 即可。

# 参考资料

- https://blog.csdn.net/wsmrzx/article/details/81478103
- https://hexo.io/docs/commands
- https://www.cnblogs.com/juzaizai/p/14472119.html
- https://blog.csdn.net/weixin_44008788/article/details/108325786