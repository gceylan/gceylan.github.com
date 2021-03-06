---
layout: post
title: configuration dosyaları ve java properties oluşturma
---

Konfigürasyon dosyaları, sonradan düzenlenebilir çeşitli ayar verilerine ve pek
değişmeyeceği düşünülen ayar verilerine sonradan kolayca erişebilip kod üzerinde
oynamaksızın programın işleyişini değiştirmek amacıyla kullanabileceğimiz dosya
yapılarıdır.

Ör: Derlenmiş bir projede config dosyaları sayesinde veritabanı adı, tablo 
adları gibi bilgiler değiştirilerek verilerin kaydedildiği yerler
kolayca değiştirilebilr. Böyle bir durumda kaynak kodlar üzerinde değişme
yapılmaz ve kaynak kod tekrar derlenmek zorunda kalmaz.

Java' da config dosyaları `java.util.Properties` sınıfı kullanılarak hazırlanır.

**Örnek Java Config dosyası hazırlama**

<pre><code class="java">

package com.gceylan.simleconfigfileexample;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.util.Properties;

public class Config {

	private String database;
	private String dbUser;
	private String dbPassword;
	private String filePath;

	Properties prop;

	public Config() {
		filePath = "config/config.properties";
		prop = new Properties();
	}

	public void addConfigFile() {

		try {
			// config dosyasında tutulması istenilen özellikler set ediliyor
			prop.setProperty("database", getDatabase());
			prop.setProperty("dbUser", getDbUser());
			prop.setProperty("dbPassword", getDbPassword());

			// bilgiler config.properties dosyasına kaydediliyor
			prop.store(new FileOutputStream(filePath), null);

		} catch (FileNotFoundException fileNotFoundEx) {
			fileNotFoundEx.printStackTrace();
		} catch (IOException ioEx) {
			ioEx.printStackTrace();
		}
	}

	public void printConfig() {
		
		try {
			// config.properties dosyası açılıyor
			prop.load(new FileInputStream(filePath));

			// property değeri ekrana basılıyor
			System.out.println(prop.getProperty("database"));
			System.out.println(prop.getProperty("dbUser"));
			System.out.println(prop.getProperty("dbPassword"));

		} catch (IOException ioEx) {
			ioEx.printStackTrace();
		}
	}

	public static void main(String[] args) {
		Config c = new Config();
		c.setDatabase("localhost");
		c.setDbUser("gceylan");
		c.setDbPassword("123456");

		// config.properties dosyasına kaydedildi
		c.addConfigFile();

		// config dosyasındaki ayarlar ekrana basıldı
		c.printConfig();

	}

	public String getDatabase() {
		return database;
	}

	public void setDatabase(String database) {
		this.database = database;
	}

	public String getDbPassword() {
		return dbPassword;
	}

	public void setDbPassword(String dbPassword) {
		this.dbPassword = dbPassword;
	}

	public String getDbUser() {
		return dbUser;
	}

	public void setDbUser(String dbUser) {
		this.dbUser = dbUser;
	}

}
</code></pre>
	
**Not:**Yukarıdaki örneğin [kaynak kodları](https://github.com/gceylan/pro-lang/tree/master/java/SimpleConfigFileExample)na linkten ulaşabilirsiniz.
