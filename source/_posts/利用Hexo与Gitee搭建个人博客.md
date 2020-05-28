---
title: 利用Hexo与Gitee搭建个人博客
date: 2020-05-27 17:57:57
tags: Hexo
categories: 博客搭建
---

# 写在前面：随着研究生复试的顺利结束与毕业设计的完成，自己准备学习一些研究生期间需要用到的知识，于是萌生了搭建个人博客的想法，以此来进行知识的总结整理。这个博客的搭建过程是参考了B站UP主[codesheep](https://www.codesheep.cn/)的[视频教程](https://www.bilibili.com/video/BV1Yb411a7ty/?spm_id_from=333.788.videocard.10)以及网上一些朋友的经验完成的。初期博客比较~~简约~~丑陋，后期应该会进行一些优化。  
<!-- more -->

# 环境  
- Windows系统  
- Git
- Node.js

# 安装Git
其实这个之前因为使用github的原因已经安装过了，这里再记录一下安装过程。  
- 首先到Git的官网找到自己电脑对应的版本进行下载，官网下载地址：[https://git-scm.com/download](https://git-scm.com/download)。
- 安装时配置选择默认就好，一路next即可。
- 输入`git version`查看是否安装成功  
  ![测试](查看版本.png)
`git config --user.email "youremail"`  
`git config --user.name "yourname"`  
# 安装Node.js
这个语言我没有学过，不过用Hexo博客必须安装Node.js,并用到其中的npm包管理器安装插件。  
- Node.js官网下载地址:[https://nodejs.org/en/download/](https://nodejs.org/en/download/),选择LTS中自己电脑对应的包下载即可。
- 依旧是一路next。
- 完成安装后在GitBash中输入`node -v`和`npm -v`查看node和npm的版本。
  
# 安装Hexo
直接用npm安装Hexo速度会很慢，先利用npm安装cnpm工具(国内淘宝npm镜像源)。  
- 安装cnpm  
  `npm install -g cnpm --registry=https://registry.npm.taobao.org`  
- 使用cnpm安装Hexo  
  `cnpm install -g hexo-cli`
- 验证是否安装成功  
   `hexo -v`  
   若出现下图信息则安装成功。   
   ![测试](1.png)
   
# 博客搭建  
安装完前面的工具就可以正式进行博客的搭建了。  
首先在自己电脑上建立一个文件夹，用来存放自己的博客项目。我自己建立了一个myBlogs文件夹，用来存放各种博客项目，对于此次的Hexo，在其中建立一个blog文件夹。  
- 在自己建立的文件夹上右键选择`Git Bash Here`。
- 输入`hexo init`完成初始化，之后需要等待一段时间。
- 初始化完成后会在文件夹中发现多出了一些文件夹和文件。  
  * node_modules: 依赖包  
  * public: 存放生成的页面
  * scaffolds: 生成文章的模板
  * source: 自己之后写文章时都会在该目录下进行
  * theme：存放博客主题
  * _config.yml: 博客配置文件
- 在本地打开Hexo服务 
  ![图片](2.png)
  此时我们可以通过在浏览器中输入localhost:4000来访问自己的博客界面了。界面我就不贴了。  
  这个命令还是很有用的，当我们对博客主题或者内容更新后，可以先在本地查看一下效果再部署到外部。
- 用`hexo n "博客名称"`完成文件的创建，其中博客名称是不带.md的。**注意，运行该命令时应确保自己当前目录为你最初创建的博客项目文件夹下**,例如，我的应该在/e/myBlogs/blog。  
  Hexo博客文件是基于markdown文法编辑的，对于markdown语法不了解的可以点击[这里](https://www.runoob.com/markdown/md-tutorial.html)进行简单的学习。
- 文档编写完成后重新启动Hexo  

  `hexo clean         #清除一下缓存`  
  `hexo generate      #生成静态网页 可简写为hexo g`  
  `hexo sever         #启动本地服务 可简写为hexo s`  

# 部署博客到Gitee
为了能够让其他人访问到我们的博客，需要将其部署到远端去。部署的方式有很多种，比如可以选择买个域名和虚拟主机。这里选择了免费的方式，将其部署到Gitee上，其实也可以部署到Github上去，不过速度可能会慢一些。  
如果还没有注册Gitee的话需要先完成注册，很简单。  
- 登录我们的Gitee账户。
- 新建一个仓库,**这里要注意仓库名称需要与自己账户名称一致**,这点与Github中是不一样的，假如你要使用Github的话，新建的仓库名应该为`youraccount.github.io`
  ![图片](3.png)
- 打开Hexo中的配置文件`_config.yml`,找到并修改一下内容：  
  ```  
  deploy:
    type: git
    repo: https://gitee.com//mmmcn/mmmcn.git  #你自己仓库的url
    branch: master  
  ```
- 安装git插件
  ```
  cnpm install hexo-deployer-git --save   #没有此插件无法将项目推到远程仓库

  hexo d     #将博客项目推到远程仓库

  # 上传时需要输入账户名称和密码，好像配置了SSH之后不需要每次都输了。
  # 但是我推到Github不用每次都输账号密码，推到Gitee仍然每次都要输入，
  # 我的Gitee中已经配置了SSH密钥了，这里还有些问题。
  ```
- 成功上传到Gitee仓库后还需要打开Gitee Page服务,**需要注意的是每次博客更新之后都需要进行Gitee Page的更新**
  ![图片](4.png)
- 最后就可以在浏览器输入Gitee Page中显示的网站地址来访问自己的博客啦！  

# 一些问题
1. 新建仓库时如果仓库名称不是你自己的账户名称会导致博客网站地址过长，也不美观。
2. 仍然是仓库名称导致的问题，假如你的仓库名称叫做test，可能你会发现在查看自己博客时只有内容，而那些CSS样式都没有了。可以用如下方式解决：  
   - 进入到自己的hexo配置文件config.yml中，找到以下部分：   
    ![图片](5.png)
   - 将url后边改为`http://yoursite.com/test`，root后边改为`/test/`  
    之后你就会发现又可以愉快的玩耍了~