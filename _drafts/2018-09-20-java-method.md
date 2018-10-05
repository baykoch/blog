---
title: "Java Metot Kavramı "
last_modified_at:
categories:
  - java
tags:
  - java  
  - java  
  - java 
  - java 
toc: true
toc_label: "Java "
author_profile: True
---

Metotlar nesnelerin davranışlarını yerine getiren fonksiyonlardır. Metotlar ancak sınıfın içerisinde tanımlanabilir. Aynı sınıftan üretilen nesneler o sınıfta tanımlanan her metodu yerine getirir. 

Metotlar oluşturulurken dikkat edilmesi gereken noktalar:

- Tanımlandığı sınıfın alanını ilgilendiren davranış yerine getirmelidir. Daire sınıfında alan metodu karenin alanına hesaplamamalı.
- Metotlar sadece ve sadece bir davranışı gerçekleştirmeye odaklanmalı. Daire sınıfı içinde hem alan hemde çevresini hesaplayan  metot  yazılmamalı
- Karmaşıklığı önlemek için satır sayısı az olmalı eğer fazla satır kod yazmak gerekiyorsa yeni motorlar oluşturulmalı.
- Motorların isimleri yerine getirdiği davranış ile ilişkili kısaltma kullanılır. Emir kipinde, uzun ve açık halinde koyulmalı. Java metot sınıf simine uzunluğu sınırlama yoktur.

Bir metodun söz dizimini altı parçadan oluşur.

```java
<erişim niteleyici>  <geri dönüş tipi> <metod ismi> ( <parametreler> ) {

    <kod bloğu>

	return <geri dönüş değeri> 
}
```



### Metod ismi (name) 

 Metodun davranışı ile ilişkili, anlamlı emir kipinde bir isim olmalı. 

### Geri Dönüş Tipi  (*Return Type*)

 Metot davranışı çağrıldı noktaya bir değer dönderekçe ise bu değerin tipi, eğer bir değer döndürmeyecekse `void` kullanılır.

### Parametre (*Parametre*) 

Metod çağrıldığı yerden geçilen parametreler. Parametre geçilmesi zorunlu değil. Parametreler basit ve karmış tiplerde olabilir. Javada doğası gereği basit tip değeri `null` geçilemez. Aksine karmaşık tiplerde `null` geçilebilir. 

Metotların çağrıldığı yerden geçilen parametre **gerçek parametre**(*actual parameter*), metroda tanımlanmış parametrelere ise **formal parametre**(*formal parameter*) denir. Gerçek ve formal parametreler uyumlu olmalıdır. Veri tipleri konusunda detaylı şekilde [bahsettiğiniz](https://baykoch.github.io/blog/java/java-veri-tipleri/) otomatik yükselte yapılmıyorsa `cast` yapmak zorundayız.

```java
public class Methods {

	public static void main(String[] args) {
		
		short y = 12;
		double z = 2.13;
		
		Person person = new Person();   
		System.out.println(person); // null
		
		// short değerini int değerine otomatik yükseltme yaptı.
		// int değerini byte değerine cast yapmak zorunda.
		// double değerini int değerine  cast yapmak zorunda.
		int result = calculete((byte)25, y, (int)z, person); // person  değeri null olabilir.
		                                            // diğer tipler basit olduğunda null olamaz.
	}

	public static int calculete(byte x, int y, int z, Person person) {  

		return x + y + z;
	}

}
```



### Kod Bloğu (*Code Implementation*) 

Metot davranışını yerine getiren kısım. Davranışlardan dört farklı eylemi icara etmesini beklenir.

1. Durumunun hakkında bilgi ver.  Örnek :`Get... metodları`
2. Durumunu değiştir.  Örnek :`Set... metodları`
3. Bir faaliyeti yerine getir. Örnek :`calculateField()`.
4. Son olarak istenileni bir başka nesneye havale eder. Havale edilen nesne yukarıdaki bahsedilen 3 özelliği yerine getirir. (*Delegation*)



### Geri Dönüş Değeri (*Return Value*) 

Geri dönüş tipine göre, metod davranışı sonucu istenilen mesajdir. Geri dönüş tipi `void` ise yazılmayabilir veya yazılıp boş geçilebilir. (`return;`). Herhangi bir geri dönüş tipine sahip metod çağrıldığında geri dönüş değeri tutulmuyorsa buna yan etki `side effect` denir.

```java
public class Methods {

	public static void main(String[] args) {
		// Yan etki(Side effect) metot çağrısı.
   		calFunc(25, 25 ,25);
	}

	public static int calculete(int x, int y, int z) {
		return x + y + z;
	}
}
```

### Erişim Niteleyici (*Access Modifier*) 

### İmza (*Signature*) ve Arayüz (*Interface*)

Bir metodun isim ve parametrelerin toplamına -Geri dönüş değeri dahil değildir.- metodun imzası (Signature) denir.

Javada arayüz iki farklı anlam çağrıştırır.

1. Sınıfın veya nesnenin davranışlarının hepsi arayüz olarak bilinir.
2. Bir metodun isim parametreleri ve dönüş değeri hepsine arayüz denir.

Bu konuda ikinci anlamında bahsediyoruz. Bir metodun çağrılması için arayüzü bilmelidir.Ayrıca bir sınıfta aynı arayüz veya imzaya sahip metot kesinlikle bulunmaz. 

#### Metotlarda  yeniden tanımlama (*Overloading*)

Daha önce `overloading` yeniden tanımlama operatör konusunda  bahsetmiştik. Benzer şekilde metotların `overloading` halleri olabilir. Bir metot aynı isimle farklı parametre tipleri ile `overload` olurlar. Mesela `System.out.println()` metodun en az 10 tane farklı hali vardı.

{% include figure image_path="/assets/images/java-sysout.png" alt="sysout" caption=""%}

Örnekte `print` metodu girilen parametreye göre ilgili metodu çalıştıracaktır.

```java
public class OverloadMethod {

	public static void main(String[] args) {
		// Aynı isimli metodun oveloading olması
		print(123.4);   // double
		print("Hello"); // String
		print(25);		// int
	}

	public static void print(String x) {
		System.out.println(x);
	}

	public static void print(int x) {
		System.out.println(x);
	}

	public static void print(double x) {
		System.out.println(x);
	}

}
```

İmazası aynı fakat dönüş değerleri farklı olan metotlar yeniden tanımlama (*overloading*) yapılamaz. Çünkü olası bir yan etki (*side effect*) çağrısında JVM hangi metodu çağıracağını bilemez.

```java
public class Methods {

	public static void main(String[] args) {
		// Yan etki(Side effect) metot çağrısı.
        calculete(25, 25, 25); // JVM hangi metodu çağıracak ? Bilemez.
	}
	
	public static int calculete(int x, int y, int z) {     // Hata !
		return x + y + z;
	}
	
	public static double calculete(int x, int y, int z) {  // Hata !
		return x + y + z;
	}

}
```
Basit veri tiplerinde bilmesi gereken diğer nokta ise otomatik yükselte gereken çağrılarda en yakın -minimal cast yapabileceği- değerdeki metot çağrılır.  Mesela  parametre değeri `byte` ise  `short` ve `int` metodları mevcut ise  short metodunu kullanılır.

```java
public class Methods {

	public static void main(String[] args) {
		
		short x = 2;
		print(x);  // En yakın otomatik yükseltme int tipinde

	}

	public static void print(int x) {
		System.out.println("int metot print :"+x);
	}
    
	public static void print(long x) {
		System.out.println("long metot print :"+x);
	}

}
```



