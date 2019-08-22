---
title: Ubuntu Sistemlerde/Sunucularda Sudo User/Kullanıcı Nasıl Oluşturulur?
layout: post
date: 2019-08-22 14:30
image:
headerImage: false
tag: ubuntu
category: blog
author: alidasbasi
description: Ubuntu Sistemlerde/Sunucularda Sudo User/Kullanıcı Nasıl Oluşturulur?
---

`sudo` komutu sistem üzerinde yönetici işlemlerini gerçekleştirmeye yönelik tasarlanmıştır. Bu yazıda Ubuntu sistemlerde kullanıcı ekleme ve bu kullanıcıya `sudo` yetkisi vermeyi göreceğiz.

## Sunucuya Giriş Yapılması

Sunucuya `root` kullanıcı ile giriş yapılır:

{% highlight sh %}
$ ssh root@server_ip_address
{% endhighlight %}

## Yeni Kullanıcı Oluşturma ve `sudo` Yetkisi Tanımlanması

Yeni kullanıcı `adduser` komutu ile oluşturulur.

{% highlight sh %}
$ adduser kullanıcıadı
{% endhighlight %}

Komut çalıştırıldığında aşağıda verildiği gibi kullanıcı bilgilerini sizden talep edecektir.

{% highlight sh %}
root@ubuntu:~# adduser newuser
Adding user `newuser' ...
Adding new group `newuser' (1001) ...
Adding new user `newuser' (1001) with group `newuser' ...
Creating home directory `/home/newuser' ...
Copying files from `/etc/skel' ...
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
Changing the user information for newuser
Enter the new value, or press ENTER for the default
	Full Name []:
	Room Number []:
	Work Phone []:
	Home Phone []:
	Other []:
Is the information correct? [Y/n] Y
{% endhighlight %}

Kullanıcımızı oluşturduktan sonra sıra yetkilendirme aşamasına geldi. Kullanıcıyı yetkilendirmek için `sudo` grubuna ekliyoruz.

{% highlight sh %}
$ usermod -aG sudo kullanıcıadı
{% endhighlight %}

Test etmek için:

{% highlight sh %}
root@ubuntu:~# su - kullanıcıadı
$ sudo whoami
root
{% endhighlight %}