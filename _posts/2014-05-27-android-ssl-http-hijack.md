---
title:  安卓通过http代理劫持ssl
author: admin
layout: post
permalink:  /android-ssl-http-hijack/
tags:
  - android
  - ssl
---




安卓ssl抓包

1、新版安卓系统支持从设备存储空间安装，直接将自签名的CA拷贝到设备存储空间，直接识别安装。

2、通过adb等方式

<!--more-->

adb常用命令

1、获得root权限：adb root  
2、设置/system为可读写：adb remount  
3、将文件复制到PC：adb pull /system/etc/hosts 文件名  
4、修改PC机上文件  
5、将PC机上文件复制到手机：adb push 文件名 /system/lib  
但在第五步时，有的人会报out of memory的错误这是因为直接用命令行启动，而没加一个参数造成的，所以用下面这个命令来启动就行了  
	
	$emulator -avd youravdname -partition-size 128

以fiddler代理为例，要想调试HTTPS必须把Fiddler生成的CA证书加入到可信，与iOS不同，Android下载crt或cer用户模式安装证书后是无效的。

1 下载http://www.fiddler2.com/dl/FiddlerCertMaker.exe安装完毕后移除Fiddler之前创建的证书，并生成新证书。（由于默认证书的兼容性问题）  
2 获取模拟器的cacerts.bks 然后把Fiddler的CA证书打进去。  
在PC操作  
把Fiddler的CA证书导出桌面，FiddlerRoot.cer。  
利用adb把手机里的证书全部导出来  
	adb.exe pull /system/etc/security/cacerts.bks cacerts.bks
然后把FiddlerRoot.cer文件移到与cacerts.bks同一目录  

	keytool -keystore cacerts.bks -storetype BKS -storepass changeit -importcert -trustcacerts -alias fiddler -file FiddlerRoot.cer

（keytool在JAVA当前环境的Java\jre7\bin下）然后会提示输入y后打包成功   Trust this certificate? [no]:  y，或者中文状态下输入：是  

设置系统目录可写权限，然后将合并后的证书文件push到/system/etc/security/目录下  
	
	adb shell mount -o remount,rw -t yaffs2 /dev/block/mtdblock0 /system
	adb push cacerts.bks /system/etc/security/cacerts.bks

这样就把新的证书导入进去了。