---
layout: post
title: ubuntu - java kurulumu
---

Merhaba. Sözü uzatmadan doğrudan Java kurulumuna geçiyorum.
İşe Javayı Oracle' ın resmi sitesinden indirmekle başlıyoruz. [Bu adrese](http://www.oracle.com/technetwork/java/javase/downloads/java-se-jdk-7-download-432154.html) gidelim. `Accept License Agreement` seçenegini seçelim. Daha sonra sisteminize uygun(32 bit || 64 bit) `.tar.gz` uzantılı JDK(Java Development Kit)yı seçerek indirmeye başlayalım.

Masaüstüne `java` isminde bir dizin oluşturalım ve indirdiğimiz JDK paketini bu
dizinin içine atalı. Daha sonra yeni bir uçbirim açalım ve sırasıyla aşağıdaki komutları uygulayalım:

	$ cd ~/Masaüstü/java
	$ tar xvf jdk*
	$ sudo mv jdk1.7.0/ /usr/lib/jvm/
	$ sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.7.0/bin/java" 1
	$ sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.7.0/bin/javac" 1
	$ sudo update-alternatives --install "/usr/bin/javaws" "javaws" "/usr/lib/jvm/jdk1.7.0/bin/javaws" 1

Kurulum tamamlandı. Şimdi Java 7 sürümünü kullanmak için yapılandırmalıyız.
Aşağıdaki komutu girelim ve `jdk1.7.0` olan seçimi seçip entere basalım.

	$ sudo update-alternatives --config java

![Resim1][1]
[1]: http://github.com/gceylan/gceylan.github.com/raw/master/images/java_confing.png

Buraya kadar uyguladığımız işlemler sonucunda `Java`yı ve `Javac` derleyicisini
kurduk. Komut satırına `java -version` yazarsak resimdeki çıktıya ulaşmış
olmalıyız:

![Resim2][2]
[2]: http://github.com/gceylan/gceylan.github.com/raw/master/images/java_version.png

**Tarayıcılar için ek adımlar**

Önce tüm eklentileri kaldıralım:

	$ rm -f ~/.mozilla/plugins/libnpjp2.so ~/.mozilla/plugins/libjavaplugin_oji.so
	$ sudo rm -f /usr/lib/firefox/plugins/libnpjp2.so /usr/lib/firefox/plugins/libjavaplugin_oji.so

Şimdi yenilerini kuralım:

	$ mkdir -p ~/.mozilla/plugins

Sisteminiz 32 bit ise:

	$ ln -s /usr/lib/jvm/jdk1.7.0/jre/lib/i386/libnpjp2.so ~/.mozilla/plugins/

64 bit ise:

	$ ln -s /usr/lib/jvm/jdk1.7.0/jre/lib/amd64/libnpjp2.so ~/.mozilla/plugins/

Bu kadar yükleme yaptıktan sonra ilk java uygulamsını yapmadan gitmek olmaz.
[Buradan buyrun.](http://gceylan.github.com/903/ilk-java/)
