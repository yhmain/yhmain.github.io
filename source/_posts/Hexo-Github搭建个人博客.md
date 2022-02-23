---
title: Hexo+Github搭建个人博客
date: 2022-02-09 22:10:43
categories: 博客搭建
tags: Hexo
---
<center style="font-size:larger;font-weight:bold">GitHub+Hexo 搭建个人网站详细教程（一）------初识Hexo</center>

# 前言
&emsp; 利用Hexo快速搭建一个网站，并且将其部署在github上面，使得可以通过域名访问你自己的个人网站，实现成为一个站长的梦想！就这样快速拥有自己的博客网站，写文章记录生活，享受这种从0到1的过程!
<!-- more -->
# 搭建步骤
## Github创建个人仓库
&emsp; 如果无Github账号，使用你的邮箱在[Github官网](https://github.com/)注册帐号，不会的同学请自行百度“Github如何注册账号”。
&emsp; 注册完成或者已有账号做如下操作：
1. 点击GitHub中的New repository创建新仓库
![Github_new](https://tva4.sinaimg.cn/large/006LDSTgly1gz9w2lq6lyj31hc0o2ara.jpg)
这里我报红是因为我已经创建了一个同名仓库。记住仓库名为：**用户名**.github.io，仔细看图中的红框，用户名一定要和你Github账户的用户名相同！
![Github_resp_name](https://tvax3.sinaimg.cn/large/006LDSTgly1gz9w7mlm2dj30wn0ka46l.jpg)
2. 点击Create repository即可
## 安装Git
&emsp; 什么是Git ?简单来说Git是开源的分布式版本控制系统，用于敏捷高效地处理项目。我们网站在本地搭建好了，需要使用Git同步到GitHub上。提供如下资料：
+ [Git教程](https://link.zhihu.com/?target=http%3A//www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)
+ [Git下载](https://link.zhihu.com/?target=https%3A//git-scm.com/download/win)，现在的电脑基本都是64位的，选择64位的安装包，下载后安装，在命令行里输入git测试是否安装成功。若安装失败，参看其他详细的Git安装教程。
1. 安装成功后，将你的Git与GitHub帐号绑定，鼠标右击打开Git Bash
![Git_Bash](https://tvax4.sinaimg.cn/large/006LDSTgly1gz9wiffji1j306z0a4glv.jpg)
2. 设置user.name和user.email配置信息：
```bash
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```
3. 生成ssh密钥文件：
```bash
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```
4. 接下来直接三个回车即可，默认不需要设置密码，然后找到生成的.ssh的文件夹中的id_rsa.pub密钥，将内容全部复制。可能在页面上看不到.ssh，那么你可以直接在上方地址栏输入路径，再回车进入（我查看打开隐藏项目，似乎也没有看到，所以这样做的）
![ssh](https://tvax1.sinaimg.cn/large/006LDSTgly1gz9wusjq2aj30sj09kjv2.jpg)
5. 打开[GitHub_Settings_keys](https://link.zhihu.com/?target=https%3A//github.com/settings/keys) 页面，新建new SSH Key。Title为标题，任意填即可，将刚刚复制的id_rsa.pub内容粘贴进去，最后点击Add SSH key
![new_ssh_key](https://tva4.sinaimg.cn/large/006LDSTgly1gz9wxtqa7ej30k70aijrj.jpg)
6.在Git Bash中检测GitHub公钥设置是否成功，输入 `ssh git@github.com `：
![ssh_check](https://tva4.sinaimg.cn/large/006LDSTgly1gz9x2kbn0ej30pa087n0s.jpg)
如上则说明成功。这里之所以设置GitHub密钥原因是，通过非对称加密的公钥与私钥来完成加密，公钥放置在GitHub上，私钥放置在自己的电脑里。GitHub要求每次推送代码都是合法用户，所以每次推送都需要输入账号密码验证推送用户是否是合法用户，为了省去每次输入密码的步骤，采用了ssh，当你推送的时候，git就会匹配你的私钥跟GitHub上面的公钥是否是配对的，若是匹配就认为你是合法用户，则允许推送。这样可以保证每次的推送都是正确合法的。
## 安装Node.js
&emsp; Hexo基于Node.js，Node.js下载地址：[Node.js 下载安装包](https://nodejs.org/en/download/)，注意安装Node.js会包含环境变量及npm的安装，安装后，检测Node.js是否安装成功，在命令行中输入 node -v :
![1644588153(1)](https://tva3.sinaimg.cn/large/006LDSTgly1gz9x6x4a6aj30m8066ach.jpg)
检测npm是否安装成功，在命令行中输入npm -v :
![1644588204(1)](https://tva3.sinaimg.cn/large/006LDSTgly1gz9x7rirkkj30m708fgor.jpg)
到这了，安装Hexo的环境已经全部搭建完成。
## 安装Hexo
Hexo就是我们的个人博客网站的框架， 这里需要自己在电脑常里创建一个文件夹，可以命名为Blog，Hexo框架与以后你自己发布的网页都在这个文件夹中。为了后面方便描述，假设我是建在D盘，则现在路径如下：`D:\Blog`
创建好后，进入文件夹中，如下所示：
![1644588492(1)](https://tvax2.sinaimg.cn/large/006LDSTgly1gz9xcw356bj30n5070acu.jpg)
进入路径`D:\Blog`后，再使用npm命令安装Hexo，输入：
`npm install -g hexo-cli`
这个安装时间可能会很长？安装完成后，初始化我们的博客，输入：
`hexo init blog`  该命令会在Blog文件夹下创建一个名称为blog的文件夹
说明：这里的命令都是作用在刚刚创建的Blog文件夹中。
**接下来进入blog文件夹！！！**：
`cd blog`
为了检测我们的网站雏形，分别**按顺序输入以下三条命令**：
`hexo new test_my_site`
`hexo g`
`hexo s`
这些命令在后面作介绍，完成后，打开浏览器输入地址：
[localhost:4000](localhost:4000)
可以看出我们写出第一篇博客，只不过我下图是**我修改过的配置**，和大家的显示不一样。
![test_site](https://tva1.sinaimg.cn/large/006LDSTgly1gz9xmc4n64j31hc0o2gy1.jpg)
## 常用的Hexo 命令及含义
```bash
npm install hexo -g #安装Hexo
npm update hexo -g #升级
hexo init #初始化博客
```
```bash
命令简写
hexo n "我的博客" == hexo new "我的博客" #新建文章
hexo g == hexo generate #生成
hexo s == hexo server #启动服务预览
hexo d == hexo deploy #部署
```
```bash
hexo server #Hexo会监视文件变动并自动更新，无须重启服务器
hexo server -s #静态模式
hexo server -p 5000 #更改端口
hexo server -i 192.168.1.1 #自定义 IP
hexo clean #清除缓存，若是网页正常情况下可以忽略这条命令
```
## 推送网站
上面只是在本地预览，接下来要做的就是就是推送网站，也就是发布网站，让我们的网站可以**在互联网上访问**。在设置之前，需要解释一个概念，在blog根目录里的_config.yml文件称为**站点配置文件**，如下图：
![1644589346(1)](https://tva3.sinaimg.cn/large/006LDSTgly1gz9xrnnhn5j30sh0fraho.jpg)
进入根目录里的themes文件夹，里面也有个_config.yml文件，这个称为主题配置文件，如下图：
![1644589425(1)](https://tva3.sinaimg.cn/large/006LDSTgly1gz9xsxlynij30s60ivgu6.jpg)
记住：这2个文件在我们之后对网站的样式修改的过程中起到非常重要的作用！！！
---
下一步将我们的Hexo与GitHub关联起来，打开站点的配置文件_config.yml，翻到最后修改为：
**<font color=red>注意点：1. 间隔的空格 2. 地址后面加上.git</font>**
```bash
deploy:
  type: git
  repo: https://github.com/yhmain/yhmain.github.io.git
  branch: master
```
![1644589645(1)](https://tvax3.sinaimg.cn/large/006LDSTgly1gz9xwx2uzaj30q60gh457.jpg)
其实就是给hexo d 这个命令做相应的配置，让hexo知道你要把blog部署在哪个位置，很显然，我们部署在我们GitHub的仓库里。最后安装Git部署插件，输入命令：
`npm install hexo-deployer-git --save`
这时，再分别输入三条命令：
`hexo clean `
`hexo g `
`hexo d`
其实第三条的 hexo d 就是部署网站命令，d是deploy的缩写。完成后，打开浏览器，在地址栏输入你的放置个人网站的仓库路径，即 xxxx.github.io，比如我的xxxx就是我的GitHub用户名：yhmain.github.io
你就会发现你的博客已经上线了，可以在网络上被访问了!:tw-1f31e:
补充：
- 如果想使用自己的域名，可以参考这篇文章：[Github+Hexo搭建个人网站](https://zhuanlan.zhihu.com/p/26625249)
## 更换主题
如果你不喜欢Hexo默认的主题，可以更换不同的主题，主题传送门：[Themes](https://hexo.io/themes/) 我自己使用的是Next主题（**推荐**，后续咱也有主题对应的教程），可以在blog目录中的themes文件夹中查看你自己主题是什么。现在把默认主题更改成Next主题，首先我们需要把主题下载下来（2种方法）：
1. 在线下载。在blog目录中（就是命令行的位置处于blog目录）打开命令行输入：
`git clone https://github.com/theme-next/hexo-theme-next`
记住地址可能会变，但是你看这个人的仓库就知道或许移到哪了。
2. 离线下载。 选择Download Zip。下载后放到themes文件夹下，解压后命名为next
![1644590953(1)](https://tva2.sinaimg.cn/large/006LDSTgly1gz9yjfze1sj31hc0o217y.jpg)
说明：如果Github下载慢，对于在线下载，有VPN条件的同学试试 让终端走代理 export xxx；对于离线下载，可以先将这个仓库拉到自己的[码云](https://gitee.com/)仓库，不会的就可以去自行百度了，毕竟方法都教给你了，路总是要亲自走的~:tw-2611:
之后，打开**站点**的_config.yml配置文件，修改主题为next：
![1644591425(1)](https://tvax2.sinaimg.cn/large/006LDSTgly1gz9yrko790j30pu0gcn3r.jpg)
接下来，打开**主题**的_config.yml配置文件，找到Scheme Settings
![1644591557(1)](https://tvax1.sinaimg.cn/large/006LDSTgly1gz9yu18l2nj30q70g8435.jpg)
next主题有三个样式，我用的是Pisces，你们可以自己试试看，选择你自己喜欢的样式（只需要把行首的#去除，#是注释），选择好后，再次部署网站，hexo g、hexo d，查看效果。选择其他主题，按照上述过程即可实现。
注意：每次部署后，需要等几分钟才会刷新页面，毕竟是在Github上面嘛。所以想要即时看到效果的话建议是hexo s，在本地输入[localhost:4000](http:/localhost:4000/)查看。


