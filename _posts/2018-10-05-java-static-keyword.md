---
title: "Java Statik Anahtar Kelimesi"
last_modified_at:
categories:
  - java
tags:
  - java statik kullanımı
  - java static keyword
  - java statik metot
  - java statik değişken
toc: true
toc_sticky: true
toc_label: "Java Static"
author_profile: True
---

Sınıfların nesne değişkenleri aynı sınıftan üretilen nesnelerden bağımsız bir şekilde değiştirilebilir. Yani her nesnenin kendine has durumları vardır. Ama bazı durumlarda ise bir sınıfın özelliği(attribute) yada durumu(state) o sınıftan üretilen tüm nesneler için aynı olması istenebilir. Bu şekildeki nesne değişkenleri `static` anahtar kelime ile nitelendirilir. Bu gibi değişkenlere statik değişkenler(yada sınıf değişkenleri) denir.

- Statik değişkenleri nesne değişkeni değil sınıf değişkenidir.

- Nesne değişkenlerini aksine sadece bir tane kopyası vardır ve o sınıftan üretilen bütün nesneler için aynıdır. 

- Nesne değişkenlerine hem nesne üzerinde hemde sınıf üzerinden erişilebilir.

- Statik değişkenler nesne üretilmeden de ulaşılabilir.

- Statik(sınıf) değişkelerine benzer şekilde statik metotlarda tanımlanabilir. Yukarıda belirtilen statik değişkenlerin özellikleri geçerlidir. Dikkat edilirse main metot nesne üretilmeden kullanılabilen statik metoddur.

- Statik metotlar statik olmayan değişkenlere doğrudan(nesne üretmeksizin) ulaşamazlar.

  ```java
  public class StaticKeyword {
  	static String str;
  	static int x;
  
  	public static void staticMetod() {
  		str = str.concat("World");
  		x += 2;
  	}
  	public static void main(String[] args) {
  		// Statik değişkenlere sınıf üzerinde erişim.
  		System.out.println(StaticKeyword.str); // null
  		System.out.println(StaticKeyword.x); // 0
  
  		x++;
  		str = "Hello";
  
  		// Statik değişkenlere nesne üzerinden erişim önerilmez !
  		StaticKeyword nesne = new StaticKeyword();
  		// The static field StaticKeyword.str should be accessed in a static way
  		System.out.println(nesne.str); // Hello
  		System.out.println(nesne.x); // 1
  
  		// Statik değişkenlerin tek bir kopyası vardır.
  		nesne.x++; // 2
  
  		staticMetod(); // x = 4 ve str ="HelloWorld"
  
  		System.out.println(StaticKeyword.x); // x = 4
  		System.out.println(nesne.x); 		 // x = 4
  	}
  }
  ```



Uyarı: 
Statik değişkenlere sınıf üzerinde erişilmesi tavsiye edilir.
{: .notice--danger}

- Eğer bir metot sadece ve sadece statik değişkenler kullanıyorsa o metot statik yapılır.

- Nesneye merkezli olmayan dillerin tüm metotları statik yapıdadır. Statik metotlar nesne metotların aksine bir kez oluşturulduğu için çok fazla yer kaplamazlar. Buda progracıları statik metot tanımlamaya iterki böyle bir yaklaşım sakıncalı hatta işgüzarlıktır. Yani nesne çok fazla yer kaplıyorsa bunun nedeni tasarımsal problemler sonucunda gereksiz nesne üretilmesidir. *Yer açmak için amaç her zaman gereksiz nesnelerden kurtulmak olmalı, **statik yapmak değil!***

**Ne zaman statik yapılar kullanılmalı?**

Statik yapılar genellikle birden fazla nesne üretilmesi anlamsız olduğu hatta nesne üretilmesinin anlamsız olduğu durumlarda kullanılır. Matematiksel işlemler, ekran ifade yazdırma gibi örnekler verilebilir.

**Statik kullanmak bağımlılık yapar!**

Statik ifadeleri kullandıkça onunla ilişkili kodları statik yapmaya zorlar. Örnek olarak bir `x` değişkenine nesne oluşturmadan ulaşma çalışalım.

```java
public class StaticIsBad {
	// x değişkenin ilk hali
	// static int x = 2;

	// 2.adım: hatayı gidermek için x statik yapalım
	static int x = 2;

	// Metot ilk hali
	// public int add(int x) {
	// return x++;
	// }

	// 4.adım: Metoduda statik yaptık.
	public static int add(int x) {
		return x++;
	}

	public static void main(String[] args) {
		// 1. adım : x nesne üretmeden ulaşmaya çalışalım.
		System.out.println(x); // 1.adım :Hata 2.adım: hata giderildi.
		// 3.adım: add metotuda kullanmaya çalışalım.
		x = add(x); // 3.adım: Hata!
		// Hımm 4.adım: O zaman metoduda statik yapalım.
		// 5.adım : hata düzeldi.
	}
}
```

### Final ve Statik Değişken

Değişkenlere `Final` ve `static` anahtar kelimeler tanımlamak sınıf üzerinden değişme sabiler oluşturulmasını sağlar. (*Math.PI* sayısı gibi) Bu gibi değişkenler ayırt edilmesi için büyük harfle aralarında alttire `_` kullanmak suretiyle isimlendirilir.

```java
static final int NUMBER_OF_THE_STUDENTS = 100;
static final String ID_FILE = "TXT21";
```

