---
title: ARTS(06~autolayout)
date: 2019-11-24 22:01:14
tags:
- ARTS
categories:
- 持续学习
---
ARTS第六周，内容如下包括：算法，[autolayout](https://developer.apple.com/videos/play/wwdc2015/219/?time=326) , <!--more-->

## Algorithm
链表位移运算[github](https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/)
## Review
WWDC autolayout[autolayout](https://developer.apple.com/videos/play/wwdc2015/219/?time=326)，及开发[文档](https://developer.apple.com/library/archive/documentation/UserExperience/Conceptual/AutolayoutPG/ModifyingConstraints.html#//apple_ref/doc/uid/TP40010853-CH29-SW3)

### The Layout Cycle
![cycle](https://yfeii-blog.oss-cn-hangzhou.aliyuncs.com/weekly-arts/WeChat490dfb2e0aeaa03bd59bf2a32f7ad838.png)
### Update Pass
遍历调用view对应层级的 <code>updateViewConstraints </code>方法
### Layout Pass
遍历调用view对应层级的 <code>viewWillLayoutSubviews </code>方法，<code>layoutSubviews  </code>。

 
## Tip
分享一个使用断点的方式，首先下一个断点，然后按control+step into，有意外惊喜呦。

## Share
分享OC 对象创建的流程，![OC](https://yfeii-blog.oss-cn-hangzhou.aliyuncs.com/graphic_series/objc-alloc.png)
