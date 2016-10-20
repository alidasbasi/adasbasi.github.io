---
layout: post
title: Emulatore APK Dosyası Kurulumunun Yapılması
tags: [android, apk, emulator, mac ]
---

### Android APK dosyalarının Emulatore kurulumu nasıl yapılır?

***

__MAC:__

*	Emulator çalıştırılır.
*	APK dosyası "/Users/kullanici/Library/Android/sdk/platform-tools/" dizini altına kopyalanır.
*	"/Users/kullanici/Library/Android/sdk/platform-tools/" dizini içinde __`$ ./adb install dosya.apk`__ komutu çalıştırılır.
*	Emulatör ekranını kontrol ettiğinizde uygulamanın yüklenmiş olduğunu göreceksiniz.

__Linux:__

*	APK dosyası MAC sistemlerde olduğu gibi `android-sdk` dizini altında bulunan `platform-tools` dizinine kopyalanır.
*	__`$ ./adb install dosya.apk`__ komutu çalıştırılır.
*	Emulatörü çalıştırdığınız APK dosyasının yüklenmiş olduğunu göreceksiniz.