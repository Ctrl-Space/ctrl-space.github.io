---
layout: post
title: 代码中的Material Design（一）
category: Android
date: 2015-07-15
---   


##代码中的Material Design（一）   

>这是一篇在实际项目中开发Material Design风格应用的总结性文章   

>掌握从零开发一款Material Design 的应用所需的一切

<!-- more -->   

####使用AppCompat
1. 使用`ToolBar`替代`ActionBar`   

>[ToolBar 使用教程](http://blog.mosil.biz/2014/10/android-toolbar/)

2. Activity 必须继承或间接继承 `AppCompatActivity`   

>它继承于`FragmentActivity`，所以还可以继续使用 Fragment .

3. 使用（或继承）`Theme.AppCompat`作为APP的主题   

>一般使用`Theme.AppCompat.NoActionBar `，因为要使用`ToolBar`

4. 使用新的`Dialog`   

>直接将 AlertDialog 改为`android.support.v7.app`包下的 AlertDialog 即可

5. View 的 Theme   

>Android 5.0引入一个全新的特性，允许你对view设置theme，这种设置会影响控件及其包含的子控件。
>使用AppCompat v22.1.x 后，也可以给你 layout 里的任意视图设置主题。
>Toolbar常用的ThemeOverlay
	`ThemeOverlay.AppCompat.Light.ActionBar`
	`ThemeOverlay.AppCompat.Dark.ActionBar`



####使用新的控件和兼容包
 - `com.android.support:appcompat-v7`
 - `com.android.support:design`
 - `com.android.support:cardview-v7`
 - `com.android.support:recyclerview-v7`
 - `com.android.support:palette-v7`
 - ···

 

####使用标准Material Design Icons
- [Material icons guide](http://google.github.io/material-design-icons/)
- [官方 icon](https://www.google.com/design/icons/)
- [Git 仓库](https://github.com/google/material-design-icons)
- ···


###参考资料
[Material 适配详解](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0511/2862.html)   

[实现Instagram的Material Design概念设计](http://www.jcodecraeer.com/a/anzhuokaifa/androidkaifa/2015/0204/2415.html)   

[Android 5.x Theme 与 ToolBar 实战](http://blog.csdn.net/lmj623565791/article/details/45303349)   



- - - - - - - - - - 

至此，算是搭建好了项目UI设计的基本框架