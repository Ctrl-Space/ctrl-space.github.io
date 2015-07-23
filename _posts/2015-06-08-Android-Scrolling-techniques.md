---
layout: post
title: Material Design 的界面滚动技术
category: Android
date: 2015-07-22
---
##界面滚动技术   

###Scrolling   

**可滚动的区域**   

- 状态栏 (Status bar)   
- 导航栏 (Tool bar)   
- 标签栏 (Tab bar)   
- 弹性空间 (flexible space)   

<!-- more -->

**标准 app bar**   

在手机上，标准的 app bar 高度为56dp，大屏幕设备则是64dp。   
在界面滚动时，有两个行为选项：   

1. app bar 可以随着滚动滚出屏幕，然后在反向滚动时重新回到界面。   

2. app bar 保持固定的顶部。   

**Tabs**   

app bar 是一个包罗万象的组件，可以包含如（tool bar, tab bar, flexible space.）等。   

tabs 可以有下列行为之一：   

1. tab bar 保持固定在顶部，而 tool bar 滚动。   

2. tool bar 和 tab bar 都保持固定在顶部，只有下面的内容滚动。   

3. tool bar 和 tab bar 都随着内容滚动而滚动， tab bar 在内容反向滚动时恢复显示，tool bar 在反向滚动回顶部时恢复显示。   


**flexible space**   

因为 app bar 是非常灵活的，它可以被扩展以适应更大的字体或图像，创造一个灵活的空间。   
它有两个显示选项：   

1. 固定模式：tool bar 固定不动。当界面在顶部时开始滚动，flexible space 开始扩展。反向滚动时，弹性空间缩小至tool bar 大小。     

2. 视差模式：整个 app bar 滚动，有一种 app bar 从 status bar 底部拉出，而内容从 app bar 底部拉出来的视差效果。   


**带图片的flexible space**   


在弹性空间放置图片，在用户滚动界面的时候渐渐淡出，同时 app bar 的高度也随着变化。   

图片和动画效果可看官方   

**与内容重叠的 flexible space**      
app bar 起始的部分与内容有重叠，叠在内容的背后。向上滚动时，app bar 滚动地比内容滚动的速度更快。      
直到内容不再覆盖于app bar。并允许内容在app bar 下面来回滚动。      



[Scrolling techniques](http://www.google.com/design/spec/patterns/scrolling-techniques.html#)   


技术实现可下面的参考博客   

[Android M新控件](http://blog.csdn.net/feiduclear_up/article/details/46514791)   

[CoordinatorLayout与滚动的处理](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0717/3196.html)   
