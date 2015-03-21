---
layout: post
title: 在 Ubuntu 下安装 Android Studio 
category: Android
date: 2015-03-21
---   

###一/ 配置JDK   


1. 首先到 Oracle 官网下载 JDK (Linux 版，x86 还是 x64 看个人电脑)   
比如我下载的是 jdk-8u40-linux-x64.tar.gz    
这种格式是我使用得最多的压缩格式。它在压缩时不会占用太多CPU的，而且可以得到一个非常理想的压缩率。   

2. 下载完成后，将该压缩包移动到 /usr/lib/jvm 下进行解压   
tar -zcvf jdk-8u40-linux-x64.tar.gz   
得到 /usr/lib/jvm/jdk1.8.0_40   

3. 解压之后，开始配置 JDK 环境   
<!-- more -->   
(如果 系统中已经安装了 OpenJDK，可以先卸载了，具体方法请Google)   
sudo vim ~/.bashrc   

4. 在打开的文件后面添加各种路劲   
export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_40   
export JRE_HOME=$JAVA_HOME/jre   
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib   
export PATH=.:$PATH:$JAVA_HOME/bin:$JRE_HOME/bin:$JAVA_HOME/lib   

5. 然后保存文件，退出。      

6. 执行 java -version 测试是否配置成功   
出现如下所示的信息表示配置成功   
java version "1.8.0_40"   
Java(TM) SE Runtime Environment (build 1.8.0_40-b26)   
Java HotSpot(TM) 64-Bit Server VM (build 25.40-b25, mixed mode)   

###二/安装Android Studio   

1. 这个也是十分简单，到Android 官方网站下载到 Linux 版的 Android Studio   

2. 在/usr 目录下创建文件夹 sudo mkdir android-studio   
3. 在Downloads 目录下，sudo mv android-studio-ide-135.1740770-linux.zip /usr/android-studio   
4. 接着解压该 zip 包，unzip android-studio-ide-135.1740770-linux.zip   
5. 解压后，进入 /usr/android-studio/android-studio/bin   
执行 ./studio.sh

###常见问题   

1.    
Q : Android Studio Setup Wizard 过程中，遇到“unable to run mksdcard tool.”   
A : sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0 lib32stdc++6   

2. 
Q : Failed to fetch URL http://dl-ssl.google.com   
A : 请翻墙，或配置 Hosts，具体请Google   


