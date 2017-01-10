---
layout:     post
title:      "Android Service 服务保活"
subtitle:   "如何做一个打不死的小强"
date:       2017-01-08
author:     "Ouwenjie"
header-img: "img/post-bg-2015.jpg"
tags:
    - Android
---

在我看来，Service 被杀掉有两个大的原因：  
- 系统行为    
- 人为处理（任务管理器、强行停止）  

### 系统行为   
如果是系统自动回收了 Service 服务，一般是因为该服务长时间不活动，或系统的内存不足需要干掉一些它人为不重要的服务进程。  
那么，这里可以做提升优先级：  
- 设置为前台服务  setForeground()   

> 但是这个方法需要传 notification ，这个会在通知栏显示一个去不掉的通知，  
> 如果你的 APP 不是用户强烈需要在前台运行的，一般用户看了会挺反感。  

- 被系统杀掉后自动重启   

> 在 onStartCommand 方法里，可以返回 START_STICKY 使 service 被 kill 掉后自动重写创建   

- 提升 Service 所在进程的优先级  

> 在 AndroidManifest.xml 中，将 application 节点下设置 android:persistent="true"   

- 其它重启手段  

> 在 Service 被回收时，会调用 onDestroy() 方法，可以在这个方法重启 Service ，也可以发送一个广播，由广播重启 Service   

### 人为处理   
- 监听（开机、WIFI、界面唤醒）等系统广播，然后进行重启服务   
- 开启定时器，定期开启服务   
- 使用守护进程、互相监听、相互启动   
- 作为系统应用（安装到 system/app ）
- 使用 C 编写守护进程


### 参考资料  
- [怎么让 Android 程序一直后台运行，像 QQ 一样不被杀死？](https://www.zhihu.com/question/29826231)   



