---
layout: post
title: SlidingMenu 的基本使用
category: Android
date: 2015-02-09
---

##**SlidingMenu 的基本使用**   

这是一个来自GitHub 的开源项目[SlidingMenu](https://github.com/jfeinstein10/SlidingMenu)   

> SlidingMenu 是一个开源的Android Library，可以为开发者提供非常简单的创建一个带有滑动菜单的应用。    

###**在Eclipse 中添加 SlidingMenu 到你的项目中**   

- 先下载好该项目的项目[库](https://github.com/jfeinstein10/SlidingMenu)   
- 在 Eclipse 中，import the library as an Android library project.   
- 然后 Project -> Clean 该项目来生成所需的R文件,etc.   
- 最后，将该library 添加到你的项目中。  

<!-- more -->   


###**如何为你的应用集成 SlidingMenu ？**    

####第一种方法：   

1. 在 Activity 中调用 SlidingMenu 的构造方法 `new SlidingMenu(Context context)`     
2.  然后调用`SlidingMenu.attachToActivity(Activity activity, SlidingMenu.SLIDING_WINDOW | SlidingMenu.SLIDING_CONTENT)`
（第二个参数可在其中选一个，具体的作用将在下面说明）     

如：   

	public class SlidingExample extends Activity {

		@Override
		public void onCreate(Bundle savedInstanceState) {
			super.onCreate(savedInstanceState);
			setTitle(R.string.attach);
			// set the content view
			setContentView(R.layout.content);
			// configure the SlidingMenu
			SlidingMenu menu = new SlidingMenu(this);
			menu.setMode(SlidingMenu.LEFT);
			menu.setTouchModeAbove(SlidingMenu.TOUCHMODE_FULLSCREEN);
			menu.setShadowWidthRes(R.dimen.shadow_width);
			menu.setShadowDrawable(R.drawable.shadow);
			menu.setBehindOffsetRes(R.dimen.slidingmenu_offset);
			menu.setFadeDegree(0.35f);
			menu.attachToActivity(this, SlidingMenu.SLIDING_CONTENT);
			menu.setMenu(R.layout.menu);
		}
	}    


####第二种方法：   

1. 通过继承`SlidingActivity` 来提供侧滑功能   
2. 通过 `setContentView` ,设置内容的布局   
3. 通过 `setBehindContentView` 设置菜单的布局   
4. 通过 `getSlidingMenu` 方法获取对象，然后对菜单进行定制   

如：  

	/** 
	 * 初始化滑动菜单 
	 */  
	private void initSlidingMenu(){  
		// 设置主界面视图  
		setContentView(R.layout.content_frame);  
		getSupportFragmentManager().beginTransaction().replace(R.id.content_frame, new SampleListFragment()).commit();  
				  
		// 设置滑动菜单视图  
		setBehindContentView(R.layout.menu_frame);  
		getSupportFragmentManager().beginTransaction().replace(R.id.menu_frame, new SampleListFragment()).commit();  

		// 设置滑动菜单的属性值  
		SlidingMenu sm = getSlidingMenu();        
		sm.setShadowWidthRes(R.dimen.shadow_width);  
		sm.setShadowDrawable(R.drawable.shadow);  
		sm.setBehindOffsetRes(R.dimen.slidingmenu_offset);  
		sm.setFadeDegree(0.35f);  
		sm.setTouchModeAbove(SlidingMenu.TOUCHMODE_FULLSCREEN);  
		sm.setBehindScrollScale(0.0f);  
		sm.setBehindCanvasTransformer(mTransformer);  
		  
		setSlidingActionBarEnabled(true);  
	}    


####第三种方法：   

1. 直接在 XML 布局文件中集成 SlidingMenu   

如：    

	<com.jeremyfeinstein.slidingmenu.lib.SlidingMenu
		xmlns:sliding="http://schemas.android.com/apk/res-auto"
		android:id="@+id/slidingmenulayout"
		android:layout_width="fill_parent"
		android:layout_height="fill_parent"
		sliding:viewAbove="@layout/YOUR_ABOVE_VIEW"
		sliding:viewBehind="@layout/YOUR_BEHIND_BEHIND"
		sliding:touchModeAbove="margin|fullscreen"
		sliding:behindOffset="@dimen/YOUR_OFFSET"
		sliding:behindWidth="@dimen/YOUR_WIDTH"
		sliding:behindScrollScale="@dimen/YOUR_SCALE"
		sliding:shadowDrawable="@drawable/YOUR_SHADOW"
		sliding:shadowWidth="@dimen/YOUR_SHADOW_WIDTH"
		sliding:fadeEnabled="true|false"
		sliding:fadeDegree="float"
		sliding:selectorEnabled="true|false"
		sliding:selectorDrawable="@drawable/YOUR_SELECTOR"/>
		
	

**SlidingMenu 主要属性详解：**    

	// SLIDING_WINDOW 菜单将包裹整个窗口（包括ActionBar / Title）.   
	// SLIDING_WINDOW 模式，菜单只包裹内容区域   
	menu.attachToActivity(this, SlidingMenu.SLIDING_WINDOW);     

|  属性  |  作用  |   
| :---: | :---: |  
| viewAbove | 不了解 0.0 |   
|　viewBehind　|　不了解 0.0 |   
| touchModeAbove | 滑动菜单的有效区域（TOUCHMODE_MARGIN边缘 Or TOUCHMODE_FULLSCREEN全屏） |   
| behindOffset | 菜单的偏移像素 |   
| behindWidth | 菜单的宽度（菜单的宽度 + 偏移像素 = 360dp ）  |   
| behindScrollScale | 菜单栏随手指滑出的动作快慢程序 0-不懂，1-完全跟随进出 |   
| shadowDrawable | 阴影  |   
| shadowWidth | 阴影宽度  |   
| fadeEnabled | 使能亮暗变化  |   
| fadeDegree | 滑动菜单时的亮暗变化 0-不变，1-最暗  |   
| selectorEnabled | 不了解 0.0  |   
| selectorDrawable | 不了解 0.0  |   

- - - - - - - - -    

待续



