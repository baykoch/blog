---
title: "Java "
last_modified_at:
categories:
  - genel
tags:
  - java
  - java
  - java
  - java
toc: true
toc_sticky: true
toc_label: "Java "
author_profile: True
---

Bu dersimiz çok sık kullanılan fakat hakkında çoğu yazılımcının az bilgiye sahip olduğu String tiplerinde bahsedeceğiz. En başta String  ilkel yani basit tip değildir. Hata C programlama dilinde string diye bir değişken olmadığını farketmişsinizdir. 

String karakter dizilerinde oluşur. Dizi gibi davranırlar. Javada ise String bir sınıftır. Final anahtar belitriçine sahiptir ve miras alınmaz.

SJavada String iki faklı biçimde kullnılabilir. 

- Kurucu çağrısı yapılarak: Yeni nense üretir

```java
String  str = new String("Merhaba"); // Kurucu çağrısı String nensesi ile üretme
```

- Atama operatörü ve çift tırnakarlar  kullanılarak: Yeni nesne üretilmez.

```java
String str = "Merhaba"; // String nesnesi üretilmez.
```

Java bellek daha optimal yönetmelik  çift tırnak string tanımlanmasında String havuzunda metin değeri var ise  yeni nesne üretmez havuzunda bulunan değerin referansını döndürür. 

```java
String str = "Merhaba";  // Nesne üretildi.
String str2 = "Merhaba"; // Nesne üretilmedi.
System.out.println(str == str2);  // True

String strWithObject = new String("Merhaba");  // Nesne üretildi.
String strWithObject2 = new String("Merhaba"); // Nesne üretildi.
System.out.println(strWithObject == strWithObject2); // False
```

String değişkenleri eğer havuzdaki aynı nesneleri gösteriyorsa, herhangi biri üzerinde yapılan değişiklik diğer değişkenlerin etkilediğini düşünebiliriz. Haklısınızda, fakat String değişmez (immutable) tiplerdir. String üzerinde yapılan her değişiklik yeni değişkneleri üretilmesine sebep olur. 

String sınıf üzerinde manipulasyon yapan (concat, replace ...) onlarca metotlar vardır. Bu metotlar her işlemede yeni string üretir. Buda tabi olarak JGC çok fazla çalışmasına, performans düşmesine yol acar.

```java
public class StringDemo {
    
	public static void main(String[] args) {
		String str = "Merhaba";
		String str2 = "Dünya";
		String  strInPool = "MerhabaDünya";
		str = str + str2; // Yeni nesne üretilir.
		
		// Manipulasyon yapıldığı için yeni değer üretildi. Referansları eşit değil.
		System.out.println((strInPool == str)); 	// false
		// Veri değerleri eşit.
		System.out.println(strInPool.equals(str)); // True
		// Yeni nense üretilmez havuzda buluna değere referas eder.
		String strFromPool = "MerhabaDünya"; 
		// Huvuzda biriktiği için hem değerleri hemde referasları eşit.
		System.out.println((strInPool == strFromPool));   // True	
	}
}
```

Metinler üzerinde çalışıldığında;

- Ufak tefek işlemlerde kullan-at mantığında String metotları kullanılabilir.
- Eğer veriler büyükse asla String metotlarını kullanılmamlıdır. Örneğin metin dosyasında veriler okunup ekleme değiştirme gibi işlemleri String metotları üzerinde yapma.

- Diğer bir önemli nokta ise  String nesneleri çoğu zaman havuzunda birikmesi için çift tırnak ile üretilmelidir. 