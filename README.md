---
title: GitHub+Hexo 搭建个人博客
date: 2019-01-15
tag: github
categorie: 技术
---
随着互联网时代的到来，国内外涌现出越来越多的社交网站让用户之间分享信息变得更加便捷，那么你是否也曾想过拥有一个属于自己的网站，写文章记录生活？如果你曾经或现在拥有这样的想法，就请跟随这篇文章，充分发挥你的动手能力，快速搭建属于你自己的个人博客网站，记录下生活中的美好。
<!-- more -->
## 搭建步骤
>1.GitHub创建个人仓库
>
>2.安装Git
>
>3.安装Node.js
>
>4.安装Hexo
>
>5.推送网站
>
>6.更换主题
>
>7.发布文章
## Hexo简介
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dk9icd7j30p008cweu.jpg)
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。
## Github简介
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dkn2lt2j30xc0hiaap.jpg)
GitHub 是一个面向开源及私有软件项目的托管平台，因为只支持 Git 作为唯一的版本库格式进行托管，故名 GitHub。GitHub 于 2008 年 4 月 10 日正式上线，除了 Git 代码仓库托管及基本的 Web 管理界面以外，还提供了订阅、讨论组、文本渲染、在线文件编辑器、协作图谱（报表）、代码片段分享（Gist）等功能。目前，其注册用户已经超过百万，托管版本数量也是非常之多，其中不乏知名开源项目 Ruby on Rails、jQuery 等。
## 搭建过程
### Github创建个人仓库
首先我们需要注册一个Github账号，注册成功后，使用刚才注册的账号密码进行登陆。
注册地址：[https://github.com/join?source=header-home](https://github.com/join?source=header-home)
点击GitHub中的New创建新仓库，仓库名应该为：[用户名.github.io](http://用户名.github.io)
这个用户名使用你的GitHub帐号名称代替，这是固定写法，比如我的仓库名为：[1sniper.github.io](http://1sniper.github.io)
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dlha95dj309l05yt8m.jpg)
### 安装Git
Git是开源的分布式版本控制系统，用于敏捷高效地处理项目。
Git下载地址:[https://git-scm.com/downloads](https://git-scm.com/downloads)
>**Windows 用户**
>由于众所周知的原因，从上面的链接下载git for windows最好挂上一个代理，否则下载速度十分缓慢。也可以参考[这个页面](https://github.com/waylau/git-for-win)，收录了存储于百度云的下载地址。

安装完成后，在命令行里输入git测试是否安装成功，若安装失败，参看其他详细的Git安装教程。
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dm8frj0j30lv06d0wl.jpg)
安装成功后，将你的Git与GitHub帐号绑定，在任意位置鼠标右击打开Git Bash，或者在菜单里搜索Git Bash，使用如下代码设置user.name和user.email配置信息：
```
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```
如下图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dmt8fhxj30ly05g0vl.jpg)
然后利用以下命令生成ssh密钥文件：
```
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```
如下图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dnqvcvej30u40jw14y.jpg)
然后找到生成的.ssh的文件夹中的id_rsa.pub密钥，将内容全部复制
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7docahdfj30v60gdmxi.jpg)
打开[GitHub_Settings_keys](https://github.com/settings/keys) 页面，新建new SSH Key
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dp7yh8tj30l204bdfq.jpg)
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dr3qi3sj30lb0craa2.jpg)
Title为标题，任意填即可，将刚刚复制的id_rsa.pub内容粘贴进去，最后点击Add SSH key。
添加完成后，页面如下：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dq27vhij30l607s74c.jpg)
另外，当我们添加ssh密钥成功后，会收到一封来自Github的邮件，或者我们可以在Git页面检测是否设置成功，命令如下：
```
ssh git@github.com
```
如图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dqn6rvvj30xe09kmyh.jpg)
如上则说明成功。这里之所以设置GitHub密钥原因是，通过非对称加密的公钥与私钥来完成加密，公钥放置在GitHub上，私钥放置在自己的电脑里。GitHub要求每次推送代码都是合法用户，所以每次推送都需要输入账号密码验证推送用户是否是合法用户，为了省去每次输入密码的步骤，采用了ssh，当你推送的时候，git就会匹配你的私钥跟GitHub上面的公钥是否是配对的，若是匹配就认为你是合法用户，则允许推送。这样可以保证每次的推送都是正确合法的。
### 安装Node.js
简单的说 Node.js 就是运行在服务端的 JavaScript。Node.js 是一个基于Chrome JavaScript 运行时建立的一个平台。Node.js是一个事件驱动I/O服务端JavaScript环境，基于Google的V8引擎，V8引擎执行Javascript的速度非常快，性能非常好。
Node.js下载地址：[https://nodejs.org/en/download/](https://nodejs.org/en/download/)
下载完成后进行安装，注意安装Node.js会包含环境变量及npm的安装，安装后，检测Node.js是否安装成功，在命令行中输入
```
node -v
```
检测npm是否安装成功，在命令行中输入
```
npm -v
```
如图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7drqvxrtj30hc05k41e.jpg)
### 安装Hexo
Hexo是我们的个人博客网站的框架， 需要自己在电脑常里创建一个文件夹，可以命名为Blog，Hexo框架与以后你自己发布的网页都在这个文件夹中。
创建好后，进入文件夹，按住shift键，鼠标右键点击"在此处打开Powershell窗口"，使用npm命令安装Hexo，输入：
```
npm install -g hexo-cli 
```
安装时间较长耐心等待
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dsckri0j30u204jq6k.jpg)
安装完成后，在刚才创建的文件夹内点击鼠标右键，选择"Git Bash Here"，初始化我们的博客，输入命令：
```
hexo init
```
如图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dt30evzj30xc0km4e5.jpg)
然后按顺序输入以下命令，在本地部署博客，用于检查网站雏形：
```
hexo g
hexo s
```
如图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dtsg39bj30tf03ota8.jpg)
完成后，打开浏览器输入地址：[localhost:4000](http://localhost:4000)
可以看到我们的网站雏形如下：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7du1ffsdj31hc0opqbq.jpg)
**附：Hexo常用命令简介**
```
npm install hexo -g #安装Hexo
npm update hexo -g #升级 
hexo init #初始化博客

hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署

hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略
```
### 推送网站
上面介绍的只是用于本地预览，接下来要做的是推送网站，也就是发布网站，让我们的网站可以被更多的人访问。在进行部署之前，需要解释一个概念，在blog根目录里的_config.yml文件称为站点配置文件，如下图：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dukn5fuj30v30g8jrz.jpg)
进入根目录里的themes文件夹，里面也有个_config.yml文件，这个称为主题配置文件，如下图：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dv26avrj30v20g83z4.jpg)
下一步将我们的Hexo与GitHub关联起来，打开站点的配置文件_config.yml，将最后的代码修改为：
```
deploy: 
type: git
repo: 这里填入你之前在GitHub上创建仓库的完整路径，记得加上 .git
branch: master
```
**注意：在冒号之后有一个空格（英文格式）**
参考如下：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dvjslqkj30ht03adfr.jpg)
保存站点配置文件。
其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。最后安装Git部署插件，在网站根目录文件夹下按住shift点击鼠标右键选择"在此处打开Powershell窗口"，输入命令：
```
npm install hexo-deployer-git --save
```
如下图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dwbcxrqj30xd07djxx.jpg)
然后我们在网站根目录文件夹下按住shift点击鼠标右键选择"Git Bash Here"，依次输入三条命令：
```
hexo clean 
hexo g 
hexo d
```
如图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dwvj9ykj30gw03mdh3.jpg)
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dxendw0j30q70kkk4p.jpg)
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dxszj2ij30so054q4a.jpg)
我们第一次部署的时候会要求输入Github的账号密码，按要求输入即可，如图所示：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dz5va9ej30b60bgdfr.jpg)
完成后，打开浏览器，在地址栏输入你的放置个人网站的仓库路径，即 [http://](http://xxxx.github.io/)[xxxx.github.io](http://xxxx.github.io/) 比如我的xxxx就是我的GitHub用户名，你就会发现你的博客已经上线了，可以在网络上进行访问了。
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dz62x7dj31hc0op0zo.jpg)
### 更换主题
如果你不喜欢Hexo的默认主题，可以在网络上下载其他主题进行更换
主题下载地址：[https://hexo.io/themes/](https://hexo.io/themes/)
将自己喜欢的主题下载之后进行解压，注意因为大多数主题在Github上下载，我们需要将文件名更改，例如hexo-theme-next-master，需要更改为next，然后放在网站根目录下的theme文件夹下，最后修改网站的配置文件中theme这一行为你的主题名称，例如:
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dz5vykhj30cz03c747.jpg)
然后我们在网站根目录文件夹下按住shift点击鼠标右键选择"Git Bash Here"，依次执行以下命令进行部署：
```
hexo g
hexo d
```
我们可以看到博客的主题已经更改了：
![image](http://ww1.sinaimg.cn/large/007z5ekzgy1fz7dz5x0cij31gv0okaag.jpg)
### 发布文章
我们可以用markdown语法编写完文章后，将md文件放置于网站根目录的\source\_posts下，然后重新进行部署，或者可以利用以下命令：
```
hexo new "博客名字"
```
直接在\source\_posts下生成md文件，然后进行编辑，重新部署。
这样一篇章新的文章就发表了。如图所示：
## 总结
怎么样，到这里是不是你的个人博客也搭建完成了呢？是不是成就感满满呢？
允许你偷偷激动一下...哈哈哈

