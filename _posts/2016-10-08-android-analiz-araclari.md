---
layout: post
title: Androguard Analiz Aracının İncelenmesi
tags: [android, androguard, reverse engineering, apk, analiz ]
---

Android uygulama dosyası APK uzantılı, "zip" formatında sıkıştırılmış arşiv dosyasıdır. 
Bu yazıda APK dosya analizinde tersine mühendislik yöntem ile python programlama dilinde geliştirilmiş Androguard yazılımı inceleyeceğiz. Androguard ile Android uygulamasının özelliklerine, kaynak kodlarına, izinlerine, DEX kodlarına, XML dosyalarına, uygulama kaynaklarına(resources) vb. özelliklerine erişebilirsiniz. 

Androguard yazılımını [Androguard Github](https://github.com/androguard/androguard) adresinden indirebilirsiniz. Androguard dosyasının içeriği aşağıdaki gibi olacaktır.

~~~
- androguard
  |- androauto.py
  |- androaxml.py
  |- androcsign.py
  |- androdiff.py
  |- androdis.py
  |- androguard
       |- __init__.py
       |- core
       |- decompiler
       |- ...
  |- androgui.py
  |- androlyze.py
  |- androsign.py
  |- androsim.py
  |- apkviewer.py
  |- setup.py
  |- tests
  |- tools
  |- ...
~~~

Androguard incelenmesinde ilk olarak **androlyze.py** dosyasından başlamak Androguard aracının öğrenmek ve anlayabilmek için kolay bir ilk adım olacaktır. 

androlyze.py dosyasını komut satırından çalıştırabilmek için;

```bash
	$ ./androlyze.py -s
```
komutu çalıştırılır. Komut ile Androguard'ın içeriğinin çalıştırıldığı python interaktif shell ekranı açılacaktır. Analize uygulama dosyasını tanımlamakla başlayacağız. Uygulama dosyasını tanımlamak için "AnalyzeAPK" fonksiyonu kullanılır. 

```bash
	In [1]: a, d, dx = AnalyzeAPK("android_uygulamasi.apk") 
	In [2]: a
	Out[2]: <androguard.core.bytecodes.apk.APK at 0x10d94bcd0>
	In [3]: d
	Out[3]: <androguard.core.bytecodes.dvm.DalvikVMFormat at 0x10d95f390>
	In [4]: dx
	Out[4]: <androguard.core.analysis.analysis.uVMAnalysis at 0x10d98abd0>
```

AnalyzeAPK fonksiyonu ile yaptığımız tanımlama sonucu 3 ayrı değer elde ettik. a sınıfı APK dosyası hakkında genel
bilgileri elde etmek, d ve dx sınıfları ise DEX kod analizinde kullanacağımız sınıflardır. Bu yazımda, a sınıfı ile elde edebileceğimiz bilgilere ilişkin yöntemlerden bir kaçı aşağıda açıklanmıştır.

Android uygulamasının versiyonunu ve sürüm numarasını `androidversion` değeri ile öğrenebiliriz.

	In [5]: a.androidversion
	Out[5]: {'Code': u'1', 'Name': u'1.0'}

Android uygulamaının ismine erişmek için filename değeri ile elde edebiliriz.

	In [6]: a.filename
	Out[6]: '/Users/ali/Desktop/f2305198a4789bc0f74afb7627bf998c0329b4.apk'

show() yöntemi ise APK dosyasının decompile sonucu göstemektedir. `FILES` bölümü `classes.dex` ve medya dosyalarını, `DECLARED ve REQUESTED PERMISSIONS` tanımlanan ve gerekli izinleri, ve sırasına göre ana aktiviteyi, bütün aktiviteleri, uygulamanın arka planda çalışan servislerini ve alıcıları göstermektedir.

```bash
	In [6]: a.show()
	FILES: 
		META-INF/MANIFEST.MF Unknown 3e6eaf8d
		META-INF/ALIAS_NA.SF Unknown -2dc737d3
		META-INF/ALIAS_NA.RSA Unknown 747b605e
		res/drawable/icon.png Unknown -5a550d00
		res/drawable/photo1.jpg Unknown -6a53287f
		res/drawable/photo2.jpg Unknown -16ec4d8f
		res/drawable/photo3.jpg Unknown -70b0687e
		res/drawable/photo4.jpg Unknown -ed53f1c
		res/drawable/photo5.jpg Unknown -4d16125a
		res/drawable/photo6.jpg Unknown 71e37589
		res/drawable/photo7.jpg Unknown 59274db3
		res/drawable/photo8.jpg Unknown 4fa7e656
		res/layout/main.xml Unknown -18f5a7f9
		AndroidManifest.xml Unknown 40ebbf8d
		resources.arsc Unknown -61619347
		classes.dex Unknown -2b13e650
	DECLARED PERMISSIONS:
	REQUESTED PERMISSIONS:
		android.permission.SEND_SMS
	MAIN ACTIVITY:  com.agewap.ero.gallery.GalleryActivity
	ACTIVITIES: 
		com.agewap.ero.gallery.GalleryActivity {'action': [u'android.intent.action.MAIN'], 'category': [u'android.intent.category.LAUNCHER']}
	SERVICES: 
	RECEIVERS: 
	PROVIDERS:  []
```
