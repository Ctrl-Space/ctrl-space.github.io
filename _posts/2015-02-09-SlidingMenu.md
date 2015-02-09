---
layout: post
title: SlidingMenu �Ļ���ʹ��
category: Android
date: 2015-02-09
---

##SlidingMenu �Ļ���ʹ��   
����һ������GitHub �Ŀ�Դ��Ŀ[SlidingMenu](https://github.com/jfeinstein10/SlidingMenu)   

> SlidingMenu ��һ����Դ��Android Library������Ϊ�������ṩ�ǳ��򵥵Ĵ���һ�����л����˵���Ӧ�á�    

###��Eclipse ����� SlidingMenu �������Ŀ��   

- �����غø���Ŀ����Ŀ[��](https://github.com/jfeinstein10/SlidingMenu)   
- �� Eclipse �У�import the library as an Android library project.   
- Ȼ�� Project -> Clean ����Ŀ�����������R�ļ�,etc.   
- ��󣬽���library ��ӵ������Ŀ�С�  

<!-- more -->   


###���Ϊ���Ӧ�ü��� SlidingMenu ��    

####��һ�ַ�����   

1. �� Activity �е��� SlidingMenu �Ĺ��췽�� `new SlidingMenu(Context context)`     
2.  Ȼ�����`SlidingMenu.attachToActivity(Activity activity, SlidingMenu.SLIDING_WINDOW | SlidingMenu.SLIDING_CONTENT)`
���ڶ���������������ѡһ������������ý�������˵����     

�磺   

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


####�ڶ��ַ�����   

1. ͨ���̳�`SlidingActivity` ���ṩ�໬����   
2. ͨ�� `setContentView` ,�������ݵĲ���   
3. ͨ�� `setBehindContentView` ���ò˵��Ĳ���   
4. ͨ�� `getSlidingMenu` ������ȡ����Ȼ��Բ˵����ж���   

�磺  

	/** 
	 * ��ʼ�������˵� 
	 */  
	private void initSlidingMenu(){  
		// ������������ͼ  
		setContentView(R.layout.content_frame);  
		getSupportFragmentManager().beginTransaction().replace(R.id.content_frame, new SampleListFragment()).commit();  
				  
		// ���û����˵���ͼ  
		setBehindContentView(R.layout.menu_frame);  
		getSupportFragmentManager().beginTransaction().replace(R.id.menu_frame, new SampleListFragment()).commit();  

		// ���û����˵�������ֵ  
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


####�����ַ�����   

1. ֱ���� XML �����ļ��м��� SlidingMenu   

�磺    

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
		
	

SlidingMenu ��Ҫ������⣺   

	// SLIDING_WINDOW �˵��������������ڣ�����ActionBar / Title��.   
	// SLIDING_WINDOW ģʽ���˵�ֻ������������   
	menu.attachToActivity(this, SlidingMenu.SLIDING_WINDOW);     

|  ����  |  ����  |   
| :---: | :---: |  
| viewAbove | ���˽� 0.0 |   
|��viewBehind��|�����˽� 0.0 |   
| touchModeAbove | �����˵�����Ч����TOUCHMODE_MARGIN��Ե Or TOUCHMODE_FULLSCREENȫ���� |   
| behindOffset | �˵���ƫ������ |   
| behindWidth | �˵��Ŀ�ȣ��˵��Ŀ�� + ƫ������ = 360dp ��  |   
| behindScrollScale | �˵�������ָ�����Ķ����������� 0-������1-��ȫ������� |   
| shadowDrawable | ��Ӱ  |   
| shadowWidth | ��Ӱ���  |   
| fadeEnabled | ʹ�������仯  |   
| fadeDegree | �����˵�ʱ�������仯 0-���䣬1-�  |   
| selectorEnabled | ���˽� 0.0  |   
| selectorDrawable | ���˽� 0.0  |   

- - - - - - - - - 




