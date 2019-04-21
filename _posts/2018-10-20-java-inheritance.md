---
title: "Java Miras (inharitance) "
last_modified_at:
categories:
  - java
tags:
  - java miras
  - java yeniden kullanım
  - java birleşik nesne
  - java extends
  - java super nedir
toc: true
toc_sticky: true
toc_label: "Java "
author_profile: True
---



Java'da  yeniden kullanım iki farklı şekilde sağlanır.

1. Var olan sınıflardan yararlanarak birleşik sınıflar oluşturma: Sahiplik ilişkisi (*has-a /composite*)

2. Var olan sınıflardan devralarak alt sınıflar oluşturma. Olma ilişkisi (*is-a /inheritance*)

## Sahiplik İlişkisi (*Composite*)

Sahiplik (*composite*)  ilişkininde sınıflar birilerine sahiptirler. Bu sahiplik bazen güçlü(***composition***) bazen zayıf(***aggregation***) olabilir. Bir bilgisayar işlemci, bellek (*ram*) olmadan çalışamaz. Bu bir güçlü bağlantıdır. Oysa hoparlör veya monitör olmadan çalışabilir belki ihracatlarımız tam anlamıyla yerine getirmezse de yine çalışır, bu da zayıf ilişkidir diyebiliriz. Java sahiplik ilişkisi her zaman referanslar sağlanır aslında hiçbir nesne birbirine sahip olamaz sadece ona ulaşabileceği bir adrese sahip olur.

```java
public class Cumputer {
    // Güçlü sahiplik, kesinlikle olmalı.
    private String name;
    private Cpu cpu;
    private Ram rams;
    private HardDisk hd;
    // Zayıp sahiplik, olmasada olur.
    private Monitor monitor;
    private Speaker[] speakers;
    private Printer printer;

}
```

**Dikkat** edilirse Computer değişkenlerin sadece referans numaralarına sahiptirler.

Birleşik nesneler arasında bir ilişki (*association*) ve bağımlılık (*coupling*) -işlemci olmadan bilgisayar çalışmaz.- oluşturular. Birleşik nesneler birimlerinde hizmet alırlar. Bilgisayarın bir belgeyi yazıcıdan çıktı verilmesini  talep etmesi gibi. Bu gibi hizmet bileşen istenmesine yönlendirme (***delegation***) denir.

```java
public class Printer {
    
    public void print() {
        System.out.println("Completed print job");
    }

}
```

- Yönlendirme (*delegation*) metot çağrısı

```java
public class Computer {

    private String name;
    private Printer printer;

    public Computer(String name, Printer printer) {
        this.name = name;
        this.printer = printer;
    }
    // Yönlendirme (delegation) metot
    private void printDocument() {
        // İstenilen işi bileşinden talep edilmesi.
        this.printer.print();
    }        
}
```

## Olma ilişkisi (*inheritance*)

Miras olma veya gibi ilişkisidir. Bir nesne diğerinin özellikleri olarak türeyebilir. Örneğin taşıt sınıfından otomobil, kamyon gibi sınıflar veya öğrenci sınıfından lisans,  lisansüstü sınıflar türetilebilir.

- Kendisini miras olan sınıfa ebeveyn  veya süper sınıf (***parent/super class***) denir.

- Miras alan sınıflara çocuk veya alt-sınıf (***child/sub-class***) denir.

- Miras `extends` anahtar kelimesi ile sağlanır.

Miras alan sınıf süper sınıfın özelliklerini(state) ve metotları devir alırlar. Bu noktada üç kıstas vardır.

1. Ebeveyn sınıfın  private  üye ve metotlarını devralınamaz.
2. Eğer başka bir pakette ise varsayılan(default) üye ve metotları devralınamaz.
3. Kurucular devralınamaz, çağrılabilir.

```java
package baykoch.inheritance.A;

public class Rectangle {
    private int id;            // Alt-sınıflarca devir alınamaz.      
    protected int length;    // Alinabilir.
    protected int width;    // Alinabilir.
    String color;             // Alınamaz. Ancak aynı pakette bulunmak koşulu ile devri alınabilir.
}
```

Dikdörtgen(*Rectangle*) sınıfını devralarak (miras ile) dikdörtgen prizma(*RectangleSolid*) sınıfı elde edilmesi.

```java
package baykoch.inheritance.B;

public class RectangleSolid extends Rectangle {
    protected int height;
    
    public static void main(String[] args) {
        
        RectangleSolid shape = new RectangleSolid();
        shape.height = 3; // Ulaşılabilir, kendi değişkeni
        shape.length = 4;// Ulaşılabilir, ebeveyn sınıftan devir almış.
        shape.width = 2; // Ulaşılabilir, ebeveyn sınıftan devir almış.
        
        shape.id = 123;       // Hata! Ulaşılamaz (The field Rectangle.id is not visible).
        shape.color = "red"; // Hata! Ulaşılamaz (The field Rectangle.id is not visible).

    }
}
```

Sonuç olarak miras yolu ile  **protected** olan özelliklere farkı pakette dahi olsa ulaşılabilir. Varsayılan (*default*) özelliklere sadece aynı pakette ise ulaşılabilir.

- Her sınıf kendi kurucusuna sahip olmalıdır. Miras alan sınıflar ebeveyn sınıfları içerdikleri için kullanıcı tarafından çağırmaz ise ebeveyn sınıfın varsayılan kurucusu çağrılır. Aksine alt-sınıflar üst sınıfın akıllı kurucularını çağırabilir.

- Super/ana/ebeveyn sınıf akıllı kurucu varsa alt/devir alan/miras alan sınıflarda akıllı kurucu olmak zorundadır.

- Ebeveyn sınıflardaki kurucu çağrıları `super()` ile sağlanır.

  ```java
  public class RectangleSolid extends Rectangle {
 
      protected int height;
      
      public RectangleSolid(int height, int id, int length, int width, String color) {
          super(id, length, width, color);// Ebeveyn kurucu çağrısı
          this.hight = hight;
      }
 
  }
  ```

- Ebeveyn sınıfı:

  ```java
  public class Rectangle {
 
      private int id;
      protected int length;
      protected int width;
      String color;
 
      public Rectangle(int id, int length, int width, String color) {
          this.id = id;
          this.length = length;
          this.width = width;
          this.color = color;
      }
 
  }
  ```

- `super()`  kurucu çağrısı en üstte yazılmalıdır. Çünkü ilk atama (initializing) her zaman ebeveynden çocuklara doğru devam eder.

  - [Daha önce nesne başlatma sırasına değinmiştik](https://baykoch.github.io/blog/java/java-initializing/#ba%C5%9Flatma-s%C4%B1ras%C4%B1-initialization-order). Başlatma sırasını miras konusu dahilinde güncelleyelim.

    1. İlk başta miras alınan sınıflar başlatılır.
    2. Static sınıf değişkenleri
    3. Static metotlar
    4. Nesne sınıf değişkenleri
    5. Nesne kurucusu

    ```java
    public class A extends B{
        
        static B b = new B();
    
        public A() {
            System.out.println("A");
        }
        public static void main(String[] args) {
            A a = new A(); // A nesnesini üretme
        }
    }
    
    class B extends C{    
        public B() {
            System.out.println("B");
        }
    }
    
    class C {
        public C() {
            System.out.println("C");
        }
    }
    ```

    >C <br/>
    >B<br/>
    >C<br/>
    >B<br/>
    >A
    
    A nesnesini üretmek için sırayla:

    - A sınıfı B sınıfını miras aldığı için ilk B sınıfı

    - B sınıfı C sınıfını miras aldığı için ilk C sınıfı çalıştırılacak. **Çıktı : *C B***

    - Ebeveyn sınıfların üretilmesi tamamladığına göre artık A nesnenin üye değişkenleri yani `static B b = new B();` komutu çalıştırılır. B sınıfının üretilmesi için C sınıfı çalıştırılır. **Çıktı : *C B C B***

    - Son olarak A’nın üye değişkenleri kalmadığından A sınıfın kurucusu çağrılır. **Çıktı : *C B C B A***

- ***extends*** kelime anlamı genişletme demektir. Eğer ebeveyn/ana sınıfların miras alınıp ona ekstra bir şeyle ekrnemıyorsa onun ebeveyn sıfıtan bir farkı olmaz ki bunu yapmak anlamsızdır.

- Çocuk sınıflar ebeveyn sınıflar arayüzüne ve üye değişkenine sahip olurlar(*Protected* olduğunu varsayıyoruz). Bu özelliğe ***yerine geçebilme*** denir. Aşağıdan yukarıya yani çocuklardan ebeveynlerine doğru çalışır. Aşağıya doğru çalışmaz. Bir örnekle anlatalım.

- İşçi sınıf, İşçi  sınıfını miras  olan Çırak sınıfı, çırak sınıfını miras alan Kalfa sınıfı, kalfa sınıfını miras alan usta sınıflarını kurgulyayım:

> Müteahhit bana bir işçi çağırın dediğinde çırak, kalfa ve usta çağrılabilir. Çünkü çırak,kalfa ve usta aynı zamanda bir işçidir. <br/>Eğer müteahhit bana bir usta çağırın dediğinde çırak, kalfa çağrılamaz. Çünkü çırak ve kalfa aynı zamanda bir usta değildir.

```java
public class Usta extends Kalfa{
    
    // İşçi çağrısı
    public void up(İşçi işçi) {}
    // Usta çağrısı
    public void down(Usta usta) {}
    
    public static void main(String[] args) {
        Usta usta=new Usta();
        // Yeniden kullanım aşağıdan yukarıya doğru çalışır.
        usta.up(new İşçi());
        usta.up(new Çırak());
        usta.up(new Kalfa());
        usta.up(new Usta());
        //Yeniden kullanım yukarıdan aşağıya doğru çalışmaz.
        //usta.down(new İşçi()); // Hata!
        //usta.down(new Çırak());// Hata!
        //usta.down(new Kalfa());// Hata!
        usta.down(new Usta()); // Usta çağrılıyorsa ancak usta gönderilebilir.
    }
}

class Kalfa extends Çırak{}

class Çırak extends İşçi{}

class İşçi {}
```

- Sınıflarda yukarıdan aşağıya inildikçe (ebeveynden çocuklara) sınıfların daha spesifik ve özel halleri bulunur. Yani dikdörtgen örneğimizde dikdörtgenin iki boyutlu iken onu miras alan çocuğu/alt-sınıfı olan dikdörtgen prizması üç boyutludur.

### Ezme (*Overriding*)  

Miras allan alt-sınıflar kendi metotlarını tanımlayabildiği gibi  ebeveyn sınıfların metotlarını değiştirebilir. Metodun arayüzü aynı kalıp içeriğini değiştirmesi yeniden tanımlamasına ezme(***overriding***) denir. Overriding edilmiş metotlara çok şekilli metotlar denir(*polymorphic*).

İşçi usta örneğimizde her işçi çalışmalıdır. Ama çırak kalfa ve usta farklı işleri yaparlar. İşçi work() ezilerek yeni iş tanımı yapılır. Yeni metot tanımlamak yerine ezme işlemi yapılması anlamlıdır. Yani nabza göre şerbet verilir. Ama verilen sonuçta şerbettir.

```java
public class RectangleSolid extends Rectangle {

    protected int height;

    public RectangleSolid(int height, int length, int width) {
        super(length, width);
        this.hight = hight;
    }
    // calculateArea metodu ezilerek yeniden yazılması
    @Override
    public int calculateArea() {

        return 2 * (hight * width + height * length + width * length);
    }
    public static void main(String[] args) {
        
        RectangleSolid rs = new RectangleSolid(2, 3, 4);
        int result = rs.calculateArea();
        System.out.println("Area:" + result);

    }
}
```

```java
public class Rectangle {

    protected int length;
    protected int width;

    public Rectangle(int length, int width) {
        super(); // Object sınıfının kurucu çağrısı
        this.length = length;
        this.width = width;

    }
    public int calculateArea() {

        return length * width;
    }
}
```

- ***Sadece nesne metotları (non-static) ezilebilir. Sınıf metotları (static) ve üye değişkenleri ezilemez.***

  ```java
  public class A extends B {
  
      // Hata! static metotlar ezilemez(overriding).
      @Override
      public static void staticMethod() {
          System.out.println("Static method in A");
      }
  }
  class B {
   
      public static void staticMethod() {
          System.out.println("Static method in B");
      }
  }
  ```

- Ebeveyn sınıftaki nesne değişkeni yeniden tanımlanırsa kendi yeni(ebeveyne sınıftan bağımsız) nesne değişkeni gibi davranır. Yani nesne değişkenleri `overriding` işlemine tabi olmadıkları için tanımlanabilir.

  ```java
  public class A extends B { 
      //Nesne değişkenleri overriding işlemine tabi olmadıkları için tanımlanabilir.
      // protected int id = 17; 
      
      public static void main(String[] args) {
              A p = new A();
          // Eğer 3.satırı (protected int id = 17) yorumu kaldırırsak 
          // p.id = 17 (A sınıfındaki id çağrılır.)
          // Aksi halde p.id = 7 (B sınıfındaki id çağrılır)
          System.out.println(p.id);
   
      }
  }
  class B {
      protected int id = 7;
  }
  ```

- Statik metodun alt-sınıflata yeniden tanımlanması ebeveny sınıfdaki metodu gölgeler(***shadowing***). 

  ```java
  public class A extends B {
  	// Gölgeleyen statik metot
  	public static void call() {
  		System.out.println("Static method in A");
  	}
  
  	public static void main(String[] args) {
  		// 3. satıdaki call() metodunu silersek
  		// Her iki durumdada B sınıınfaki call metodu çağrılaçaktır.
  		// Aksi durumda A sınınfaki call() metodu B sınıfndakini gölgeler.
  		// A.call() A sınıfındaki metodu
  		// B.call() ise B sınıfdaki metodu çağırır.
  		A.call();
  		B.call();
  
  	}
  }
  
  class B {
  
  	// Gölgelenmiş statik metot
  	public static void call() {
  		System.out.println("Static method in B");
  
  	}
  }
  ```

- Ezme işleminde daha **kısıtlayıcı bir erişim niteleyici** tanımlanamaz. İşçi `work()` metoduna sahipse, çırak metodu ezip private yapamaz. Çünkü çıraktan devralan kalfa çalışması gerekir(`work()`) ama çırak kısıtladığı için çalışamaz ki buna anlamsız durumdur. Ters yönde *genişletici* **erişim niteleyici**  tanımlanabilir.

  ```java
  public class A extends B {
  	// Hata! Ezme işleminde daha kısıtlayıcı bir erişim niteleyici tanımlanamaz
  	@Override
  	protected void call() { // Cannot reduce the visibility of the inherited method from B
  	}
  }
  
  class B {
  	public void call() {
  	}
  }
  ```

- **Dikkat!** `Overloading` bir sınıfın arazyünün (parametreleri) değiştirilerek yeniden aynı sınıfta yazılmasını ifade eder. `Overriding` ise ebeveyn sınıftaki bir metodun ezilerek aynı arayüzle yeniden tanımlanmasıdır.

### Super
`Super` ebeveyn kurucusu çağrısı yapıldığını yukarıda görmüştük. **Ayrıca super ile bir üstteki ebeveyn sınıfın metotlarını çağırabilir**. Hatta bakım(*maintenance*) açısından çok önemlidir. İşçi sınıfının maaşına 100 TL fazla para eklendiğinde her alt-sınıfın (çırak,kalfa ve usta) metotlarına bu değer eklemek zorunda kalabiliriz. Sadece işçi sınıfına ekleyip diğer metotları ezerken(overriding) `super` ile bu metot çağırabiliriz.

- super.super gibi kullanım yoktur. Sadece bir basamak yukarıdaki ebeveyne ulaşılabilir.
- `super` **statik metot veya bloklarda kullanılamaz.**
- `this` kelimesi kullanılarak kendi metot ve üye değişkenlerine `super` ile  ebeveyn sınıfa (miras alınan)  değerlerine ulaşılır.

Şimdi dikdörtgen örneğimizdeki alan hesabında tekrar eden kısımları yeniden yazmadan ve yukarıdaki notları içeren programı yazalım.
Dikdörtgenin alanı : `l * w`
Dikdörtgenin prizmanın alanı : `2( l*w + l*h + w * h)`


```java
public class RectangleSolid extends Rectangle {
	protected int id = 2;
	protected int hight;

	public RectangleSolid(int hight, int length, int width) {
		super(length, width);
		this.hight = hight;
	}

	public void thisVsuper() {
		System.out.println(id); // Kendi değeri = 2
		System.out.println(this.id); // Kendi değeri = 2
		System.out.println(super.id); // Ebeveynin değeri = 3

	}

	@Override
	public int calculateArea() {
		// Ebeveyn metot çağrısı super()....
		return 2 * (super.calculateArea() + hight * length + hight * width);
	}

	public static void main(String[] args) {

		RectangleSolid rs = new RectangleSolid(2, 3, 4);
		System.out.println(rs.calculateArea()); // 52
		// Hata! main metot static olduğu için super kullanılamaz.
		System.out.println(super.calculateArea()); // Hata!
		System.out.println(super.length); // Hata!
	}
}

class Rectangle {
	protected int id = 3;
	protected int length;
	protected int width;

	public Rectangle(int length, int width) {
		super();
		this.length = length;
		this.width = width;
	}

	public int calculateArea() {
		return length * width;
	}
}
```

Örnekte `super.calculateArea()` kullandığımız gibi tekrar eden kısımlardaki hizmeti ebeveyn sınıftaki metottan talep etmek ***kaliteli kod*** yazımı sağlar.

### Javada Çoklu Miras (Multiple *extends*)

Java çoklu mirasa (*extends ile*) izin vermez. Yani bir sınıf aynı anda iki sınıfı birden miras (*extends edemez*) alamaz.

```java
// Çoklu mirasa izin verilmez.
public class A extends B,C { // Hata!
    
}
```

Javada neden çoklu mirasa izin verilmediği açıklayalım:

Eğer **B** ve **C** sınıfı bir D sınıfını miras almış olsun. **B** ve **C** sınıfların ikiside **D** sınıfın `call()` metodu ezdiğini(overriding) varsayalım. Bu durumda **A** metot hangi sınıfın (*B ve C*) `call()` metodunu çağıracağını bilemez.

```java
public class A extends B,C { // Hata!

    public static void main(String[] args) {
        A p = new A();
        p.call(); // Hangi sınıftaki call metodu çağrılacak (B or C)?
    }

}
class B extends D {

    @Override
    public void call() {
        super.call();
    }
}
class C extends D {

    @Override
    public void call() {
        super.call();
    }
}
class D {
    public void call() {

    }
}
```


