---
title: 通过Hexo+GitHub创建自己的博客
date: 2017-09-17 20:03:42
categories:
  - 生活日志
  - 博客建立
tags:
  -Blog Setup
---
### 摘要: 用Hexo和GitHub建立自己的独立博客
<!--more-->
## <font color=#0000FF>缘由</font>
从本科开始用百度空间记录自己的一些日常，因为自己注册为数不多的一个网站就包含百度，因而顺理成章的通过百度空间来充当自己的博客，而且编辑和主题等功能使用起来还算便捷。随后读硕士的时候，有个课题是WCDMA+NS2网络仿真，那时还通过自己的博客和别人交流了一番，再后来工作就很少touch这块东西了，因为各种笔记和自己的公司在一直支持使用的onenote，随时记录也算方便，但最近突然在学习C++和Cloud的时候翻阅了很多在线资料，发现还是有些博客靠谱，而本地的记录在这时就显得很力不从心了。结果当自己打算重新在百度上翻找自己当年的博客时，居然全部没了，百度空间中的博客功能取消了，于是决心去搭建一个自己的博客，也正好通过这个平台来记录自己工作生活的点滴，做技术，或者更深入的说，做人，还是要积累。
在“知乎”一番之后，决定用当下流行的“Hexo+GitHub”,方便快捷，而且通过git多终端同步，最重要的，数据不会丢失，作为一个“攻城狮”，解决这种基本问题是必须的。
## <font color=#0000FF>简介</font>
### <font color=#A52A2A>·Hexo</font>
Hexo 是一个快速、简洁且高效，基于Node.js的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页（引用自：[Hexo 文档](https://hexo.io/zh-cn/docs/)）。静态的优点就是支持它的环境十分好找，比如GitHub。但相比动态博客，静态博客要频繁改动文件。
### <font color=#A52A2A>·GitHub</font>
GitHub是一个面向开源及私有软件项目的托管平台，因为只支持git 作为唯一的版本库格式进行托管，故名gitHub。GitHub提供了订阅、讨论组、文本渲染、在线文件编辑器、协作图谱（报表）、代码片段分享（Gist）等功能。对于我的博客来说，GitHub就是一个数据仓储中心和网络访问接口
## <font color=#0000FF>步骤</font>
总体来讲可以概括为：软件安装->GitHub仓储建立->Hexo部署
### <font color=#A52A2A>1· 软件安装</font>
#### 准备
* **系统** : 	Win10 64bits
* **Git**		v2.11.1 [地址](http://pan.baidu.com/s/1kUK3hH1)
* **Node.js** 	v6.11.3 [地址](http://pan.baidu.com/s/1slFNv1j)

#### Git
因为我是在windows的环境下，所以直接从如上地址取得软件包安装即可，一切按照默认设置即可，有一点注意的是中间在选择控制终端的时候，因为考虑到兼容性，我选择了默认的MingW，不过实际使用中发现这个自带终端有点偏慢，马虎接受吧。各位这里安装也可以试用windows自带的CMD
![git1](/CSBLOG/images/Git1.JPG)

![git2](/CSBLOG/images/Git.JPG)
#### Node.js
同上述基本一致，按照默认安装即可
![NJ](/CSBLOG/images/NJ.JPG)
#### 验证安装版本
如果以上软件安装一切顺利，则通过Git Bash(MingW)来查看各个软件安装的版本是否匹配，分别在界面内输入如下命令：
```bash
git --version
node -v
npm -v
```
输出结果如下，如果版本和下面图片输出的一致，则安装OK。
![bash_version](/CSBLOG/images/bash_version.JPG)
前面的很简单，接下来才是核心。
### <font color=#A52A2A>2· GitHub仓库建立</font>
如前述，我们需要通过[GitHub](https://github.com/)来建立远程数据库，首要当然需要通过自己的邮箱和用户名注册一个GitHub账号，具体步骤不详述了，只要一步步的按照提示到‘Finish’。注册完成后就需要建立仓库了，进入自己的GitHub主页后，进入Repositories页面，接着点击右侧的‘New’，如下图所示，
![GitHub](/CSBLOG/images/GitHub.jpg)
此时会有新建仓库页面跳出，输入仓库名，出现对号后，点击‘Create repository’，此时Git的分支随即创建出来，如图例所示的地址即https://github.com/xiaobinliGit/Hexo.git ，此地址就是我们博客的数据仓库，如后的操作全是通过Git基于这个仓库来的。
![GitHub](/CSBLOG/images/GitHub_Repo.jpg)
仓库建立成功后会跳出初始化提示操作，因为我们这时还没任何代码commit，所以settings下的GitHub Pages还无法给出具体的https链接，只有后期我们有代码commit了，才会出现相应的网址，如下面第二个图就是此网站正在使用的链接
![GitHub](/CSBLOG/images/GitHub_Repo1.jpg)
![GitHub](/CSBLOG/images/GitHub_Repo2.jpg)