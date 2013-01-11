---
layout: post
uri: /posts/2013/03
permalink: /posts/2013/03/index.html
title: "使用sshDroid，令android手机变成ssh服务器"
tags: [android,ssh]
tagline: "使用sshDroid，令android手机变成ssh服务器"
description: "使用sshDroid，令android手机变成ssh服务器"
exerpt: |-
---

##需要用到的软件如下：
[PieTTY-0.3.26.exe](/posts/images/posts/2013/03/PieTTY-0.3.26.exe "pietty-0.3.26")

[SSHDroid.apk](/posts/images/posts/2013/03/SSHDroid.apk "sshDroid.apk")

##在手机里面安装sshDroid.apk 


手机里面的运行效果如下：

<img src="/posts/images/posts/2013/03/sshDroid-pic2.png" heigh="442" width="228" title="pic-1" >

#连接手机上面的ssh服务器：

## 1.在电脑里面运行pietty.exe
 在**Host Name(or IP address) **里面输入你的手机里面显示的地址（例如： sftp://root@113.113.255.189)
 在 **Port**里面输入在手机显示的接在**host name**后面的几个数字，我的为:2222
效果如下图：
<img src="/posts/images/posts/2013/03/sshDroid-pic1.png" heigh="429" width="308" title="pic-2" >


点击**Open**后，连接到手机的ssh服务器，输入密码后，如下图：

<img src="/posts/images/posts/2013/03/sshDroid-pic3.jpg" heigh="443" width="584" title="pic-3" >

## 2. 使用cygwin或者是linux系统的终端输入如下的命令：(系统中需要安装ssh程序)
   {% highlight bash %}
  ssh -l root 113.113.255.189    #其中root为登陆的用户名，113.113.255.189为服务器地址
  {% endhighlight %}
  图片如下：
  
  <img src="/posts/images/posts/2013/03/sshDroid-pic4.jpg" heigh="271" width="593" title="pic-4" >
  
##建议，把sshDroid的检测wifi功能关闭
