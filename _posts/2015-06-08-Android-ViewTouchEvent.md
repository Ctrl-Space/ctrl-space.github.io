---
layout: post
title: 触摸事件的传递机制
category: Android
date: 2015-06-08
---   

#### 触摸事件的传递机制   
>粗略地说，控件触摸，事件派发是先传递到最顶级的ViewGroup，再由ViewGroup递归传递到View的。   
会调用dispatchTouchEvent方法，而在dispatchTouchEvent中,先判断touchable 和 onTouchListener 是否为空，   
为空则直接调用 onTouchEvent 方法，先执行的是onTouch方法，   
然后再根据onTouch 的返回值判断是否调用onTouchEvent 方法，而在onTouchEvent方法里，ACTION_UP 事件将触发onClick 方法。   
子View中如果将传递的事件消费掉，ViewGroup中将无法接收到任何事件。   

<!-- more -->   


**各方法返回值的情况**   

**dispatchTouchEvent**   

返回 **true**  : 可以处理，继续触发下一个ACTION   
   
返回 **false** : 处理不了，不再触发下一个ACTION   

- - - - - - - - - -   


**onInterceptTouchEvent** （仅在 ViewGroup 以及其子类的控件中调用）   

默认返回 **true**  : 不阻止事件继续向子View传递   

返回 **false**     : 阻止事件继续向子View传递   

- - - - - - - - - -   


**onTouch** （在该控件的touchable 属性为true , 且有 setOnTouchListener 的情况下才会调用 onTouch）  

返回 **true**  : 不触发 onTouchEvent 方法   

返回 **false** : 触发 onTouchEvent 方法   
  
- - - - - - - - - -   

**onTouchEvent** （一个控件是enable且clickable则继续进入到该event的switch判断中，然后最终onTouchEvent都返回了true）    

返回 **true**  : 处理完成，请继续 （super.dispatchTouchEvent 的返回值与 onTouchEvent 的返回值相同）  

返回 **false** : 处理不了，请给上级   





