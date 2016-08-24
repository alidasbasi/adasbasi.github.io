---
layout: post
title: Androguard Analiz Aracının İncelenmesi
---

Android uygulama dosyası APK uzantılı, "zip" formatında sıkıştırılmış arşiv dosyasıdır. 
APK uzantılı dosyaları incelemek için birçok araç mevcuttur. Bu yazıda APK dosya analizinde kullanılan,
python programlama dili ile geliştirilmiş Androguard yazılımı incelenmiştir. İlk olarak
Androguard yazılımını [Androguard Github](https://github.com/androguard/androguard) adresinden indirebilirsiniz. Androguard Anthony Desnos
ve Geoffroy Gueguen tarafından Python programlama dilinde geliştirilmiştir. Androguard ile Android uygulamasının 
DEX kodlarına, XML dosyasına, uygulama kaynaklarına vb. özelliklerine erişebilirsiniz. 

Androguard, Android uygulama dosyasını birçok yönden incelemeye imkan tanımaktadır. Androguard incelenmesinde ilk olarak **androlyze.py** 
dosyasından başlamak Androguard aracının öğrenmek için kolay bir ilk adım olacağı gibi aynı zamanda Androguard'ın gelişmiş özelliklerini
anlayabilmek bakımından kolaylık sağlayacaktır.

androlyze.py dosyasını komut satırından(Linux, MAC işletim sistemleri için) çalıştırabilmek için;

```bash
$ ./androlyze.py -s
```
komutu çalıştırılır. Komut ile python interaktif shell ekranı açılacaktır. Analize uygulama dosyasını okumakla başlanılır.

~~~
$ a, d, dx = AnalyzeAPK("dosya_adi.apk")

$a
<androguard.core.bytecodes.apk.APK at 0x10d94bcd0>
$d
<androguard.core.bytecodes.dvm.DalvikVMFormat at 0x10d95f390>
$dx
<androguard.core.analysis.analysis.uVMAnalysis at 0x10d98abd0>
~~~

AnalyzeAPK fonksiyonu sonucu elimizde 3 ayrı değişken oluşmuştur. a değişkeni APK dosyası hakkında genel bilgileri toplamak için kullanacağımız değişkendir. a değişkenine ilişkin yöntemlerden bir kaçı aşağıda açıklanmıştır.


~~~
$ a.androidversion # Uygulama hazırlanırken kullanılan Android sürüm numarası 
{'Code': u'1', 'Name': u'1.0'}
~~~
~~~
$ a.filename() # analiz edilen uygulamanın adı
'/f85cb70381b45161f4b0a70ebb28359e91caed9b78eae2f5a4a9011261a8.apk'
~~~

~~~
$ a.show() # APK dosyası hakkında genel bilgiler

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
~~~