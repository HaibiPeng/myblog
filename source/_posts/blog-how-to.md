---
title: Hexo+GitHubPages+腾讯云搭建个人博客
date: 2022-01-17 16:19:37
tags: Hexo, 个人博客
categories: Hexo, 个人博客
---

本教程需要读者具有基础的编辑器(VSCode/WebStorm/其他...)和命令行知识，以及文档教程阅读和复现能力。以下大致说明以下步骤吧。

## Hexo

### 安装依赖项和Hexo

按照官方文档安装所需程序（Node.js/Git）。

安装指南传送门：
1. [Node.js](https://www.runoob.com/nodejs/nodejs-install-setup.html)
2. [Git](https://www.runoob.com/git/git-install-setup.html)
3. [Hexo](https://hexo.io/zh-cn/docs/#%E5%AE%89%E8%A3%85-Hexo)

### 使用Hexo建站并修改配置

详见官方文档：

1. [建站](https://hexo.io/zh-cn/docs/setup)
2. [修改配置](https://hexo.io/zh-cn/docs/configuration)

### 启动网站

在命令行运行以下命令：

``` bash
$ hexo server
```

然后再浏览器输入 http://localhost:4000/ 就可以打开网站看到原始版的个人博客网站了。

## GitHub Pages

这一部分需要你有一个github的账号，以及新建一个repo，并且将上一步Hexo中的代码关联到这个repo。

### 创建GitHub Pages站点

指南传送门：[创建GitHub Pages站点](https://docs.github.com/cn/pages/getting-started-with-github-pages/creating-a-github-pages-site)

### 修改博客url

在_config.yml文件中修改url为你的repo的Github Pages的网址：

``` yml
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/repo'
url: https://username.github.io/repo
```

### 部署到GitHub Pages

1. 安装 hexo-deployer-git。

``` bash
$ npm install hexo-deployer-git --save
```

2. 修改配置：
``` yml
deploy:
  type: git
  repo: <repository url> #repo的地址，如https://github.com/username/repo
  branch: [branch] #需要部署的代码分支，如main、master，需要去掉[]
  message: [message] #部署信息，可以随便填，需要去掉[]
```

3. 生成站点文件并推送至远程库

``` bash
$ hexo clean && hexo deploy
```

4. 在库设置（Repository Settings）中将默认分支设置为_config.yml配置中的分支名称就可以了。

这样你就可以用GitHub Pages的url打开你的个人博客了。

更详细的指南请移步官方文档: [一键部署到GitHub](https://hexo.io/zh-cn/docs/one-command-deployment)

## 腾讯云

### 域名申请

购买申请指南请移步：[腾讯云购买域名](https://dnspod.cloud.tencent.com/)

其中需要一堆实名认证过程，请按照官方文档操作。

### 绑定到Github Pages

详见这篇博客: [GitHub Pages搭建的博客绑定域名](https://cloud.tencent.com/developer/article/1421879)

添加DNS解析部分详见这篇，需要用命令行ping一下自己的github page获取ip地址：[github pages绑定域名](https://cloud.tencent.com/developer/article/1454059)

### 修改先前的配置

在第二步中将博客url设置成了自己的GitHub Pages的url，而既然我们已经有了自己的域名，就需要把之前的url换成我们自己的域名：

``` yml
# URL
## 你自己申请的域名
url: https://username.cn
```

大功告成。

## Hexo主题

如果你觉得默认主题不太好看，是可以自己设计或者更换主题的。

官方文档：[主题](https://hexo.io/zh-cn/docs/themes)

官方还有一个[主题库](https://hexo.io/themes/)，可以搜索自己觉得好看的主题，然后去主题的GitHub repo下载并移到自己博客的theme文件夹下，修改对应配置为这个主题的名字。

比如我用的主题为[ocean](https://github.com/zhwangart/hexo-theme-ocean.git themes/ocean)，就在root _config.yml 中选择 theme: ocean：

``` yml
theme: ocean
```

其他个性化配置就需要参考每个主题的相关文档了，一般是主题的设计开发者写的，没有的话就需要自己摸索了。主题里的各种图标，图片，视频等等都是可以自己换的，可能需要使用者有一些css、html和markdown的基础，这里就不深入下去了，有兴趣的话各位自己学习吧哈哈哈。
