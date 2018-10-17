---
title: "Javada Paket Yapısı ve Import Kavramı"
last_modified_at:
categories:
  - java
tags:
  - java import 
  - java sınıf ihraç etme 
  - java package kavramı
  - java paket nedir
  - java core paketler
toc: false
toc_sticky: true
toc_label: "Java"
author_profile: True
---

Öğrencilik yıllarımızda odalarımız her ne kadar  dağınık olsada aradığınız şeyi hemencecik bulduğumu anımsıyorum. Yani derler ya karmaşıklık kendi düzenini kurar ya da karışıklık içinde kendine göre bir düzen vardır. Maalesef yazılım dünyasında işler büyüdükçe, karmaşıklık arttıkça işler bu kadar basite indirgenemez. Bir noktadan sonra her şey kategorize edilmeye mecburdur.

- Javada sınıflar, arayüzler ve enum dosyaları  mantıksal açısından kategorize edilmelidir. Ayrıca kategoriler arasına erişim belirleyici koymak zorundayız.

- Paketler `package name` şeklinde belirtilir.

- Her sınıfın ilk başına (yani en üstüne) koyulur.

- Sınıf arayüzün dışında tanımlanır. Çünkü sınıf bir pakete aittir -sınıfın bir özelliği değildir- ve her sınıf sadece bir pakette bulunabilir. Fakat bir pakette arzulandığı kadar sınıf tanımlanabilir. 

- Pek önerilmesede bir sınıf dosyasında birçok sınıf tanımlanabilir. Bu gibi sınıflar dosyanın en üstünde tanımamış pakete  dahildir.

- Paket isimleri aralarında nokta kullanılarak hiyerarşi yapısı oluşturulabilir. Her bir hiyerarşi işletim sisteminde bir klasöre denk gelir. Sınıf `package` isim ile belirtilen(yada ait olduğu) hiyerarşi klasöründe bulunur.

- Aynı fonksiyona ve amaca sahip sınıflar aynı pakette olurlar. Veri katmanı (*dao*) veya arayüz (*gui*) katmanı örnek verilebilir.

- Paketlerin diğer oluşturulma nedeni ise çakışmalardan kaçınmaktır. Aynı isme sahip fakat farklı fonksiyonları yerine getiren sınıfları ayırmaktır. Bu sınıflar aynı projede olabileceği gibi birbiri ile haberleşen farklı projede de olabilir. Yada `import` kelimesi ile projeye eklenen bir kütüphane (yada modül) olabilir. **Paketlerde muhtemel çakışmaları önlemek için geliştirici kişi veya firmanın internet  domain adresi tersinde başlayarak isimlendirme yapması önerilir**( `com.google.docs....` ). Çünkü domain isimleri **tek ve eşsizdir**.

- Javada `java.*` ile `javax.*` ile başlayan paketler tanımlanamaz. Eğer tanımlanırsa çalışma zamanında değil derleme zamanında hata verecektir. 

  ```java
  package java.not.allowed; // java ile başlayan paket ismi 
  
  public class Test {
  
  	public static void main(String[] args) {
  		System.out.println("java* ve javax* ile başlayan paket ismi olamaz.");
  	}
  }
  ```

  > Error: A JNI error has occurred, please check your installation and try again <br/>
  > Exception in thread "main" java.lang.SecurityException: Prohibited package name: java.not.allowed

- Aynı paketteki sınıflar birilerine erişim belirleyiciler izin verdiği sürece (protected, default, public) doğrudan erişebilir. Farkı pakettekiler birlebirlin erişmek için açık adresi yazılmalıdır. Sınıfın açık adresi uzun ise bu durum işkenceye dönüşür. Aşağı kodda bu yöntemin ne kadar zahmetli olduğu görülüyor.

  `package io.github.baykoch.javase;` paketinde `Person` sınıfı

  ```java
  package io.github.baykoch.javase;
  
  public class Person {
  	
  	 String name;
  	 int age;
  }
  ```

  `package io.github.baykoch.test;` paketinde `TestDemo` sınıfında  `Person`  sınıfını kullanalım.

  ```java
  package io.github.baykoch.test;
  
  public class TestDemo {
  
  	public static void main(String[] args) {
          // Başka paketteki sınıf kullanmak için açık adresi yazılmalı.
  		io.github.baykoch.javase.Person person = new Person();
  	}
  }
  ```

- Bu gibi istenmeyen durumdan kaçınmak için `import` kelimesi ile ilgili sınıf ihraç edilir.

-  `import` kelimeleri `package` cümlelerinden sonra, sınıf arayüzünden önce -yani dışında- olmalıdır. `import` edilen sınıf veya sınıflar sade isimleri ile kullanılabilirler.

- `import` kelimeleri birden fazla olabilir (yada birçok sınıf ihraç edilebilir).`*` ile ilgili paketin tamamı -**Dikkat**! *alt paketler dahil değildir.*- ihraç edilebilir. 

- `*` ile tüm sınıfları ihraç etmek yazılımı asla yavaşlatmaz çünkü Java sadece kullandığı sınıfları kaynak dosyasına ekler.

  ```java
  package io.github.baykoch.test; // import her zaman  package sonra konulur.
  // Sınıflar tek tek ihraç edilebildiği gibi bütün sınıflar '*' ile ihraç edilebilir.
  import java.util.Date;  
  import java.util.Random;
  
  // import java.util.*; 
  
  public class Calculator {
  
  	public static void main(String[] args) {
  		
  		Random r = new Random();
  		Date time = new Date(); 
  	}
  }
  ```

- `Import` etmek aslında Javaya dosyanın yolunu göstermektir. Kısmet olursa *Java* komutları  üzerine(`classpath` gibi) detaylı bir yazı çalışması yapacağım (*on Linux*). 

### Java Çekirdek Paketler (*Java Core or Pre-Defined Packages*)

Java standart sürümde kullanıcıları sunulan paketlerdir. Bu paketler ancak `import` kelimesi ile ihraç edilerek kullanılır. En temel paket olan `java.lang` `import` edilmesine gerek yoktur.

- **java.lang**: Temel dilin işlevselliği ve veri tipleri (Class, Object, String, Thread)    
- **java.util**: Torba veri yapıları (LinkedList, Map, HashTable, Date, Calendar...)
- **java.io**: Dosya işlemleri 
- **java.math**: Sayısal işlemler (exponential, logarithm, square root,trigonometric functions ...)
- **java.nio**: Yeni (new i/o) Non-blocking I/O framework yapısı.
- **java.net**: Ağ operasyonları (soket,dns...)
- **java.security**: Güvenlik (anahtar üretme, şifreleme, çözme) yapıları
- **java.sql**: Veritabanı işlemleri(JDBC) Java SE 9 sürümü ile  kaldırıldı ve ayrı dağıtılıyor.
- **java.awt**: Grafiksel kullanıcı arayüzü (GUI) bileşenleri
- **java.text**: Konuşma dilleri için metin, sayılar ve mesajlar sağlar.
- **java.rmi**: Uzak Metod Çağrısı( RMI ). Başka makinede çalışan metodu çağırma 
- **java.time**: Zaman, süre kavramları ile alakalı sınıflar