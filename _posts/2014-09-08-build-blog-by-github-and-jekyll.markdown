---
title: Jekyll博客流程
layout: post
guid: 2ef3550f-8cf3-400b-a55b-c512c9af8b2d
tags:
  - Tech
---

<!--
[![bridge to wonderland]({{ site.baseurl }}/media/files/2014/09/05/bridge-to-wonderland.jpg)](http://500px.com/photo/82158657)

[Lucian](http://lucianmarin.com/ "Lucian")
-->

来，我们先看两个博客，[rusty shutter](http://lhzhang.com/ "rusty shutter")，[Lucian](http://lucianmarin.com/ "Lucian")，这种4、5年前就建立好，放到现在看却依旧一点都不过时的简约风格博客是否符合你的胃口？如果答案是“是”的话，往下看吧，下面是我博客之魂熊熊燃烧了三天的成果。

###1. 基础知识

现在的个人博客市场使用人数最多的是WordPress，使用wp的好处在于：

1. 使用人数多，这意味着很容易找到人帮你
2. 模板多，不管免费还是付费的到处都是
3. 支持动态网页，评论什么的很好弄

但是我不喜欢现在wp千篇一律的酷炫风格，而且我在wp中没有找到一个很好的列表功能，完整得展示我所有的文章，现在回头去看看上面那两个博客中的Archive，你就知道我想要什么了。

我想要的这种博客是基于Jekyll和Markdown技术做的，只支持静态网页，缺点挺多，但是对于一个只追求简约博客的人来说，绰绰有余。

###2. 技术路线

用Jekyll从空白开始做一个博客大概需要这些知识：

* Jekyll
* HTML
* css
* Git
* Javascript

至于其他还需要什么知识，我暂时没接触到，可能会更多。反省自己一下，不行吧？所以为什么我不在遵守开源协议的情况下直接使用别人的代码呢？

以下是这个思路的技术路线：

1. 找一个喜欢的Jekyll博客，找到他的Github项目，fork
2. 在自己的Github账号下新建一个repository，名字是username.github.com
3. 把喜欢博客clone到自己的本地git仓库，修改好，push到远程刚建立的repository
4. 安装Jekyll开发环境
5. 本地编译
6. 上传主机
7. 绑定域名
8. 完成


###3. 实际操作

1. 以[rusty shutter](http://lhzhang.com rusty "shutter")为例讲解。在任意页面最下面右侧，点击fork me，跳转该作者Github页面，选择名为```blog```的repository，点击fork，此时注意页面地址，已经跳转为你自己的repository页面，我的就是```www.github.com/keaising/blog```
2. 在自己的Github账号下新建一个repository，名字是username.github.com，username是你的账户名字，我的就是```keaising.github.com```
3. 这里分为很多步：
 * 首先在本机安装Git，打开Git Bash，定位到想要存放网页文件的目录下（这里你需要一点点控制台知识，百度一下，很简单）。
 * 输入```git clone https://www.github.com/keaising/blog.git blog```，这段代码的意思是，在当前目录新建一个名为```blog```的文件夹，将位于```https://www.github.com/keaising/blog```中的代码克隆到```blog```文件夹下。
 * 删除```blog```文件夹下的```.git```文件夹，这是隐藏文件。
 * 新建一个```keaising.github.com```文件夹，该文件夹要与```blog```在同一目录下，至少不能是包含关系。
 * 将```blog```文件夹中所有文件复制到```keaising.github.com```文件夹中。
 * 在Git Bash中导航至```keaising.github.com```文件夹下，输入以下代码：
 + ```git init``` 初始化本地代码仓库
 + ```git add .``` 将所有文件添加到当前工作区
 + ```git commit -m "init" ``` 提交当前工作区
 + ```git remote add origin https://www.github.com/keaising/keaising.github.com.git``` 将本地仓库添加到远程repo中
 + ```git push origin master``` 把所有文件推送到远程repo
 + 在浏览器中打开```keaising.github.com```页面，enjoy:)
 + 需要注意的是，上面所有的```keaising```都是我的Github账户名，你需要换成你的，这中途需要注意Git Bash的报错信息，根据报错信息自行谷歌吧，没有遇到过报错的码农注定不能成功。
 + 其实到这一步，用Github和Jekyll建立网站的过程已经结束了，以下是本地编译网页文件和从Github迁移到其他主机的过程

4. 安装开发环境教程很多，特别是在Linux和OS X下，那根本不是个事，现在讲Windows下的安装，安装过程主要参照该文：[在 Windows 上安装 Jekyll](http://cn.yizeng.me/2013/05/10/setup-jekyll-on-windows/ "在 Windows 上安装 Jekyll") 或者 [Run Jekyll on Windows](http://jekyll-windows.juthilo.com/) 由于墙的原因，很有可能遇到麻烦，比如不能通过控制台下载所需文件，这时候就需要换源了，换源方法：[RubyGems 镜像](http://ruby.taobao.org/ "RubyGems 镜像") 不得不感叹一句：壮哉我大淘宝！如果一切顺利，你的Jekyll开发环境就搞定了。

5. 本地编译
 * 打开cmd，导航至```keaising.github.com```页面下，输入：
 * ```jekyll bulid``` 将所有文件编译成网页，网页内容在```_site```文件夹中。
 * ```jekyll serve``` 启动本地服务器，你可以用浏览器打开```localhost:4000```看看，这是方便不断调试用的。
 * 这样就完成了本地调试，所有的网页文件都已经存放在```_site```中了。

6. 上传主机和域名配置
将```_site```文件夹中所有内容上传到你主机中，将域名的dns指向主机，就完成了所有工作。

7. 写文章。写文章一般使用Markdown，标记语言很简单的。写好之后放到```_post```中，重复5中的本地编译，将```_site```文件夹下变化了的文件上传主机，完成文章更新。
8. 这里我其实回避了很多问题，比如Git的知识、Github的使用、全部网页的文件结构等，这些都是其他教程反复讲了很多的，我觉得不需要我讲，多看看其他教程吧。

###4. 小结
总的来说，这工作量相当大，特别是对于一个完全没接触过的人来说，学习曲线过于陡峭，建议有时间的时候慢慢折腾，实在不行，还是回去用WordPress吧，那个省心很多。