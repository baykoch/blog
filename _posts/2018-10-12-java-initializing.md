---
title: "Java Değer Atama ve Başlatma Sırası"
last_modified_at:
categories:
  - java
tags:
  - java tanımlama cümleleri 
  - java ilk değer atama blokları 
  - java intilializing
  - java başlama sırası
toc: true
toc_sticky: true
toc_label: "Java Inıtializing"
author_profile: True
---

Bu yazımızda basit ve karmaşık değişkenlere ilk değer ataması nasıl yapılır inceleyelim.

- Tanımlama Cümleleri

- Metot çağrılar

   - Kurucu Metot Çağrısı

- İlk değer atama blokları (*Initialization Blocks*)

   -  Nense(*non-static*) Değişkenler
   -  Sınıf(*static*) Değişkenler

## Tanımlama Cümleleri (*Definition Statement*)

Tanım cümlesi değişkenlerin tanımlandığı yerde atama yapılmasıdır. Tanılama cümlelere tek bir ifadeden oluşabileceği gibi birleşik (*compound*) ifadenden oluşabilir. Sınıfın özellikleri (*state*) ([*üye değişkenleri*](https://baykoch.github.io/blog/java/java-object-create-attribute/#nesne-de%C4%9Fi%C5%9Fkenleri-object-variable)) tanımlama cümleleri ile atanabilir.

```java
public class InitializationDemo {
	// Nesne Değişkenleri
	int x = 4;
	InitializationDemo demo = new InitializationDemo();
	// Sınıf Değişkenleri
	static int id = 123213;

	public static void main(String[] args) {
		// Tanım Cümleleri ile ilk atama
		// Basit(ilkel) değişkenler
		double x = 2; // Basit ifade
		String str = "Hello";
		String y;
		y = ((Math.pow(x, 2)) <= x) ? "x Ondalık sayı" : "x tam sayı"; // Birleşik (Compound) ifade
		// Karmaşık(referans) değişkenler
		InitializationDemo p = new InitializationDemo();
		p.demo = null;
		p.x = 7;
	}
}
```

## Metot Çağrıları İle Değer Ataması

Metotlar ikiye ayırmıştır: Geriye değer döndüren ve değer döndürmeyen(*void*) Geriye değer döndüren metot çağrıları yaparak değişkenlere değer atanabilir.

```java
public class InitializationDemo {
	
	public static int  getPower(int x) {
		return x^x;
	}
	
	public static void main(String[] args) {
		// Metot Çağrısı ile değer atama
		int x=getPower(2); 	
	}
}
```

Nesne değişkenleri metot çağrısı ile atama yapılabilir. Aşağıdaki noktaları dikkat edilmesi gerekir.

- Nesne değişkeni için nesne metodu(*non-static*) sınıf değişkeni için sınıf metodu([static](https://baykoch.github.io/blog/java/java-static-keyword/)) kullanılmalıdır.

  ```java
  public class InitializationDemo {
  	// Nesne değişkeni
  	static int x=getPower(2); 
  	// Sınıf değişkeni
  	int y = new InitializationDemo().getAbs(4);
  	// Nesne metodu
  	public  int  getAbs(int x) {
  		return x^x;
  	}
  	// Sınıf metodu
  	public static int  getPower(int x) {
  		return x^x;
  	}
  }
  
  ```

- Üye değişkenleri(*nesne değişkenleri **+** sınıf değişkenleri*) ileri bir metottan veya değişkenden almak derleme hatasıdır.

  ```java
  public class InitializationDemo {
  	// İleri bir değer atama yapma
  	static int x = y;  // Hata! y henüz tanımlanmamış.
      // İleri bir metotdan atama yapma
  	static int y=getPower(z); // Hata! z henüz tanımlanmamış.
  	static int z = 2;
  
  	public static int  getPower(int x) {
  		return x^x;
  	}
  }
  ```

- Üye değişkenlerde metot çağrıları yapmak hatalı değildi fakat anlamsızdı çünkü olağan değerler([default](https://baykoch.github.io/blog/java/java-object-create-attribute/#nesne-olu%C5%9Fturmak)) geri döndürür.

  ```java
  public class InitializationDemo {
  	// İleri referans
  	static int x = getPow(); // y henüz tanımlanmadı. x = 0
  	static int y = 4;
  	
  	public static int  getPow() {
  		return y*y;
  	}
  	public static void main(String[] args) {
  		System.out.println(x); // x = 0
  		System.out.println(y); // y = 4
  	}
  }
  ```

### Kurucu Metot (*Constructor*) Çağrısı

[Kurucu metot]() ile değer atanabilir. Eğer üye değişkenleride sabit değişken([final](https://baykoch.github.io/blog/java/java-final-keyword/)) varsa bütün kurucu metotlarda [final](https://baykoch.github.io/blog/java/java-final-keyword/) değişkene ilk değeri kesinlikle atanmalıdır.

```java
public class InitializationDemo {
	 String name;
	 int age;
	 final int id;

	public InitializationDemo(String name, int age,int id) {
		this.name = name;
		this.age = age;
		this.id = id; // Final olduğu için atama yapmak zorunludur. 
	}
	public InitializationDemo(String name,int id) {
		this.name = name;
		this.id = id; // Final olduğu için atama yapmak zorunludur. 
	}

	public static void main(String[] args) {
		// Kurucu çağrısı ile değer atama
		InitializationDemo p = new InitializationDemo("M.K", 24, 01);
        InitializationDemo p2 = new InitializationDemo("Z.Y",02);
	}
}
```

## İlk değer atama blokları (Initialization Blocks)

İlk değer atama blokları genellikle sınıfların başlarında tanımlanır. Sınıf(*static*) ve nesne(*non-static*) değişken blokları olmak üzere ikiye ayrılır. İlk değer atama blokların kullanımla nedeni değişkenin ilk değeri bir takım işlemlerin- veritabanından veri çekmek gibi- sonucunda almasıdır. Diğer bir önemli neden ise eğer atanmak istenen değer **sıradışı bir durum** üretiyorsa istenmeyen bu durumu kontrol edebilmektir. 

- Nesne ilk değer atama blokları sınıftan üretilen *her nesne için çalıştırılırken* sınıf ilk değer atama blokları *sadece bir kez* çalıştırılır. 

- İlk değer atama blokları ileriye referans veremez ve geriye herhangi bir değer döndürmez. 

- Sınıf ve nesne değişkenleri ayrı ayrı tanımlanmalıdır. Sınıf değişkenleri için ilk değer atama blokları basında `static` anahtar kelimesi kullanılması **zorunludur**. 

  ```java
  public class InitializationDemo {
  	static int id;
  	static String country;
  	String name;
  	int age;
  
  	// Static değişkenler için statik blok kullanılır.
  	static {
  		id = 1;
  		country = "TR";
  	}
  	// Nesne değişkenler için normal blok kullanılır.
  	{
  		name = "M.";
  		age = 24;
  	}
  	
  	/* Static bloklarda nense değişkenleri kullanılamaz.
  	static {
  		id = 0;
  		age = 24; // Hata!
  	}
  	*/
  	public static void main(String[] args) {
  		InitializationDemo p = new InitializationDemo();
  		System.out.println("Name:" + p.name + " Age:" + p.age); // Name:M. Age:24
  		System.out.println("Country:" + country + " ID:" + id); // Country:TR ID:1
  	}
  }
  ```

- Sınıf değişkenlerini ilk değer blokları içinde yapılmalı ve kesinlikle kurucu metotlara bırakılmamalıdır. Çünkü nense hiçbir zaman üretilmez ise **kurucu metot asla çalışmayacaktır**.

- Süslü parantezler `{}`içinde dizinin ilk değerleri belirtilemez.

  ```java
  public class InitializationDemo {
  
      int [] digit = new int[10];
    	// Süslü parantezler {} içinde dizinin ilk değerleri belirtilemez.
      {
     	 // digit = {1,2,3,2,2,3,2,2,3}; // Hata!
     	}
      // Dizi hücrelerine atama yapılabilir.
      {
      	for (int i = 0; i < digit.length; i++) {
  			digit[i] = i;
  		}
      } 
      
      public static void main(String[] args) {
  		InitializationDemo p = new InitializationDemo();
  		for (int i : p.digit) {
  			System.out.println(i); // 1,2,3,4,5,6,7,8,9
  
  		}
  	}
  }
  ```

### Başlatma Sırası (*Initialization Order*)

Bir sınıf tasavvur edelim ki nesne ve sınıf değişkenleri; kurucu ve normal metotlardan oluşsun. Bu etkenler hangi sıra ile başlatılır veya çağrılır? 

Sırası üstten aşağıya olmak üzere:

   1. Statik değişkenler - karmaşık (*referans tipli*) ise onun alanları(*üye değişkenleri ve kurucular*) - çalıştırılır.
   2. Statik değer atama blokları (*initialization blocks*) çalıştırılır.
   3. Nesne değişkenleri çalıştırılır.
   4. Nesne(non-static) değer atama (*initialization blocks*) blokları çalıştırılır. Nesne değişkeni karmaşik tipli ise onun üye değişkenleri ve kurucu metotlar çalıştırılır. 

Not:
Nesne değişkeni sınıf (statik) değişkeninden üste sırada olsa bile her zaman sınıf değişkeni ilk çalıştırılır.
{: .notice--danger}

```java
public class FamilyTree {

	Father f = new Father();
	static GrandFather gf = new GrandFather();
	// statik değer atama bloğu
	static {
		System.out.println("Statik ilk değer atama bloğu");
	}
	// Normal (nesne değikenleri) değer atama bloğu
	{
		System.out.println("Normal ilk değer atama bloğu");
	}

	// Kurucu metot
	public FamilyTree() {
		System.out.println("FamilyTree kurucusu");
	}

	// Statik metot
	public static void staticMethod() {
		System.out.println("Statik metot");
	}

	public static void main(String[] args) {
		// FamilyTree family = new FamilyTree();
	}
}

class GrandFather {
	Father f = new Father();

	public GrandFather() {
		System.out.println("GrandFather kurucusu");
	}
}

class Father {
	Child c = new Child();

	public Father() {
		System.out.println("Father kurucusu");
	}
}

class Child {
	public Child() {
		System.out.println("Child kurucusu");
	}
}
```

Yukarıdaki kodu iki farklı açıdan inceleyelim. Eğer 25. satırdaki  nesne değişkenini çalıştırılmazsa sadece sınıf değişkenleri ve metotları çalıştırılacak:

1. `static GrandFather gf = new GrandFather();` satırı çalıştırılacak. 

   - `gf` karmaşık tip olduğu için üye değişkenleri çalıştırılacak. GrandFather sınıfında `f` nesne değişkeni, 
   - `f` sınıfın içinde ise `c` nesne değişkeni çalışacak. 
   - Değişkenler kalmadığı için `child` nesnesinin kurucusu çalışır. 
   - Daha sonra sırayla `Father` ve `GrandFather` kurucuları çalışır.

2. Statik değer atama bloğu(6-8 satır arası)  çalışır.

3. Statik metot üretilir ama çalıştırılmaz.


>Child kurucusu<br/>
>Father kurucusu<br/>
>GrandFather kurucusu<br/>
>Statik ilk değer atama bloğu

`FamilyTree family = new FamilyTree();` 25. satırdaki yorum işaretleri kaldırdığımızda: 

1. Yukarıdaki anlatıldığı gibi çalışır. Ve çıktılar aynı olur.

2. `Father fatherNesne = new Father();`  (nesne değişken) satırı çalışır.

   - Dikkat `fatherNesne` nesnenin üye `c` statik değişkeni ilk adımda üretildiği için tekrar üretilmeyecektir. 

   - `fatherNesne`’nin kurucu metodu çalıştırılır ve `fatherNesne` nesne üretme işlemi bitirilir.

3. Statik değer atama bloğu ve statik metot üretimi atlanır. (*ilk adımda gerçekleşir*)

4. Normal değer atama bloğu(10-12 satır arası) çalışır.

5. Üye değişkenleri ve değer atama blokları çalışıldığından `FamilyTree` kurucusu metodu çalışır.

>Child kurucusu<br/>
>Father kurucusu<br/>
>GrandFather kurucusu<br/>
>Statik ilk değer atama bloğu<br/>
>Father kurucusu<br/>
>Normal ilk değer atama bloğu<br/>
>FamilyTree kurucusu

