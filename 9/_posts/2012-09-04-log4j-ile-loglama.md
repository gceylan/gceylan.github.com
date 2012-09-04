---
layout: post
title: log4j ile loglama
---

### Loglama nedir? ###

Loglama son kullanıcılar ve sistem yöneticileri için, uygulamanın devamlılığı
açısından çok önemlidir. Herhangi bir projede karşılaşılan hataları, performans
sıkıntılarını ve bugları anlık olarak yakalayıp düzeltmek için kullanılır.

### Log4j nedir? ###

Log4j `Apache' nin` geliştirmiş olduğu bir loglama frameworküdür. Log4j kullanabilmek 
için _**[log4j.jar](http://logging.apache.org/log4j/2.x/download.html)**_ ve _**[log4j.properties](https://raw.github.com/gceylan/pro-lang/master/java/SimpleLog4jexample/src/log4j.properties)**_ config dosyasını indirip projemize dahil etmeliyiz.

Log4j ile farklı seviyelerde loglama yapabiliriz.

![1](https://raw.github.com/gceylan/gceylan.github.com/c63a6e8c7a9beb27775310846393a9fb0c1cf331/images/severity-levels-logging.png)

Şekilde de görüldüğü gibi merkeze doğru logun kapsama alanı azalır.

### log4j.properties dosyası ###

Bu dosya log4j nin config dosyasıdır.

### Örnek log4j.properties config dosyası: ###

<pre><code class="config">
# logger options: ALL -> DEBUG -> INFO -> WARN -> ERROR -> FATAL -> OFF

# Root logger option
log4j.rootLogger=INFO, file, stdout

# Direct log messages to a log file
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=log/loging.log
log4j.appender.file.MaxFileSize=1MB
log4j.appender.file.MaxBackupIndex=1
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

# Direct log messages to stdout
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n
</code></pre>

Bu dosyayı java projesinde `src` dizininin altına koymalıyız.

Şu anda bu dosya log mesajlarını _**sistem konsoluna**_ ve _**log/loging.log**_ isimli bir dosyaya yazmak üzere ayarlanmıştır. Bu dosyanın boyutu 1 MB ulaştığında otomatik olarak 2. log dosyası açılacaktır. `log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n` satırı ile tarih, saat, logun oluştuğu satır gibi bilgilerin de loga eklenmesini sağlamaktadır.

`log4j.rootLogger` ayarı **OFF** yapılarak loglama iptal edilebilir ya da **ALL** yapılarak tüm tüm seviyelerdeki loglar izlenebilir.

**Basit bir java programı ve log4j:**
<pre><code class="java">
package com.gceylan.log4jexample;

import org.apache.log4j.Logger;

public class Log4jExample {

	private static final Logger logger = Logger.getLogger(Log4jExample.class);
	
	public static void main(String[] args) {
		
		logger.info("STARTED!");
		
		logger.trace("Trace");
		logger.debug("Debug");
		logger.info("Info");
		logger.warn("Warn");
		logger.error("Error");
		logger.fatal("Fatal");
		
		logger.info("FINISHED!");
	}

}
</code></pre>

**Diğer Faydaları:** Örneğin, kod çerisinde bulunan `system.out.println` leri kaldırmak için koda müdehale etmek gerekir. `Sysout` sistem kaynaklarını kullanarak sistem log dosyasına yazar. Her yazım işleminde `I/O` yapar. log4j kadar performanslı değildir. İstenildiği zaman kapatılamaz.
