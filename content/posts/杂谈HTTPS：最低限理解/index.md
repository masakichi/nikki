---
title: "杂谈 HTTPS：最低限理解"
date: 2020-05-23T20:15:12+09:00
lastmod: 2020-05-24T00:12:47+0900
tags: ["杂"]
isCJKLanguage: true
draft: false
slug: "basic-understanding-of-https"
aliases:
  - "/post/basic-understanding-of-https/"
---

现在但凡我们使用浏览器访问网站，尤其是大型的网站而言，基本 HTTPS 都变成了标配，对于普通用户（也就是本文的读者）来说在地址栏的部分会有一把锁🔒，它代表你和你要访问的网站之间的通讯是安全的。但是对于这个安全具体是什么意思，可能很多人不太搞得清楚，我想写一篇简单的文章谈谈我的理解。如果你赶时间，简单地说，这把锁基本（试图）解决三个主要问题：

1. 你和对方使用只有你们俩知道的密码本加密通讯
2. 你和对方用足够安全的方式分享只有你俩知道的那个密码本
3. 你需要有个方法判断对方是不是真的能信得过

<!--more-->

## 加密通讯

好奇的你肯定就有一个朴素的疑问了，通过什么来保证你和网站之间的通讯是安全的呢？这个并不难理解，如果你看过一些谍战片（比如孙红雷主演的《潜伏》）你就有个大概的印象了，他们通过一本密码本来通讯，就是说你有了这本密码本，把电台里听到的密文通过那本密码本，就能解密出电台里说的是什么了，反过来你要把你的情报送出去，就再通过那本密码本把你的情报翻译成密文然后通过电台传出去就行了。这样敌人哪怕截获或者监听你们的通讯，只要他们没有那本密码本，他们也就没有办法知道你们在说些什么。

## 秘密共有

到这里似乎没有任何问题，但是敏锐如你马上发现，怎么把那本密码本送到友军的手里呢？很显然需要额外的一个接头步骤，怎么接头呢？一般是这样有这样几种，你到一个看似是普通客栈或者药房的地方，跟掌柜的说一些意味不明或是特定的谜语，这里说什么并不重要，重要的是你要确定这个谜语只有对方知道什么意思，并且他做出了符合你预期的动作，你就能确定那个人就是你要找的人，然后你就能把那本密码本给他了。或者可能还有一种，你可以登报写个寻人启事或者讣告啥的，普通人可能就当成正常的寻人启事或者讣告了，但是你知道你的同志，而且只有你的同志知道你背后的意思，并且你的同志知道这个背后的意思之后他就能拿到或者推算出密码本是什么了。

于是，你和你的同志之间就已经共有了同一本密码本并且这个世界上只有你俩知道，你们通过这个密码本通讯当然也就安全啦。当然世界不会这么单纯，你们可能担心密码本会不会泄漏呀，或者密码会不会被破解呀，之类的。这些其实比较好解决，经常换密码，密码尽可能复杂基本能缓解这个问题。但是，这里有一个更严重的问题需要注意，你和你的同志可以进行只有你俩才知道的通讯，这很好，但是时间一长，你就开始疑心暗鬼了。这个老兄我能信得过吗？万一这个老兄是个细作，你们的通讯再安全也不能避免你的情报泄漏给敌人不是嘛？

## 信用体系

没有错，在这套通讯系统之外我们还需要一套信用体系。怎么办呢？我们需要引入证书的概念，你有了你友军的证书，一看这证书是你的上级给他批的，而且证书的有效期还在，至少你在这段有效期内是可以相信他的，你说为什么？因为你相信你的上级没有投敌，那他相信的人你也可以相信，你需要相信上级的判断。但是夜深人静的时候，你又开始寻思了，万一我的上级投敌了怎么办呢？这个时候你可能就需要想办法去查看他的证书有没有效了......然后你一级一级往上查，直到查到你们的一把手，你发现他也有证书，但是他的证书是他自己给自己发的，你可能想万一他老也......但是目前你只能选择相信他，因为如果你不相信他你们的整个信任系统就随之崩溃变得一文不值了，所以到最后，到最上级，他们的地位是不证自明的。只要最上级的证书是你信任的，那么整条信任链就能成立。

## 最后

以上大概就是你用浏览器访问 HTTPS 网站的时候，双方会去解决的课题了，只不过更数学一点儿。比如用密码本的加密方式，实际上会使用对称加密技术。而共享密码本的过程使用一种叫公开密钥加密的技术。至于信用体系，则会有第三方公信力很高的证书颁发机构颁发的根证书、他们给一些中介颁发中间证书，以及中介给普通网站颁发的证书构成。而你的浏览器或者系统则会预装根证书，网站则负责提供自己的证书以及中介的证书（如果有的话），这样用户的浏览器或者系统就能形成整条信任链从而相信这个网站是可信的。当然还有其他的细节，但是有这三个概念基本能让你对浏览器地址栏的这把小琐有个大概的了解了。在此基础上，我会在下一篇文章结合生活中的实际体验写一下我对安全和信任的一些思考。