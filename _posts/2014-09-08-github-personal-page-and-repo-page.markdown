---
title: Github Pages中个人页面和项目页面的坑
layout: post
guid: 2ef3550f-8cf3-400b-a55b-c512c9af8b2d
tags:
  - Tech
---

<!--
[![bridge to wonderland]({{ site.baseurl }}/media/files/2014/09/05/bridge-to-wonderland.jpg)](http://500px.com/photo/82158657)

[Lucian](http://lucianmarin.com/ "Lucian")
-->

在使用Github和Jekyll建立静态博客的过程中，必须要注意的一点是Github Pages分为两种，个人页面和项目页面:

###个人页面
每个账号只能建立一个个人页面，个人页面的目的是展示这个账号的各种信息，个人页面的链接为https://username.github.io，在建立个人页面的repository时repo-name一定要是username.github.com，而且推送分支是master

###项目页面
每个账号可以建立多个项目页面，项目页面的目的是展示页面对应的repository，项目页面的链接为https://username.github.com/repo-name，在建立个人页面时，repo-name随便写，但是用git推送分支时，必须要是gh-pages，切记。

从这里就可以看出，二者的区别主要在链接不同，由于二者的使用目的不同，使用环境也肯定是不同的，作为个人博客，我更推荐使用“个人页面”来建立我们的博客，理由如下：

1. 说实话作为一般爱好者（比如我），博客所有代码全部自己手写的可能性几乎为零，要去搞懂所有的Jekyll、HTML、css和其他网页设计和制作知识的可能性也几乎为零，我不是为了做一个前端码农来弄这个博客的，我只是想要一个博客，仅此而已，那么去fork其他人现成的博客项目，在遵守各种开源条件的情况下，使用现成的博客模板是最节省时间的。而大多数人的博客项目，都是基于个人页面的链接来制作的，因为这样可以更容易让博客迁移出Github，如果基于项目页面，网页代码中，所有相对路径前面都需要加上{{ site.baseurl }}这样一段字符，代码不是自己写的，而且新手入门，这个地方不知道坑了多少人。

2. 这事都怪阮一峰。在阮一峰关于用Github和Jekyll的博文[搭建一个免费的，无限流量的Blog](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html "搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门")中，阮一峰使用的是项目页面，像我这种新手都循规蹈矩照做了，结果评论中各种求问css不生效和页面链接404的小白，更重要的是，没有人在评论中给出解决方法，也是醉了。其实这个问题就是用我在1中提到的方法就可以解决。为什么我会在这里提到这篇博文呢，因为你去谷歌一下Jekyll和Github建立博客，这篇博文绝对是在中文教程中排很前面的，毕竟个人影响力在那儿摆着。

只要注意了这个问题，在建立repository时注意建立成个人页面，对一般fork的项目来说都是可以直接用的，目前还没见过放在项目页面上的博客项目，不过话又说回来，Jekyll相对于WordPress来说，用户群小太多了，可能是因为操作难度较大而且没有傻瓜式一站式解决方案、略微高冷吧，不过我也就因为喜欢那个Archive页面就坚持用下来了。