---
layout: post
title: Spring Framework hakkında kısa notlar
---

### Spring Framework Nedir? ###
	- Spring Framework, Spring Source firmasının geliştirmiş olduğu ve Kurumsal uygulamalara dönük çözümler getiren büyük bir ekosistemdir, altyapıdır.
	- Açık kaynak kodlu (Topluluğu geniş)
	- POJO-Nesne Tabanlıdır.
	- Mimarı Rod Johnsondır.
	- Ekim 2002 de çıkarttığı, Expert One-on-One J2EE Desing and Development kitabında tanıtmıştır.
	- İlk versiyonu (v1.0) 2003 tarihinde Rod Johnson tarafından çıkartılmıştır.
	- Apache License 2.0 ile lisanslanmıştır.

Inversion Of Control (IOC) ve Dependency Injection (DI) kavramları Spring Framework' ün çekirdeğini oluşturmaktadır.

	Problemler
	- Bağlaşım kesme problemi
	- Transaction desteği (Veritabanı işlemleri için önemli)
	- Güvenlik alt yapısı
	- Dağıtık programlama ihtiyacı

Yukarıdaki problemleri çözmek için 1998 yılında `EJB` adında bir teknoloji oluşturuldu. Problemleri çözmede kolaylık getiremedi ve kodu gereksz karmaşıklaştırmasından dolayı popülerliği zaman içinde azaldı.

	Spring’ in Çözüm getirdiği alanlar:
	- Modern Web (Rest, HTML5, AJAX)
	- Data Access (NoSQL, Map Reduce, RDBMS, Cloud)
	- Integration (Enterprise Orchestration, Messaging, -Batch applications)
	- Mobil alanlar (Android, Iphone)
	- Sosyal ağlarla entegrasyon (Facebook, Twitter, Linkedin)
	- Güvenlik (Authorization ve Authentication entegrasyonu)
	- Cloud Ready (Google App Engine, Amazon, Cloud Foundry)

### Inversion of Control (Dependency Injection) nedir? ###

En kısa anlamıyla `bağımlılıkları yok etmek` şeklinde tanımlanabilir. Inversion of Control (Kontrölü geliştiriciden Spring’e çevirme) yaklaşımı ile yazılım geliştiricilere büyük kolaylıklar sağlamaktadır. İlk kez 1988 Martin Fowler tarafından ortaya atılmıştır. Dependency Injection olarak yeniden tanımlanmıştır. Dependency Injection (Bağımlılık zerki) mekanizması tüm nesnelerin yönetimini kendi üstlenerek, nesneler arası bağlaşımı koparma (de-coupling) işlemini esnek bir şekilde karşılamaktadır.

### Inversion of Control Container ###

	Nesnelerin,
	- Hayat döngüsünü yönetir
	- Bağımlılıkları yönetir
	- Konfigürasyonunu sağlamak
	- Beraber bir bütün halinde çalışmasını sağlar
	- Tasarım kalıplarının kullanışını kolaylaştırır


### Neden Spring Framework? ###

Kendini ispatlamış ve kabul görmüş bir frameworktür. Hibernate ile kullanıldığında daha etkin performans göstermektedir. Inversion of Control güçlü yapısı springi güçlü kılmaktadır. Nesne tabanlı olduğu için kolay test edilebilir(OOP nin gücü). Spring Framework' ün avantajlarından biri ise uygulama sunucularına olan bağımlılığı ortadan kaldırmasıdır(GlassFish, JBoss, WebLogic gibi). Spring Framework ile geliştirilen projeler uygulama sunucularına bağımlılıkları olmadan, basit bir Servlet Konteynerda koşturulabilmektedir(Örneğin : Apache Tomcat, Jetty).

