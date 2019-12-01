---
title: ARTS(05~NSDictionary)
date: 2019-11-17 18:54:08
tags:
- ARTS
categories:
- 持续学习
---
ARTS第五周，内容如下包括：算法，[剖析NSDictionary](https://ciechanow.ski/exposing-nsdictionary/) , <!--more-->

## Algorithm
本周实现了二叉树的前序中序后续的实现总结，包括栈和递归。[github](https://github.com/yFeii/leetCodePractice)
[98. Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/submissions/)
## Review
[剖析NSDictionary](https://ciechanow.ski/exposing-nsdictionary/)
在iOS6.0之前，NSDictionary一直是采用CFDictionary的实现（hash table），但是在6.0之后已经发生了改变。
在实例 NSDictionary 后，真实的类为_NSDictionaryI，（也可能为__NSSingleEntryDictionaryI,只有一个键值对的情况）。其内存布局如下
![pic](https://yfeii-blog.oss-cn-hangzhou.aliyuncs.com/weekly-arts/WeChat2b1e9d15eab7e208f26571b4b2042bac.png)
### objectForKey
伪代码如下
```javascript
- (id)objectForKey:(id)aKey
{
    NSUInteger sizeIndex = _szidx;
    NSUInteger size = __NSDictionarySizes[sizeIndex];
    
    id *storage = (id *)object_getIndexedIvars(dict);
    
    NSUInteger fetchIndex = [aKey hash] % size;
    
    for (int i = 0; i < size; i++) {
        id fetchedKey = storage[2 * fetchIndex];

        if (fetchedKey == nil) {
            return nil;
        }
        
        if (fetchedKey == aKey || [fetchedKey isEqual:aKey]) {
            return storage[2 * fetchIndex + 1];
        }

        fetchIndex++;
        
        if (fetchIndex == size) {
            fetchIndex = 0;
        }
    }
    
    return nil;
}
```
当经过hash 之后得出的index  在ivar 中的索引，通过object_getIndexedIvars 获得ivars。关于查找过程和冲突处理。
![pic](https://yfeii-blog.oss-cn-hangzhou.aliyuncs.com/weekly-arts/B428FEA3-2556-446A-B4DD-7172550F7988.png)
![pic](https://yfeii-blog.oss-cn-hangzhou.aliyuncs.com/weekly-arts/3AD66FC0-F50C-407C-868F-DB198E27F490.png)
## Tip
巧用 methos swizzling，在接入云信SDK时，选择分别依赖基础功能库和UI库，在实现UI定制时，通过methos swizzling,hook关键方法实现自定义需求（例如 sendMessage 方法实现对消息的扩展），也就是装饰者模式。
## Share
分享一篇关于AES 加密的动图图解![图解](https://coolshell.cn/articles/3161.html)
