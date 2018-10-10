---
title: "Java Final Anahtar Kelimesi"
last_modified_at:
categories:
  - java
tags:
  - java final anahtar kelimesi
  - java final kullanım alanı
  - java final değişkenler
  - java final parametre
toc: true
toc_sticky: true
toc_label: "Java Final Keyword"
author_profile: True
---

`Final` anahtar kelimesinin 4 kullanım tipi vardır.

1. Değişkenlerin önlerine gelerek onları sabite (yani ilk atamadan sonra değiştirilemez) yapma.
2. Metotlara geçilen değerleri sabite (*Final*) yapma
3. (Soon)
4. (Soon)


### 1. Değişkenleri “*Final*” Yapma
`Final` anahtar kelimesi ile tanımlanmış bir basit değişkene ilk değer ataması yapıldıktan sonra değiştirilemez.

```java
final float pi = 3.14f;
pi = 3.145f;           //Hata The final local variable pi cannot be assigned
```
Karmaşik değişkenler(*nesne*) sabite olamazlar. Sadece onların özellikleri (*attributes or state or fields*) ve nesneye ulaşılmasını sağlayan referans değerleri sabite olabilir.
```java
public class Calculator {

	int x;
	int y;

	public static void main(String[] args) {
		final Calculator calc = new Calculator();
		// Final atanmış referans değeri değiştirilemez.
		calc = new Calculator(); // Hata!

		final Calculator calc2; // ilk değer ataması sonra yapılabilir.
		calc2 = new Calculator(); // ilk değer atama
		calc2 = new Calculator(); // Hata!
	}
}
```
`Final` ile belirtilmiş tipler ilk değer ataması (initialization) tanılanıdğı yerde yapılabildiği gibi kurucu metotlarda ve başlatma metotlarında ilk değer ataması yapılabilir. Nesne herhangi bir özelliği `final` sabite yapılmışsa kurucu metotlar da ilk değer ataması yapılmak zorundadır.

> Herhangi bir kurucuda (default kurucuda dahil) final tanımlanmış değişkenin ilk ataması yapılmadıysa **hata** verecektir.

```java
public class Calculator {
	
	final	int x;
			int y;
	
	// Hata! final x değişkeninin ilk değer ataması yapılmamış.
	public Calculator() {
	
	}
	// Hata! final x değişkeninin ilk değer ataması yapılmamış.
	public Calculator(int y) {
		this.y = y;
	}
	// x değerinin ilk değeri belirlendiği için bu kurucuda hata vermeyecektir.
	public Calculator(int x,int y) {
		this.x = x;
		this.y = y;
	}

	public static void main(String[] args) {
		final Calculator calc= new Calculator();
	}	
}
```

> **Final** yapılmış nesne artık değiştirilemez demek değildir. Referansı **Final** yapılmış nesnenin özellikleri (**attributes** or **state** or **fields**) değiştirilebilir. Sadece **Final** ile tanımlanmış nesne referansı artık başka nesne referansı gösteremez. (**null** dahil)

```java
public class Calculator {
	
	final	int x;
			int y;

	 // x değerinin ilk değeri atandığı için hata vermeyecektir.
	public Calculator(int x,int y) {
		this.x = x;
		this.y = y;
	}

	public static void main(String[] args) {
		
		final Calculator calc= new Calculator(2,3);
		calc.y = 7;	 // final nesne referansın özelliği değiştirebilir.
		calc.x = 10; // Hata! final yapılmış bir özellik değiştirilemez.
		// final nesne referansı  değiştirilemez.
		calc= new Calculator(8,9); // Hata!
		calc= null; // Hata! null dahi olmaz.
	}	

}

```

### 2. Metot Parametrelerini “*Final*” Yapma

Metot geçilen değerin değiştirilmesini istenmiyorsa parametre *final* yapılabilir. Parametreleri `final` yapma korumacı (*defensive*) programlamanın özelliklerin biridir.

```java
public class Parametre {
	// final yapılmış parametre değiştirilemez.
	public void finalParametre(final int x,final String str,final Parametre calc) {
		x = 5;  				// Hata!
		str = "Hello"; 			// Hata!
		calc = new Parametre(); // Hata!
	}

	public static void main(String[] args) {
		
		final Parametre pr= new Parametre();
		pr.finalParametre(2, "Merhaba",pr);
	}	
}
```

