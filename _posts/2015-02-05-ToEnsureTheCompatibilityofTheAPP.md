---
layout: post
title: 保证 APP 的兼容性
category: Android
date: 2015-02-05
---

##保证 APP 的兼容性   

>保证 APP 能够兼容多个版本，主要可以在以下几个方面修改：   

- styles   
- layout   
- Support Library   
- 检测 Android 系统的版本   

<!-- more -->   


###**styles**    
你可以配置你的应用，在支持 Material Design 的设备上使用 Material 主题，   
在旧版本 Android 设备上使用旧的主题  

1. 在 `res/values/styles.xml` 中定义一个主题继承自旧主题（如 Holo ）   
2. 在 `res/values-v21/styles.xml` 中定义一个同名的主题，继承自Material 主题    
3. 在 `AndroidManifest.xml`，将这个主题设置为应用的主题       

>注意：如果你的应用设置了一个主题，但是没有提供后备 Style ,   
你可能依旧无法在低于 Android 5.0 版本的系统中运行。   

   

###**Layouts**    

如果你根据Material Design设计的应用的Layout中没有使用   
任何Android 5.0 (API level 21)中新的XML属性，   
他们在旧版本Android中就能正常工作。否则，你要提供后备Layout。   
你可以在后备Layout中定义你的应用在旧版本系统中的界面。   

1. 在`res/layout/`中提供后备 layout ，当用户的设备低于Android 5.0 时，使用该文件夹下的布局文件     
2. 在`res/layout-v21/activity.xml` 中定义Android 5.0(API 21)以上系统的 Layout    
   
>为了避免代码重复，在res/values中定义style，然后在res/values-v21中修改新API需要的style。   
使用style的继承，在res/values/中定义父style，在res/values-v21/中继承。   


###**Support Library**    

**`v7 support library r21` 及更高版本包含了以下 Material Design 特性：**    
- `Theme.AppCompat` 主题包含调色板主题属性   
- `RecyclerView` 组件用于显示数据集   
- `CardView` 组件用于创建卡片    
- `Palette`类用于从图片提取主色调   

**`Theme.AppCompat` 主题中提供了这些组件的 Material Design style：**     
- EditText   
- Spinner   
- CheckBox   
- RadioButton   
- SwithCompat   
- CheckedTextView   
- Color Palette   

**要获取Material Design style ，并用 v7 support library 自定义调色板，   
就要应用以下的一个`Theme.AppCompat`主题：**     

	<!-- extend one of the Theme.AppCompat themes -->
	<style name="Theme.MyTheme" parent="Theme.AppCompat.Light">
		<!-- customize the color palette -->
		<item name="colorPrimary">@color/material_blue_500</item>
		<item name="colorPrimaryDark">@color/material_blue_700</item>
		<item name="colorAccent">@color/material_green_A200</item>
	</style>

**列表和卡片**     

>`RecyclerView` 和 `CardView` 组件可通过 `v7 support libraries` 支持旧版本Android，   
但是有以下限制：     
- CardView 需要编程实现阴影和其他的padding    
- CardView 不能将附着与原件有重合部分的子视图    

###依赖    

要在Android 5.0之前的版本使用这些特性，需要在项目的Gradle依赖中   
加入Android v7 support library:     

	dependencies {
		compile 'com.android.support:appcompat-v7:21.0.+'
		compile 'com.android.support:cardview-v7:21.0.+'
		compile 'com.android.support:recyclerview-v7:21.0.+'
	}


###**检测Android 系统版本**    

以下特性只在 Android 5.0 (API level 21) 及以上版本中可用：   

- Activity 切换动画   
- 触摸反馈   
- Reveal 动画（填充动画效果，译者注）   
- 基于路径的动画   
- 矢量drawable   
- Drawable染色      

要保持向下兼容，请在使用这些特性是，使用以下代码在运行时检查系统版本：   

	if(Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP ){
		// 可以使用材料设计   
	} else{
		// 低于Android 5.0，不能使用材料设计主题   
	}    
	
>注意：要声明应用支持哪些Android 版本，   
在manifest文件中使用android:minSdkVersion和android:targetSdkVersion属性。   
要在Android 5.0中使用Material Design特性，设置android:targetSdkVersion属性为21。   
更多信息，参见<user-sdk> [API指南](https://developer.android.com/intl/zh-cn/guide/topics/manifest/uses-sdk-element.html)      

- - - - - - - - - - 


