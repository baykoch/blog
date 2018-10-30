---
title: "Java Çok Şekillilik (Polymorphism)"
last_modified_at:
categories:
  - java
tags:
  - java binding  
  - java upcasting 
  - java downcasting
  - java çok şekillilik
  - java polymorphism	
toc: true
toc_sticky: true
toc_label: "Java Polymorphism"
author_profile: True
---

Çok şekillilik bir sınıfı birden fazla şekilde parametre veya cevap verecek şekilde kodlamasıdır. Yani bir sınıf farklı zamanlarda kendi veya alt tipleri (sub-class) göstermesidir. Miras(inheritance) ile çok şekillilik(polymorphism) iç içe geçmiştir. Overriding ve overloading çok şekliliğin bir parçasıdır. Bu konulardan [bahsedildi](https://baykoch.github.io/blog/java/java-inheritance/). Bu bölümden upcasting ve downcasting bahsedilecektir.

`Upcasting` konusuna geçmeden önce Java bağlam(***binding***) konusuna bir bakış atalım.

Değişkenlere bulunduğu bellek alanı ve bu bellek alanına yani değişkenlere ulaşmayı sağlayan göstericiler(*Java’da referans olarak bilinir*) bulunur. Değişkenleri ve göstericilerin birbirine bağlanmasına binding denir. İki tür bağlama türü (binding) vardır.

1. Statik Bağlama (*Static Binding*)

2. Dinamik Bağlama (*Dynamic Binding*)

***Statik bağlama*** ilkel tipleri üzerinde yapılan bağlamdır. Değişken tanımladığı an/yerde bağlama yapılır. Pratikte statik değişkenlerin tanımlandığı gibi bellek bölgesine ve bellek bölgesine ulaşmayı sağlayan göstericiye sahip olurlar.

Karmaşık(sınıf) tipindeki değişkenler işe **dinamik bağlama** mekanizması sahiptir. ***Java karmaşık tipli değişkenlere  `reflection` yöntemi kim olduğunu sorar aldığı cevaba göre derleme zamanında (compiled time) bağlama yapar***. Yani Java herhangi bir değişkenin hangi türde olduğunu çalışma zamanında bilemez.

### Yukarı(*upcasting*) Ve Aşağı(*downcasting*) Çevrim

`upcasting` miras hiyerarşisinde bulunan bir sınıfın bir üste sınıfa(ebeveyn) çevrilmesidir.(yada cast edilmesidir.)  Java upcating yapraken dinamik bağlamadan yaralanır. Bu çevrim şekli tamamen güvenli olup çevirim (*cast*) yapılacak tipin belirtilmesine gerek yoktur. 

```java
public class Usta extends Kalfa{
	
	public static void main(String[] args) {
		// Upcast yerine geçebilme özelliği sebebiyle her zaman güvenlidir.
		// Çırak, kalfa veya usta aynı zamanda bir işçidir.
		İşçi p = new İşçi();
		// Upcast örnekleri
		İşçi çırak = new Çırak();
		İşçi kalfa = new Kalfa();
		İşçi usta = new Usta();
		
	}
}

class Kalfa extends Çırak{}

class Çırak extends İşçi{}

class İşçi {}
```

Yerine geçebilme özelliğine göre bir çırak, kalfa veya usta aynı zamanda işçidir.

`Upcasting`, daha az kod yazarak daha çok iş yapabilmeye olanak sağlar. Bir yakıt istasyonun tankeri hangi tür arabanın geldiğine bakmaksızın yakıt ikmali yapar. Düşünelim eğer her taşıt çeşiti için tanker yapılsaydı? Benzer şekilde işçiler için yemek kayıtlarını tutan bir metot düşünelim, yerine geçebilme sayesinde herhangi bir işçi, çırak, kalfa  veya usta farketmeksizin bu davranışı yerine getirir. Aksi halde her işçi türü için yeni metotlar yazmak zorundaydık.

- Çok şekililik referaslar üzerinden yapılır.
- Ancak miras hiyerarşi içerisinde bulunan tipler arasında *upcasting*  yapılabilir.

- Miras hiyerarşisinde en üstte genel sınıf (örnekte İşçi sınıfı) göre kod yazılmalı çocuk sınıflardaki gerekleştirmeleri (*implementation*) göz önüne alma.

- Bağımlılığı azaltır. Örneğimizde Çırak sınıfın koddan çıkarılması yemek bölümünde veya diğer sınıflarda hiçbir değişikliğe neden olmayacaktır.

- Genel ebeveyn sınıf arayüzünü göre tasarım yapmak çocukların arayüzlerinde bağımsız kod yazabilmeyi sağlar. ***Yani yazılımda asli olan  kod gecekleşitme(implementation) değil arayüz tasarımıdır***. İşçi sınıf arayüzleri ne kadar mükemmel tasarlanmış ise  program bir o kadar iyidir.

> Bir işyerindeki yemek bölümünü ele alalım. Yemek bölümü hangi tür işçi tipinin olduğuna bakmaksızın yemek servis yapmasını sağlayalım. Upcasting yaparak her işçi sınıfı için yeniden metot yazmaya gerek kalmadan kodlayalım. Unutmayalım az kod çok iş. Diğer ayrıntı Usta sınıfın sınırsız yeme hakkına sahip olmasıdır.

```java
public class Usta extends Kalfa {
	
	public Usta(String name, int age, int lunchTimes) {
		super(name, age, lunchTimes);

	}
	// Usta sınıfı sınırsız yemek hakkına sahip.
	@Override
	protected boolean mealTracker() {
		return true;
	}
    protected void calculateFrom() {
		System.out.println("Kalıp hesaplandı.");
	}

}
//Kalfa Sınıfı
class Kalfa extends Çırak {

	public Kalfa(String name, int age, int lunchTimes) {
		super(name, age, lunchTimes);
	}
}
//Çırak Sınıfı
class Çırak extends İşçi {

	public Çırak(String name, int age, int lunchTimes) {
		super(name, age, lunchTimes);
	}
}
// İşçi Sınıfı
class İşçi {

	protected String name;
	protected int age;
	protected int lunchTimes; // Kalan yemek sayısı

	public İşçi(String name, int age, int lunchTimes) {
		super();
		this.name = name;
		this.age = age;
		this.lunchTimes = lunchTimes;
	}
	// Yemek sayını kontrol eden metot.
	protected boolean mealTracker() {
		boolean b = false;

		if (lunchTimes > 0) {
			lunchTimes--;
			b = true;
		}
		return b;
	}
}
```

Şimdi `upcasting` kullanarak yemek servisi yapalım.

```java
public class FoodCourt {

	protected void luchTime(İşçi p) {
		
		if (p.mealTracker() == true) {
			System.out.println("Afiyet olsun.");
		} else {
			System.out.println("Sayın "+p.name+", lütfen yemek kartınızı doldurunuz.");
		}
	}

	public static void main(String[] args) {
		
		FoodCourt serve = new FoodCourt();
		// Upcasting
		İşçi p = new Çırak("Ali", 21, 30);
		İşçi p2 = new Kalfa("Veli", 45, 0);
		İşçi p3 = new Usta("Zelda", 32, -1);
		
		// Çok şekelilik: az kod çok iş
		serve.luchTime(p); // Çırak 
		serve.luchTime(p2); // Kalfa
		serve.luchTime(p3); // Usta sınırsız yemek hakkına sahip.
	}

}
```

- ***Metotlarda çok şekillidir***. Örneğimizde dikkatli incelenirse `serve()` metodunda ***p*** `işçi` sınıfına ait olmasına rağmen `usta` sınıfının `mealTracker()` metodunu kullandı. Normalde hangi metodu  çağıranı referans tipe(*işçi*) göre belirlenir. Fakat çalışma zamanında hangi metodun çağrıldığı referans tipin değil referansın tipin gösterdiği nesnenin tipine göre belirlenir.

- ***Dinamik bağlama üye değişkenleri; static,private ve final metotlar için geçerli değildir. Çünkü static, private ve final metotlar overloading edilemezler.***
- **Polymorphism** diğer bir anlamı bilmemektir. Örneğimizde `serve()` metodu parametre aldığı işçi sınıfların hangi türde olduğunu bilmiyor. Ama mükemmel bir şekilde hangi türde ise o türün davranışlarını yerine getiriyor. Bizde bilemeyiz veya bilmemeliyiz. Aslında kullandığınız bir çok modül veya kütüphanelerde bu durum boylerdir. String veya println metotların içeriğini biliyor muyuz? Elbette, hayır. 

`İşçi p3 = new Usta("Zelda", 32, -1);`  ifadesine göre;

Derleme zamanında `p3` gerçek(*nesne*) tipine bağlandığı için `Usta` sınıfınnın ezdiği (overriding)  metrolara ulaşır.  Fakat çalışma zamanında referans tipine göre belirlendiği için alt-sınıfların özel metotlarına ulaşılamaz. Bu durumda `Usta` sınıfın `calculateFrom()` gibi özel metodunu ulaşamayız.

`Downcasting` bu gibi durumlarda gerçek tipe geri dönmek için kullanılır.

- Ancak miras hiyerarşi içerisinde bulunan tipler arasında *downcasting* yapılabilir.

- `Downcasting` güvenli değildir. Cast `()` işareti ile belirtilmek zorundadır. Fakat `downcasting` yapılacak tip bilinemez durumda olduğu varsayımı üzerine (***Java herhangi bir değişkenin hangi türde olduğunu çalışma zamanında bilemez***) `instanceof` kullanılmak zorundadır. Aksi halde `ClassCastException` hatası verecektir.

```java
public class Usta extends İşçi {
	public Usta(String name, int age) {
		super(name, age);
	}
	@Override
	protected void startWork() {
		System.out.println("Usta çalışmaya başladı.");
	}
	protected void calculateFrom() {
		System.out.println("Kalıp hesaplandı.");
	}
	public static void main(String[] args) {
		İşçi p = new Usta("Ali", 45);
		p.startWork();
		// Çalışma zamında p işçi sınıfı gibi davrandığında için Usta sınıfının
		// calculateFrom metoduna ulaşılamaz.
		// p.calculateFrom(); // Hata !
		// Bu durumda downcasting ile gerçek tipe geri dönülmelidir.
		Usta realtype = (Usta) p; // Aykırı/Sakıncalı kullanım.
		// Fakat polymorphism mantığına göre p her zaman hardcode yazıldığı gibi usta
		// olmayabilir. Böyle durumlardan kaçınmak için instanceof kullanılmak
		// zorundadır.
		// Aksı halde ClassCastException hatası verecektir.
		if (p instanceof Usta) {
			realtype = (Usta) p;
		}
		// Artık gerçek tipe dönüldüğünden Usta sınıfın özel metotlarına ulaşılabilir.
		realtype.calculateFrom();
	}
}
// İşçi Sınıfı
class İşçi {
	protected String name;
	protected int age;

	public İşçi(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	protected void startWork() {
		System.out.println("İşçi çalışmaya başladı.");
	}
}
```



