---
title: "Java Metot Kavramı "
last_modified_at:
categories:
  - java
tags:
  - java metot imzası ve arayüzü
  - java parametre
  - java by call value
  - java this kullanımı
  - java kurucu metot
toc: true
toc_sticky: true
toc_label: "Java Method"
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
<niteleyici>  <geri dönüş tipi> <metod ismi> ( <parametreler> ) {

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

### Metotlara Parametre Geçme (*by-pass-value*)

Java metotlara parametre değeri (by-pass-value) ile geçilir. Metot, geçilen parametreleri yeni değerlere kopyalar ve işlemine devam eder.

Kafa karışıklığını gidermek için veri yapıları dersimizden küçük bir hatırlatma yapalim. Basit tipler kendileri üzerinden kamaşık tiplere ise referans üzerinde ulaşılır. Basit tiper üzerinden yapılan işlemler yeni bir değer üretir.  Karmaşık nesne üzerinde  yapılan işlemler ise yeni bir nesne üretmez var olan nesne üzerinde güncellem yapar. Nesnin birden çok referansı olabilir.

Kod örneğimizde dönersek  `calculate` metoduna girilen `x` değeri(2) yeni bir değişkene kopyalanıyor ve kopyalanan değişken bir attırıyor. `Main` metodu içerisinde `x` ile metot içerisinde `x` farklı değişkenler. Benzer şekilde nense `calc` geçilirse - Dikkat! Nesne değil referası geciliyor. - nesnenin referansı yeni bir referansa kopyalanır. Artık nesnin iki ferans olur ve bu iki referans üzerinden yapılan işlemler nesne üzerinde görülür.

Sonuç olarak metotlara değişkenlerin değerleri geçilir yani kopyalanır. `x` değişkeni yeni bir `x` değerine kopyalanmıştır. Karmaşık nesnenin ise referansı yeni bir referansa kopyalanmıştır.

```java
public class Calculator {
    
    int x;
    // Call by value: X değişkenin kendisi kopyalanıyor.
    public  void calculate(int x) {
        x++;
    }
    // Call by value: Nesnenin kendisi değil, referansı kopyalanıyor.
    public  void calculateComplex(Calculator object) {
        x++;
    }
    
    public static void main(String[] args) {
        
        Calculator calc= new Calculator();
        int x = 2;
        // call by value
        calc.calculate(x);
        System.out.println(x);           // 2
        // call by value
        calc.x = 2;
        calc.calculateComplex(calc);
        System.out.println(calc.x);  // 3
    }
}
```

Eğer izah edemediysem ;

1. Basit tipler değerleri  geçilir.
2. Karmaşık tipler ise referansları geçilir. (Aslında doğru ifade değil)

  Karmaşık tiplerin referans değerleri metotlara geçildiğinden  metot içinde yapılan işlemler asıl veriyi değiştirdiğinden bahsettik(Diziler de karmaşık tiptir!). Ama maalesef  String karmaşık veri tipi için bundan bahsedemeyiz.

```java
public class CallByValue {
	 // Metoda String ve dizi karmaşık tiplerini geçme
	public void testParam(String str, int[] array) {
		// Veriyi güncelle
        str = "Test";  
		array[0] = 12; 

	}
	public static void main(String[] args) {
		 CallByValue pr = new CallByValue();
		 String str = "Hello";
		 int [] array = {1,2,3};
		 pr.testParam(str, array);
		//String tipi hariç dizi ve diğer karmaşık tip verileri güncellenir.
        for (int i : array) {
			System.out.println(i); // print "12, 2, 3"
		}
		 System.out.println(str);  // print "Hello"
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

### Niteleyici (*Modifier*)

Java niteleyiciler iki ana alt başlıkta toplanır.

1. Erişim Niteliyiciler (Access Modifier) : ***Public, Protected, Private***
2. Diğer erişim niteleyici olmayan (Non-access Modifier) : ***Abstract, [Static](https://baykoch.github.io/blog/java/java-static-keyword/), [Final](https://baykoch.github.io/blog/java/java-final-keyword/), Synchronized, Native, Strictfp, Transient, Volatile***

Genellikle ilk başta erişim niteleyici kullanılmakla birlikte her niteliciyi bir kez kullanılabilir. Kunular ilerledikce teker teker işlenecek ve sayfa bağlantısı eklenecektir.

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
        print(25);        // int
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

### Kurucu Metot (*Constructor*)

Nesne üretilikekn çağrılan metotlara kurucu metot denir. Dizi ve String tipleri hariç tüm karmaşık tiplerde kurucu metotlar bulunur ve nesne üretirken bu çağrı kullanılır. Kurucular nesnesini ilk haline (durumunu) almasına sağlarlar. Kurucu tanımlanması bile JVM olağan `default` kurucu çağrısı yapar. Kurucu metotların isimleri tanımlandığı **sınıfın ismi** ile **aynı** olmalıdır.

```java
public class Book {
    
    String name;
    String author;
    String publisher;
    int year;
    // Herhangi bir kurucu tanımlanmazsa bile JVM default kurucu tanımlar.
    // Default kurucu
    public Book() {}
}
```

Olağan `default` kurucusu nesne olağan değerler almasını sağlar.

```java
public class Test {

    public static void main(String[] args) {
        // Default kurucu çağrısı
        Book book1= new Book();
        // Default değerler
        System.out.println(book1.name);      // null
        System.out.println(book1.author);     // null
        System.out.println(book1.publisher); // null
        System.out.println(book1.year);         // 0
    }
}
```

Kurucu metotların içinde değer ataması yapılabilir ama önerilmez. Çünkü her üretilen nesne belirtilen değerleri alırlar.

```java
public class Book {
    
    String name;
    String author;
    String publisher;
    int year;
    // Kurucu metot  içinde statik değer ataması önerilmez!
    public Book() {
        name = "Vurun Kahpeye";
        author = "Halide Edib Adıvar";
        publisher = "Özgür Yayınları";
        year = 1926;
    }
}
```

Üretilen nesne özelliklerini çağrıldığı yerden girilebilir. İlgili sınıfın kurucu metot yeniden tanımlanarak `overloading` parametre alması sağlanır. Böylece  farklı parametrelerde kurucular tanımlanabilir. Parametre alan kurucuya **akıllı veya argümanlı** kurucu denir.

Yukarıda JVM herhangi bir kurucu tanımlanması default kurucu sağladığını belirtildi. Eğer bir akıllı kurucu tanımlanmışsa `JVM` artık default kurucu sağlamayacaktır. Bunun nedeni `default` kurucu ile `default` değer almasını engellemek olabilir. Yani nesne akıllı kurucu ile özelliklerini almaya zorlanır.

```java
public class Book {

    String name;
    String author;
    String publisher;
    int year;
    // Akıllı Kurucu
    public Book(String name, String author, String publisher, int year) {
        this.name = name;
        this.author = author;
        this.publisher = publisher;
        this.year = year;
    }
    // Overload  edilmiş kurucu
    public Book(String name, String author) {
        this.name = name;
        this.author = author;
    }

    public static void main(String[] args) {
        // Eğer en az bir akıllı kurucu varsa default kurucu JVM tarafından sağlanamaz.
        // Bu nedenle default kurucuyu kullanıcı tanımlamalıdır.
        Book book1 = new Book(); // Hata !
        
        // Akıllı kurucu çağrısı
        Book book2 = new Book("Vurun Kahpeye", "Halide Edib Adıvar", "Özgür Yayınları", 1926);
        // Kurucu metodu yeniden tanımlama(overloading)
        Book book3 = new Book("Huzur", "Ahmet Hamdi Tanpınar");
    }
}
```

### This Kelimesini Kullanımı

This kelimesini sınıf içerisinde belirgin 3 görevi vardır.

1. Kurucu metodan başka kurucu meoto çağrısı yapmak.
2. Sınıf değişkenleri ayırt etmek
3. Sınıf nesnesini kendi geri döndürmek

Bir kurucu yaptığı işin bir parçasını diğer bir kurucuyu  yapabilir. Bu durum kurucu diğer kurucuyu `this` anahtar kelimesi ile çağırır. `this` çağrısından önce **kod yazılamaz**. Çünkü kurucu bir nesnenin üretilmesini sağlar, üretilmeden önce o nesne ile ilgili işlem yapılamaz.

Bir kitap evinden çıkmış kitapları, yeni yayın evini tekrar girmeden oluşturalım.

```java
public class Book {

    String name;
    String author;
    String publisher;
    int year;

    public Book(String name, String author, String publisher, int year) {
        this.name = name;
        this.author = author;
        this.publisher = publisher;
        this.year = year;
    }
    // this kurucu çağrısı
    public Book(String name, String author, int year) {
        // This çağrısından önce herhangi bir kod yazılmaz!
        // System.out.println(author); // Hata!
        this(name, author, "Özgür Yayınları", year);
    }

    public static void main(String[] args) {
        // Özgür Yayınlara ait kitaplar
        Book book1 = new Book("Vurun Kahpeye", "Halide Edib Adıvar", 1926);
        Book book2 = new Book("Ateşten Gömlek", "Halide Edib Adıvar", 1922);
    }
}
```

This kelimesi aynı isme sahip sınıf değişkenleri (instance variable) ile yerel değişkenleri birbirinden (local variable) ayırt etmek için kullanılır. Örneğin akılı kurucu metotlara girilen parametre parametre ile sınıf değişkeni aynı ise  nesne değişkenin önüne konularak karmaşıklık önlenmiş olur.

```java
public class Calculate {

    int x;
    int y;

    public calculate(int x,int y) {
        this.x = x;
        this.y = y;
    }
    public void thisExample(int x) {
        System.out.println(x);       // Yerel değişkeni: 2
        System.out.println(this.x);  // Nesne değişkeni: 17
    }
    public static void main(String[] args) {
        // nesne üretildi.
        Calculate calculate = new Calculate(17,25);
        // nesne değişkeni ile yerel değişkeni ayrım
        book1.thisEx(2);
    }
}
```

Eğer nesnenin davranışı (ya da bir metot) geriye nesnenin kendisi gönderiyorsa this kelimesi kullanılır.

```java
public class Book {

    String name;
    String author;
    String publisher;
    int year;
    int printersKey;

    public Book(String name, String author, String publisher, int year,int printersKey)     {
        this.name = name;
        this.author = author;
        this.publisher = publisher;
        this.year = year;
        this.printersKey = printersKey;
    }
    public Book updatePrinting() {
        printersKey++;            // baskı değerini bir attır.
        return this;            // Nesnenin kendisini geri döndürür.(book1)
    }

    public static void main(String[] args) {
        Book book1 = new Book("Vurun Kahpeye", "Halide Edib Adıvar","Özgür Yayınları",1926,1);
        // book1 baskı değeri bir attrıldı ve geri döndü.
        // Dönen book1 üzerindeki metot yeniden çağrıldı ve "printersKey" 3 oldu.
        book1.updatePrinting().updatePrinting(); // printersKey = 3
    }
}
```
