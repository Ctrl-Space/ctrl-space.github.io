---
layout: post
title: Application 类的常见使用 
category: Android
date: 2015-04-13
---   

#### 关于 Application   

>Application 是一个基类，可用于保持那些需要维持全局的应用状态信息，   
通常我们是不需要指定一个Application 的，系统会创建一个默认的 Application.   
>开发者可以也实现自己的 Application 然后在 AndroidManifest.xml 中的 `<application>` 标签里指定该  Application.   
当应用程序被创建时，该 Application 类就会被实例化.   

<!-- more -->   

>在通常情况下是不需要 Application 的子类去保存过多的信息，因为在大多数情况下，     
我们可以通过一个静态的单例类去提供一种更模块化的方式去完成同样的工作。并在 Application 中管理这些单例对象，如果该单例类需要全局的Context ，可以在该单例Java 类的构造函数中通过 `Context.getApplicationContext()` 的方式去保存一个全局Context 。   

####创建 Application 子类   

	```Java  
	import android.app.application
	public class DemoApplication extends Application {
		@override
		public void onCreate(){
		}
		
		public void funA(){}
	}
	```   

####在AndroidManifest.xml 中指定Application   

	```Java   
	<application
		android:name=".DemoApplication"
		···
	>
		···
	</application>
	```   

####在Activity 中调用Application 对象的方法   
  
	```Java   
	DemoApplication demoApplication = (DemoApplication) getApplication();   
	demoApplication.funA();

	```

#### 常见应用情况   

#####应用程序组件之间的数据传递   

>当两个Activity 之间需要传递数据时，一般可以使用 Intent 携带信息，但是它只能携带一些基本的数据类型，比较复杂的数据需要实现erializable或者Parcellable接口，这其实是Android的一种IPC数据传递的方法。   
>但是，如果我们使用Application 来储存数据，那只需要传一个索引的标号或者键值对的键值过去，另一个Activity 就能获取到该数据。例如：在Application 中创建一个HashMap<String,Object>，以字符串为索引，Object 为值，就可以存储任何对象了。在使用时，只需要将让Intent 携带 字符串索引就可以找到相应的对象，Activity 获取后通过向下转型获得实际对象。   
		
#####数据缓存   

>可以在Application 中缓存一定的数据。比如有一个Activity 需要从网站获取一些数据，获取完之后就可以把这个数据cache 到 Application 当中，当页面设置到其它 Activity 再回来的时候，就可以直接使用缓存好的数据了。但如果需要cache一些大量的数据，最好是cache一些 (软引用)SoftReference ，并把这些数据cache到本地rom上或者sd卡上。如果在application中的缓存不存在，从本地缓存查找，如果本地缓存的数据也不存在再从网 络上获取。 

#####管理应用程序的生命周期   

>管理好Application 的生命周期对于资源释放和防止内存泄漏是很重要的事。   

>在Application 创建的时候，onCreate() 方法会被调用，当Application 被终止时，onTerminate() 会被调用。   

>如果在Application的oncreate中执行比较耗时的操作，将直接影响的程序的启动时间。不些清理工作不能依靠onTerminate完成，因为android会尽量让你的程序一直运行，所以很有可能 onTerminate不会被调用。   
>

#####内存泄漏   

>通常情况下，当用户转动手机的时候，android会重新调用OnCreate()方法生成一个新的Activity，原来的 Activity应该被GC所回收。但如果有个对象比如一个View的作用域超过了这个Activity(比如有一个static对象或者我们把这个 View的引用放到了Application当中)，这时候原来的Activity将不能被GC所回收，Activity本身又持有很多对象的引用，所以 整个Activity的内存被泄漏了。

**经常导致内存泄漏的一些原因：**   

keeping a long-lived reference to a Context.持有一个context的对象，从而gc不能回收。   

1. 一个View，的作用域超出了所在的Activity的作用域，比如一个static的View或者 把一个View cache到了application当中 etc   

2. 某些与View关联的Drawable的作用域超出了Activity的作用域。   

3. Runnable对象：比如在一个Activity中启用了一个新线程去执行一个任务，在这期间这个Activity被系统回收了， 但Runnalbe的任务还没有执行完毕并持有Activity的引用而泄漏，但这种泄漏一般来泄漏一段时间，只有Runnalbe的线程执行完闭，这个 Activity又可以被正常回收了。   

4. 内存类的对象作用域超出Activity的范围：比如定义了一个内存类来存储数据，又把这个内存类的对象传给了其它Activity 或者Service等。因为内部类的对象会持有当前类的引用，所以也就持有了Context的引用。解决方法是如果不需要当前的引用把内部类写成 static或者，把内部类抽取出来变成一个单独的类，或者把避免内部对象作用域超出Activity的作用域。   

5. out Of Memery Error 在android中每一个程序所分到的内存大小是有限的，如果超过了这个数就会报Out Of Memory Error。android给程序分配的内存大小与手机硬件有关，以下是一些手机的数据：   

G1:16M Droid:24 Nexus One:32M Xoom:48Ms   
所以尽量把程序中的一些大的数据cache到本地文件。以免内存使用量超标。     


部分内容来自`http://blog.csdn.net/lieren666/article/details/7598288`    


