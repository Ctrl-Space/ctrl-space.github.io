---
layout:     post
title:      "Android 中 View 的 Touch 事件分发机制"
subtitle:   "实现复杂交互功能的必备基础"
date:       2016-05-20
author:     "Ouwenjie"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---

> 这东西实在有点混乱，各种方法和返回值，每次用到都要重新看一遍；这次，把结果用自己的理解写下来。

**先记住几点**
- View 事件的传递是从 父 ViewGroup 传到 子 View 的.   
- 每一次 ACTION_DOWN 事件，只能被消费一次，而且，如果 View 不消费，将再没有机会消费剩下的事件.   
- 每个事件都是以 ACTION_DOWN 开始 ACTION_UP 结束.   
- 所有Touch事件都被封装成了 MotionEvent 对象，包括 Touch 的位置、时间、历史记录以及第几个手指(多指触摸)等.   
- 对事件的处理包括三类，分别为   
传递—— dispatchTouchEvent()
拦截—— onInterceptTouchEvent()
消费—— onTouchEvent() 和 OnTouchListener()   

- - - - - - - - - -    

`public boolean dispatchTouchEvent(MotionEvent event) {}`   

> 在此方法内，首先判断了该 View 是否 touchable,是否有设置 OnTouchListener.
> 如果上面两个判断同时为 true ，就会去执行 OnTouchListener.onTouch(); 并设置`result`等于 onTouch() 的返回值.
> 如果上面两个判断不同时为 true,则不执行 OnTouchListener.onTouch(); result 还是 == false.
> 如果 result == false，则说明 onTouch 没有消费事件，此时去执行 `onTouchEvent()`, 并设置 result 为 onTouchEvent() 的返回值.
> 返回 result   

结论：通过此方法一级一级地下发事件，可以看到，dispatchTouchEvent 的返回值 的结果是由 `onTouch()` 或 `onTouchEvent()` 决定的，即 result
返回 `true` ，则表示消费了该事件，
返回 `false` ,则表示没有消费这个事件，将会传递给上级的 `onTouchEvent()`，直到 Activity 的 `onTouchEvent()`。   

- - - - - - - - - -    

`public boolean onTouchEvent(MotionEvent event) {}`

> `onClick()` 的方法是在 `onTouchEvent()` 方法的 `ACTION_UP` 中执行的.
结论：若该方法返回 `true`,则说明消费了此次事件，将会继续接收下一次事件，若返回 `false`,则下一次事件将不会抵达这里.

- - - - - - - - - -   

`public boolean onInterceptTouchEvent(MotionEvent event) {}`

> 先判断`disallowIntercept`，若是 `true`,则是不允许拦截，只能返回 `false`.
> 若`disallowIntercept`为 `false`,才能执行`onInterceptTouchEvent()`.

结论：返回 `true` ，表示拦截此次事件，事件将不会传递给子 View，交给自己的 onTouchEvent()处理。
返回 `false` 则不拦截。   

> 参考文章
[trinea:Android Touch 事件传递机制](http://www.trinea.cn/android/touch-event-delivery-mechanism/)   
[图解 Android Touch 事件分发机制](http://www.jianshu.com/p/e99b5e8bd67b)
