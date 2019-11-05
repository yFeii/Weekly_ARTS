---
title: ARTS(04~NSMutableArray)
date: 2019-11-03 23:14:16
tags:
- ARTS
categories:
- 持续学习
---
ARTS第四周，内容如下包括：算法，[剖析NSMutableArray](https://ciechanow.ski/exposing-nsmutablearray/) , <!--more-->

## Algorithm
[94. Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/submissions/)
## Review
[剖析NSMutableArray](https://ciechanow.ski/exposing-nsmutablearray/) 
通过反编译获取其成员，关于如何进行反编译可[参考这篇文章](https://devyang.space/2019/08/08/KVO/)
* _used 是计数的意思
* _list 是缓冲区指针
* _size 是缓冲区的大小
* _offset 是在缓冲区里的数组的第一个元素索引  

__NSArrayM 用了环形缓冲区 (circular buffer)，
优点是：除非缓冲区满了，否则在任意一端插入或删除均不会要求移动任何内存。当从中间选择插入时，或选择对包含有较少元素的一边进行移动。
不足：当环形缓冲区扩容时，开辟新的空间，并把原空间的值复制到新空间中。
这里会有一个安全隐患，当多线程操作时，如果线程a，b同时执行添加操作，那么造成crash的原因是，其中某一个线程使得数组进行了扩容，此时或执行复制操作，或释放老值，存入新的数组，此时线程b再去访问时，原始数据已经被释放了。

## Tip
在做安全防护时，通常会采用对集合对象进行防越界操作，但是结合对象又是类簇的形式，所以想要获得所有的实体类，可以通过<code>objc_getClassList </code>来获取所以已注册类的信息，在判断是否是NSArray的子类。

## Share
[《读图解TCP/IP》](https://devyang.space/2019/11/03/%E5%9B%BE%E8%A7%A3TCP-IP/)
