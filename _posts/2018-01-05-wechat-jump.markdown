---
title: "WebDriverAgent - 用iOS调试工具来hack微信跳一跳"
layout: post
date: 2018-01-05 13:00
tag: 
- WebDriverAgent
- iOS
- Wechat
star: true
image: /assets/images/profile_2.jpg
headerImage: true
projects: false
blog: true
category: blog
author: Jianfeng
description: iOS
externalLink: false
---

## 简介
最近微信的小程序功能上线了，其中有一个叫作“跳一跳”的小游戏进入了大家的视线。这个小程序一度成为年轻朋友们茶余饭后的话题，因为它提供了好友排名的功能，有一些爱出风头的小伙伴就开始了他们的刷分之旅。

作为手残党，我的分数根本就没办法超过三位数，直到我写完这篇博文我也不清楚那些玩到300+的人是怎么做到的（我确定她们连脚本是什么都不知道）。作为coder，我在玩跳一跳的时候也根本没办法集中精神，因为潜意识里总有一个声音不停地提醒我“你为什么不写个脚本让脚本来玩呢？”。好吧，最后那个声音说服了我，于是就有了这篇文章。

本文主要介绍了我使用Facebook的iOS开源调试工具WebDriverAgent以及简单的python脚本来进行刷分的过程。如果你对一下内容感兴趣，你可以继续往下读：
- [iOS平台软件测试自动化 - WebDriverAgent](#webdriveragent)
- [使用脚本玩游戏 - python]

## WebDriverAgent
### 什么是WebDriverAgent

WebDriverAgent是Facebook推出的一款iOS移动端测试框架。基本实现原理就是WebDriverAgent在iOS端实现了一个WebDriverAgent服务器（server），在主机上使用浏览器、WebDriverAgent的客户端（client）或者WebDriverAgent的客户端（client）代码就可以实现远程获取iOS设备的屏幕，并控制该iOS设备。
WebDriverAgent的客户端API支持启动、杀死应用，点击、滚动试图，截图、确定页面展示是否正确。

### 如何获取并安装WebDriverAgent

直接google搜索WebDriverAgent，就能够直接访问到facebook发布该工具的github页面，下面附上链接。

github项目链接：https://github.com/facebook/WebDriverAgent<br/>
参考文档： [iOS真机如何安装WebDriverAgent](https://testerhome.com/topics/7220)

#### 获取代码+自动配置

首先，从github上下载源码
{% highlight bash %}
git clone https://github.com/facebook/WebDriverAgent
{% endhighlight %}

根据主页说明，应该运行脚本./Scirpt/bootstrap.sh来进行自动配置，该脚本会使用Carthage下载所有的依赖，并且使用npm来打包响应的js文件，因此在运行脚本之前，你应该确定你的平台上Carthage和npm已经准备就绪。（Mac平台上直接使用homebrew来进行安装）
{% highlight bash %}
brew update
brew install carthage
brew install Pillow
brew install node

./Scripts/bootstrap.sh
{% endhighlight %}

执行完以上命令之后，如果提示无误，那么就可以进入到编译运行的阶段了。

#### 构建iOS应用并运行

已经完成项目的自动配置之后，你应该将xcode更新到最新版本（我的是v11），并使用xcode打开WebDriverAgent.xcodeproj这个文件。

Apple已经开放了真机测试，所以我们在编译安装的过程中并不需要使用苹果开发者账号。我们只需要简单地设置证书即可（先勾选自动管理证书，并在下拉菜单中将证书选择为自己的私人appleID）。

获取WebDriverAgent并不困难，但是根据我的经验，成功构建WebDriverAgent并成功建立调试框架并不是一件很容易的事情。

准备运行前，注意勾选以下内容：
1. Product -> Destination -> xxx's iPhone
2. Product -> Scheme -> WebDriverAgentRunner
3. Product -> Test

如果一切正常，手机上会出现一个空白图标的WebDriverAgentRunner应用，它会自动启动然后立即返回桌面。这表明你已经成功编译、安装并运行了该工具。

### 常见Bug汇总及解决方案

安装WebDriverAgent，具体调试过程有很多细节需要留意，否则很容易程序编译不成功。
最主要的问题有以下几类：
1. 证书问题
证书设置起来较为麻烦，如果编译时候提示证书类的错误，你需要仔细对照参考文档里的证书设置步骤进行操作。
2. 发布者账号重名
这是另一个比较坑的地方。
由于我们使用的是免费证书，需要修改一下WebDriverAgent的BundleID，很简单地加入一些后缀就可以了，目的就是保证不要跟其他开发者账号重名。
3. 手机端信任
如果手机上出现了空白图标的WebDriverAgentRunner工具，但是运行时候提示“信任”问题，这说明你需要在iPhone设置中将该开发者账号添加入信任的开发者列表，具体操作就不说了。

## 使用Python脚本辅助玩跳一跳

跳一跳这个游戏唯一的用户输入就是点按屏幕的时长。经过一系列测试，我发现棋子跳跃的距离竟然跟点击屏幕的时间呈正比！玩家在玩的时候由于主观感受的误差，很容易就对跳跃距离、点击屏幕时间的估计产生误差，从而出现失误，但使用脚本可以完全消除以上误差，导致每次跳跃的距离都能够被精确控制，这样就能万无一失。

### 思路

在每次棋子稳定的时候对iPhone屏幕进行截图，使用Matplotlib工具打开。玩家用鼠标点击图片中棋子当前的位置和理想的落脚点的位置，Matplotlib根据两次鼠标点击事件的坐标来计算两点间的距离。

获得距离之后，脚本将该距离乘上经过测量得到的跳跃系数，获得正确的点击屏幕时间长度，最后使用WebDriverAgent的客户端发送点击屏幕的指令控制棋子的跳跃。

### 实现方法

使用Matplotlib里的动画（animation）工具，定时call下面这个截图函数，用于获得最新的iPhone屏幕画面。

{% highlight python %}
def updatefig(*args):
    global update
    if update:
        time.sleep(1)
        cast_screenshot()
        im.set_array(update_img_data())
        update = False
    return im,
{% endhighlight %}

使用定义onClick函数用于记录鼠标点击的位置坐标，并根据坐标获得棋子理想的跳跃距离。
{% highlight python %}
def onClick(event):
    global update
    global ix, iy
    global click_count
    global cor

    # next screenshot
    ix, iy = event.xdata, event.ydata
    coords = []
    coords.append((ix, iy))
    print('now = ', coords)
    cor.append(coords)

    click_count += 1
    if click_count > 1:
        click_count = 0

        cor1 = cor.pop()
        cor2 = cor.pop()

        distance = (cor1[0][0] - cor2[0][0])**2 + (cor1[0][1] - cor2[0][1])**2
        distance = distance ** 0.5
        print('distance = ', distance)
        jump(distance)
        update = True
fig.canvas.mpl_connect('button_press_event', onClick)
{% endhighlight %}

最后，在onClick函数中，脚本会call jump函数用来发送精确的点击屏幕的信号至iPhone，从而实现棋子的精确跳跃。
注意：time_coefficient是我经过多次试验得到的最佳乘系数。
{% highlight python %}
def jump(distance):
    press_time = distance * time_coefficient
    print("press_time = ", press_time)
    s.tap_hold(100, 100, press_time)
{% endhighlight %}

### 结果

实现完该系统之后，我进行了简单的测试：在我们设置了一个有效的乘系数之后，我轻松就获得了300+的高分。当然想要继续刷分当然可行，但是刷分这种事情很无聊，我就不去干了。

![Markdowm Image][1]{: class="smaller-image" }

## 总结

这篇博文介绍了用WebDriverAgent结合python脚本进行iOS移动端的软件自动化的过程，基于以上的框架，我们很容易实现AI来玩小游戏（娱乐功能），或者实现软件测试的自动化（主要功能）。


[1]: /assets/images/4_wechat_jump_result.png
