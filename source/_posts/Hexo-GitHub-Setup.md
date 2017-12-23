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
> * **系统** : 	Win10 64bits
> * **Git**		v2.11.1 [地址](http://pan.baidu.com/s/1kUK3hH1)
> * **Node.js** 	v6.11.3 [地址](http://pan.baidu.com/s/1slFNv1j)

#### ->Git
因为我是在windows的环境下，所以直接从如上地址取得软件包安装即可，一切按照默认设置即可，有一点注意的是中间在选择控制终端的时候，因为考虑到兼容性，我选择了默认的MingW，不过实际使用中发现这个自带终端有点偏慢，马虎接受吧。各位这里安装也可以试用windows自带的CMD
![git1](/images/Git1.JPG)

![git2](/images/Git.JPG)
#### ->Node.js
同上述基本一致，按照默认安装即可
![NJ](/images/NJ.JPG)
#### ->验证安装版本
如果以上软件安装一切顺利，则通过Git Bash(MingW)来查看各个软件安装的版本是否匹配，分别在界面内输入如下命令：
```bash
git --version
node -v
npm -v
```
输出结果如下，如果版本和下面图片输出的一致，则安装OK。
![bash_version](/images/bash_version.JPG)
前面的很简单，接下来才是核心。
### <font color=#A52A2A>2· GitHub仓库建立</font>
如前述，我们需要通过[GitHub](https://github.com/)来建立远程数据库，首要当然需要通过自己的邮箱和用户名注册一个GitHub账号，具体步骤不详述了，只要一步步的按照提示到‘Finish’。注册完成后就需要建立仓库了，进入自己的GitHub主页后，进入Repositories页面，接着点击右侧的‘New’，如下图所示，
![GitHub](/images/GitHub.jpg)
此时会有新建仓库页面跳出，输入仓库名，出现对号后，点击‘Create repository’，此时Git的分支随即创建出来，如图例所示的地址即https://github.com/xiaobinliGit/Hexo.git ，此地址就是我们博客的数据仓库，如后的操作全是通过Git基于这个仓库来的。
![GitHub](/images/GitHub_Repo.jpg)
仓库建立成功后会跳出初始化提示操作，因为我们这时还没任何代码commit，所以settings下的GitHub Pages还无法给出具体的https链接，只有后期我们有代码commit了，才会出现相应的网址，如下面第二个图就是此网站正在使用的链接
![GitHub](/images/GitHub_Repo1.jpg)
![GitHub](/images/GitHub_Repo2.jpg)
### <font color=#A52A2A>3· Hexo部署</font>
#### ->安装Hexo
来到最关键的一部，那就是部署Hexo框架，首先，新建一个空文件夹（必须是完全空的，否则会报错）。打开Git Bash, 进到相应的目录，或者如果在windows下，可以右击从跳出的菜单选择‘Git Bash’来安装hexo。接下来是要通过npm安装cnmp，这步主要是防止npm安装“被墙”，我们选择淘宝的cnpm镜像即可，接着再安装hexo并保存
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```
```bash
cnpm install -g hexo-cli
cnpm install hexo --save
```
安装完成后，输入如下命令，验证是否一切正确：
```bash
hexo -v
```
![hexov](/images/hexoV.jpg)
#### ->本地Hexo部署
安装Hexo成功后，即可通过hexo来本地部署博客预览效果，再次强调要在空文件夹下操作。
##### 初始化Hexo
```bash
hexo init
```
##### ->安装Hexo生成器
```bash
cnpm install
```
##### 一切就绪，查看hexo帮助命令，
```bash
hexo help
```
![hexoH](/images/hexoH.jpg)
##### ->本地静态生成并测试自己的博客
```bash
hexo s -g
```
![hexoD](/images/hexoD.jpg)
最后通过终端输出提示的地址进入浏览器预览自己的本地博客，下图显示的是我自己已经修改过内容的网站，如果是初始状态的话，应该是有“Hexo”字眼的首页。
![blogL](/images/BlogL.jpg)
##### ->通过GitHub部署自己的博客
来到这一步的话，证明我们Hexo的安装都成功了，接着就需要将我们自己的内容放到互联网并显示出来。这里最主要的是_config.yml文件，这个文件在文件夹的根目录和theme主题目录下都有，配置方式都相似，只是作用不同，我们部署博客的话先用到根目录下的，这个文件里包含了博客的各种配置，相应的解释可以参考字段前的解释，我把自己的配置文件粘贴如下，在最后的deploy配置中更改为自己的git分支即可通过hexo将自己本地的内容发布：
```

//title: Xiaobin's BLOG

subtitle: CS Life
description: This Blog is for my IT life record
author: Li Xiaobin
language: zh-CN
timezone: Asia/Shanghai

# If your site is put in a subdirectory, set url as  http://yoursite.com/child  and root as  /child/ 
# 这里这个root特别注意，如果你在github下建了独立的git分支，那就必须按照github上提示的子文件来设置，比如我的就是“CSBLOG”

url: https://xiaobinligit.github.io/
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# Directory
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:
#index_cover: images/timg.jpg

# Writing format
new_post_name: :title.md 
# File name of new posts
default_layout: post
# Transform title into titlecase
titlecase: false 
# Open external links in new tab
external_link: true 
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace:
  
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -date
  
# Category & Tag
default_category: uncategorized
category_map:
tag_map:

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
#theme: landscape
# 自己要用的主题
theme: aero-dual

# Deployment
## Docs: https://hexo.io/docs/deployment.html
## 自己定制，这里要设置成自己的git分支地址
deploy:
 type: git
 repository: https://github.com/xiaobinliGit/CSBLOG.git
 branch: master
```
* ##### config文件的配置要注意以下几点：
> 1.  每个关键字的冒号后必须要有一个空格；
> 2. 	Root目录设置一定要注意，这里需要设置成你在Git仓库分支创建后生成的https链接的子目录（比如我的是CSBLOG）；
> 3.  更改主题的话直接去hexo官网下载好相应的[主题](https://hexo.io/themes/)下载到你目录的'theme'文件夹下，然后更改_config文件即可；
> 4.  最后的deploy要替换成自己的git链接以及相应的分支名字；默认master即可；
> 5.  其他配置选项按照提示以此按自己需求定制，一般就是路径或者格式的问题。

##### ->新建博客
通过hexo help查到“hexo new 'blog-name'”是创建文章命令，生成的md文件会在(/blog/source/_posts/blog-name)下：
```
hexo new test
```
![blognew](/images/Blognew.jpg)
通过编辑器配置md文件，如下为例：
```
---
title: 重启博客
date: 2017-09-14 21:51:15
categories:
  - 技术日志
  - 关于博客
tags: ["Blog Restart"]
cover: /images/time.jpg  
---
### 摘要: 晓斌的博客
<!--more-->
正文:
新建博客，此博客主要用来记录我的日常工作内容
```

##### ->发布博客
一切都准备就绪，最后就是如何发布博客了，发布的原理就是本地通过hexo来生成静态的html文件，然后通过你本地配置的config文件中的git链接来自动push到相应的分支。首先需要配置自己的git登陆信息，
```
git config --global user.name "你的用户名"
git config --global user.email "你的邮箱"
```

接着安装hexo git插件：
```
npm install hexo-deployer-git --save
```
最后的最后，就是发布了：
老样子，参考help，输入：
```
hexo d -g
```
git会先deploy静态html网页，然后push到你之前设置的git分支上去，
![depoly](/images/deploy.jpg)
但是这步可能会提示permission denied，大部分原因是因为ssh认证问题，通过本地生成公钥并拷贝至git ssh设置下就可解决
```
ssh-keygen -t rsa 
```
一路回车，不需要任何输入，会在“你的home目录/.ssh”下生成id_rsa.pub文件，
![git2](/images/Git_SSH2.jpg)
把里面的内容全选，拷贝至自己的git ssh 设置下(new SSH key)，就可以实现本地到git的push
![git2](/images/Git_SSH.jpg)
![git1](/images/Git_SSH1.jpg)
至此，大功告成！enjoy your blog!

### <font color=#A52A2A>4· 参考文章</font>
1. http://blog.csdn.net/jzooo/article/details/46781805
2. https://xuanwo.org/2015/03/26/hexo-intor/
3. http://m.blog.csdn.net/csdn_lisword/article/details/73804982
4. http://www.cnblogs.com/tengj/p/5357879.html