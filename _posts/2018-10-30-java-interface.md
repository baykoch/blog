---
title: "Java Arayüz(interface)"
last_modified_at:
categories:
  - java
tags:
  - java arayüz  
  - java default metot
  - java private metot
  - java static metot
toc: true
toc_sticky: true
toc_label: "Java "
author_profile: True
---

 Arayüz(interface) tabiattaki nesnelerin birbirleri ile haberleştiği normlar bütünüdür. İnsanlar için dil, göz veya el birer arayüzdür.

Konumuza dönersek bütün metotları soyut olan sınıflara arayüz(**interface**) denir. Varsa erişim belirleyiciden sonra,  arayüz isminden önce `interface` anahtar kelimesi getirilerek oluşturulur.

Arayüzlerin metotları olağan(**default**) olarak soyut(**abstract**) ve `public` olur. Bu yüzden `abstract` ve `public` anahtar kelimesi yazılmayabilir.

```java
public interface A {
  // Aşağıdaki iki metot eşittir.  
  public abstract void start();
  void start(); // public ve abstract yazılmayabilir.
}
```

Arayüzler sınıflar tarafın sınıf isminde sonra ***`implements`*** anahtar kelimesini kullanarak devralır ve yerine getirir(*implementation*). Devralan sınıflar arayüzün metotları yerine getirmek zorundadırlar.

```java
public class A implements B {
    // Arayüzleri devralan sınıflar arayüzün metotlarını yerine getirmelidir.(implement)
    @Override
    public void start() {
        System.out.println("Lets go.");
    }

}
interface B {
    void start();
}
```

- Devirlan sınıflar metotları yerine getirmez ise kendisi de arayüz(interface) olmak zorundadır.

- Arayüzler ile onu devralan sınıflar arasında miras ilişkisi vardır. Bir arayüz kendisini gerçekleştiren/devralan sınıfların ebeveyn sınıftır. Aralarında somutluk ve soyutluk farkı vardır. Yani  nesnesi üretilebilen sınıflar somut, üretilemeyen arayüzler ise soyutur.

- Arayüzler yerine getirilen davranışları tanımlandığından genellikle sonu `-able` (yapılabilen) ile biten isim kullanmak yaygındır.

```java
// Arayüzlerin isimleri sonu genellikle -able biter
public interface Printable{
    
    void monochrome(String text); // Siyah-beyaz baskı
    void polychromechrome(String text);// Renkli baskı
    void printInfo();
    
}
```

- Sınıflar birden fazla arayüzü devralabilir. Devraldığı her arayüzün metotlarını geçcekteştimek zorundadır.

```java
public class A implements B, C {
    // Birden fazla arayüzleri devralan sınıf arayüzlerin metotlarını yerine
    // getirmelidir.(implement)
    @Override
    public void start() {
        System.out.println("Lets go."); // From B interface
    }

    @Override
    public void stop() {
        System.out.println("Stopping..."); // From C interface
    }
}

interface B {
    void start();
}

interface C {
    void stop();
}
```

- Sınıflar sadece bir sınıfın miras alabilirken(**extends**) birden fazla arayüzü yerine getirebilir(**implements**).

```java
//Sınıflar sadece bir sınıfı extends edebilirken birden fazla arayüzü gerçekleştirebilir.
public class A extends D implements B, C {...}

interface B {...}

interface C {...}

class D {...}
```

- Bazen arayüzler hiçbir metot içermeyebilir.-java serializable interface gibi- Bu gibi yapılara ***marker design pattern*** denir. Amacı ise bir sınıfı işaretlemektir. Örneğin `serializable` arayüzünde devalan sınıflar serialize ve deserialize edilebilir. Bir sınıfın serialize ve deserialize olup olmadığını ***instanceof*** operatörü yardımı kontrol edilebilir.
- Arayüzler durumları (*attributes*) yoktur. Sadece `public`,`static` ve `final` olan tek bir değişken tanımlanabilir. ***İlk değer verilmek zorundadır.*** Sadece bu tip değişkenlerden oluşan, davranış içermeyen arayüzler `enum` gibi davranır(eğer enum yapısı varsa neden  arayüzü bu şekilde kullanıyorsun) bu da istenmeyen durumdur, **kaçınılmalıdır**.

```java
public interface C {
    // Arayüzlerde tek tür değişken tanımlanabilir. İlk değeri verilmek zorundadır
    // Aşağıdaki iki tanımlamada eşittir.
    int i = 2; // public, final ve static yazılmayabilir.
    public static final int i = 2;
}
```

- Sıklıkla arayüz durum(*state/attributes*) içermediğinden  dolayı soyut sınıflar tarafından devralınır. Arayüzü devralan soyut sınıf(***abstract class***) durum(*attribute*) eklendiği gibi yeni metotlar ve `get/set` metotları ekler. **Soyut sınıf, somut sınıfların aksine devraldığı arayüzdeki metotları yerine getirme gibi bir zorunluluğu yoktur.**

```java
public class Usta extends İşçi {

    public Usta(String name, int age) {
        super(name, age);
    }
    @Override
    public void work() {
        System.out.println("Usta çalışyor.");
    }
    @Override
    protected void getPaid() {
        System.out.println("Maaş yatırıldı.");
    }

}
// Soyut sınıflar miras aldığı arayüzlere yeni metot tanımlayabilir.--> getPaid()
// Devraldığı arayüzdeki metot yerine getirmeyebilir. --> work()
// Arayüzlere eklenmeyen durum(attributes) ekler. --> name, age
// get/set metotları ekler.
abstract class İşçi implements Workable {

    private String name;
    private int age;

    public İşçi(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) {
        this.age = age;
    }
    protected abstract void getPaid();

}
interface Workable {
    void work();
}
```



- Arayüzlerin durumları olmadığından kurucuları yoktur. Devralan/yerine getiren sınıflar tarafından `super` çağrısı yapılmaz.
- **Arayüzler birbirini yerine getiremez**(*implements*). Fakat bir veya birden fazla `extends` edebilir. Miras aldığı (extends) arayüzlere yeni metotlar ekleyebilir.

```java
public interface A extends B,C {
    void pay();
}
interface B{
    void call();
}
interface C{
    void callOff();
}
```

Java 1.8 ile default metot, java 1.9 ile ise private metot kavramı arayüzlere eklenmiştir. Kronolojik(*tarihsel*) olarak arayüzlerdeki değişime göz atalım.

 ***Java 7 Arayüz (İnterface)***

1. Statik Değişkenler (Constant variables)
2. Soyut Metotlar (Abstract methods)

 ***Java 8 Arayüz(İnterface) Değişiklikler***

1. Statik Değişkenler (Constant variables)
2. Soyut Metotlar (Abstract methods)
3. Olağan Metotlar (Default methods)
4. Statik Metotlar (Static methods)

 ***Java 9 Arayüz(İnterface) Değişiklikler***

1. Statik Değişkenler (Constant variables)
2. Soyut Metotlar (Abstract methods)
3. Olağan Metotlar (Default methods)
4. Statik Metotlar (Static methods)
5. Özel/Hususi Metotlar (Private methods)
6. Özel/Hususi Statik Metotlar (Private Static methods)

Elimizden geldiğince bu yapıları inceleyelim.

#### A.Default and Private method in interface

Değiştirilen/güncellenen eski kütüphane veya modül dosyaları  problemlere neden oluyordu. Java `binary compatibility` geriye doğru uyumluluk sistemi ile oluşabilecek hataları bir noktaya kadar çözebiliyordu.

`binary compatibility` : Bir arayüze/soyut sınıfa herhangi bir metot eklenir ve derlenirse(*compile*) onu devralan/yerine getiren sınıflar **yeniden derlenmediği** sürece hatasız çalışmaya devam eder.

Fakat devralan sınıflar yeniden derlenirse(*compile*), yeni eklenen metodu yerine getirmek(*overriding*) zorunda olduğundan hata verecektir. Böyle durumda oluşabilecek  hataları çözmek için `Default` metotlar ile arayüzlere yerine getirme/gerçekleştirme(*implement*) yetkisi verildi.

Arayüzlere Private metot tanımlama yetkisi 1.9 sürümü ile geldi. Private metotlar Default metoların birbiri aralarında haberleşmesine olanak verirken, aynı zamanda arayüzlere özel metot yazılmasını sağladı.

> Bir yazılım için `log` bilgileri gösteren modül geliştirdiğimizi düşünelim. Basit olarak yazılım açıldığında ve kapandığında bilgi versin. Fakat sonradan program  **güncellenirken**  de bilgi vermesini sağlamalıyız.

> Javanın eski sürümleri için yapılması gereken yol/yöntem/yordam: `Loggable` arayüzüne gerekli soyut metot eklenecek ve `Loggable` devralan tüm metodlar yeni eklene metodu gerçekleştirmesi(*implement*) gerekecektir. Lakin eğer `Loggable` arayüzü yerine getiren/miras alan onlarca veya yüzlerce sınıf varsa iş çığrından çıkacaktır.

```java
public interface Loggable {
    // Arayüz il hali
    void startInfo();
    void stopInfo();

}
```

Java 1.8 sürümü ile birlikte `loggable` arayüzünde bu davranışı yerine getirebiliriz. Artık `Loggable` devralan/yerine getiren sınıfların metodu/davranışı gerçekleştirmesine gerek kalmaz.

- Private method ile `log` bilgilerin Türkçe tarih ile birlikte gösterilmesini sağlayalım. Türkce tarih bilgisi `Loggable` arayüzüne ait sinifn kendisi ilgilendiren özel metottur. Diğer sınıfların kullanımına açılmasına gerek yok.

```java
import java.text.DateFormat;
import java.util.Calendar;
import java.util.GregorianCalendar;
import java.util.Locale;

public interface Loggable {
    // ilk metotlar
    void startInfo();
    void stopInfo();
    // Sonradan eklenen metot
    default void updateInfo() {
        System.out.println(getTRDateInfo() + " Yazılım güncelleniyor.");
    }
    // Türkce Tarih Bilgisi
    // Metot arayüzü ilgili davranışı yerine getirdiğinden özel olmalı
    private String getTRDateInfo() {
        Calendar c = new GregorianCalendar();
        DateFormat df = DateFormat.getDateTimeInstance(DateFormat.MEDIUM, DateFormat.MEDIUM, new Locale("tr"));
        return df.format(c.getTime());
    }
}
```

`Loggable` arayüzünü yerine getiren sınıf yazalım ve test edelim.

```java
import java.text.DateFormat;
import java.util.Calendar;
import java.util.GregorianCalendar;
import java.util.Locale;

public class Log implements Loggable {

    @Override
    public void startInfo() {
        System.out.println(getTRDateInfo()+" Yazılım başlatılıyor.");
    }

    @Override
    public void stopInfo() {
        System.out.println(getTRDateInfo()+" Yazılım kapatılıyor.");
    }
    
    private String getTRDateInfo() {
        Calendar c = new GregorianCalendar();
        DateFormat df = DateFormat.getDateTimeInstance(DateFormat.MEDIUM, DateFormat.MEDIUM, new Locale("tr"));
        return df.format(c.getTime());
    }
    // Test log sistem
    public static void main(String[] args) {
        
        Log logObject = new Log();
        logObject.startInfo(); // 2 Kas 2018 19:16:02 Yazılım başlatılıyor.
        logObject.updateInfo();// 2 Kas 2018 19:16:02 Yazılım güncelleniyor.
        logObject.stopInfo();// 2 Kas 2018 19:16:02 Yazılım kapatılıyor.  
    }

}
```

Default metotları yerine getiren/devalan somut, soyut(abstract) sınıf ve arayüz(interface)  3 farklı şekilde yaklaşabilir.

1. Olduğu gibi kullanabilir.

2. Ezerek (*overriding*) kendi davranışını tanımlayabilir.

3. Kendisi soyut sınıf ise `abstract` şeklinde tanımlayarak soyut metot haline getirebilir.

   ```java
   public abstract class Print implements Printable {
       // Soyut sınıfın arayüz üzerindeki default metot soyut yapması.
       public abstract void updateInfo();
   }
   interface Printable extends Readable {
       // Arayüz üzerindeki metodun ezilmesi
       @Override
       default void updateInfo() {
           System.out.println(" Override default method in interface.");
       }
   }
   interface Readable {
   
       default void updateInfo() {
           System.out.println(" Default method in interface.");
       }
   }
   ```

#### Default metot ile gelen garip durum 1

Arayüzler(interface) metodları tanımlar onu devralan sınıflar ise yerine getirir. Olması gereken zaten budur. Fakat default metotların eklemesi ile 3. duruma göre tam tersi durum oluşur. Arayüz yerine getirirken onu devalan sınıf ise tanımlamıştır. Buda oop prensibine uymayan garip ve aykırı durumdur.

#### Default metot ile gelen garip durum 2

Bütün sınıflar java.lang.Object sınıfını olağan/otomatik bir şekilde miras aldığı için Object sinifi içindeki hashCode() gibi metotları ezerler,varsayılan haliyle kullanır veya kullanmaz. Default metot eklemsiyle arayüzlere yerine getirme yetkisi verildi. Eğer Object sınıfına ait bir metot arayüz üzerinde yerine getirirse onu devan tüm sınıfların zorunlu bir şekilde  metotları yerine getirmesi gerekir. Bu anormal bir durumdur. Çünkü Object sınıfın metotları isteğe bağlı kullanılması gerekir. Bu yüzden arayüz üzerinde  toString, hashCode gibi metotların tanımlanmasına izin verilmez.

#### Default metot ile gelen garip durum 3

Java çoklu mirasa  arayüzler üzerinden  izin verir.

```java
// Çoklu mirasa arayüzler üzerinden izin verilir.
public class A implements B,C {
    
}
interface B {}
interface C {}
```

Fakat şöyle bir problemle karşılaşabiliriz:

Eğer **B** ve **C** arayüzleri bir A sınıfını tarafindan implements edilmiş olsun.  **B** ve **C** arayüzlerin ikisinde bulunan aynı isimli default metot A sınıfı tarafında ezilmez ise hangi metodu çağıracağını bilemez.

```java
public class A implements B, C {
    // Devraldığı arayüzler aynı isimli iki default metot varsa ezilmesi gerekir.
    public static void main(String[] args) {
        A p = new A();
        // Hangi metot çağrılacak?
        p.mMethod(); // Hata
    }
}
interface B {

    default void mMethod() {
        System.out.println("Default method in interface B");
    }
}
interface C {
    
    default void mMethod() {
        System.out.println("Default method in interface C");
    }
}
```

### B. Static method in interface

`Utility class` veya `helper class` olarak bilinen sadece statik metotlardan oluşan durumları olmayan ve nensesi üretilmeyen sınıflardır. Birbiri alakalı birçok metot barındırırlar. Program her yerinden kullanın sağlamaktır. [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) göre programıncınn kendini tekrar etmesini engellemektedir. Java’da `Math` paketi gibi bir çok `helper` sınıfı bulunmaktadır.

Fakat nesneleri üretilmediğinden ve sarmalamadan(*durumu sahip değil*) yoksun olduğunda katarsak pekala OOP presibiyle pek uymamaktadır.

Peki neden utility class kullanılıyordu? Çünkü arayüzlerin üstünde statik metotlara izin verilmediğinden kurgulanamıyordu. Java 1.8 arayüzler üzerinde  statik  ve implements izin verildi. Artık helper sınıflarını arayüzler üzerinde tutulabilir. Ekstra sınıflar tanımlamaya gerek kalmadı.

- Dikkat edilmesi gereken nokta ise statik metotlar devralınmaz. **Bu yüzden bu metolar ancak arayüz üzerinde çağırabilirler.**

> Basit bir örnekle doğruları uzunluk bakına karşılaştıran  program yazalım. Dikkat edilmesi gereken nokta **Math** sınıf üzerindeki max metot yerine `Drawable` arayüz üzerindeki kendi (*max*) metodumuzu  kullanadık. Böylece `Drawable` arayüzünü miras yolu ile nesnesini oluşturabilidik. Bu yöntem OOP prensibini daha uygundur.

```java
public class Line implements Drawable {

    protected int size;
    
    public Line(int size) {
        super();
        this.size = size;
    }    
    @Override
    public void draw() {
        System.out.println("Line's drawing.");

    }
    public static void main(String[] args) {

        Line l = new Line(2);
        Line l2 = new Line(3);
        // Arayüz üzerindeki statik metotlar ancak arayüz üzerinden çağrılabilir.
        System.out.println(Drawable.max(l.size, l2.size));
    }
}
interface Drawable {
    void draw();
    // Arayüz üzerindeki statik metot math statik metot yerine kullanıldı.
    public static int max(int a, int b) {
        return a > b ? a : b;
    }
}
```

### Tip Kavramı (type in inheritance)

Miras alma (extends) ve arayüz yerine getirme(implements) kavralarında sonra bir sınıfın birçok tipi olabileceği anlıyoruz. Birçok tipi sahip olamaz çok şekilli olmaktır. Dünyamızdan örnek verirsek bir erkek evde baba veya eş işyerinde öğretmen hastanede bir hasta olabilir. Fakat sadece bulunduğu tipin davranışlarını yerine getirir. İşteyken herkese bir eş/koca gibi davranamaz. Hastanede hasta iken hastalara ders anlatamaz yani öğretmenlik yapamaz. Buna mukabil toparlarsak çok şekilli bir nesne sadece bulunduğu (referans) tipin davranışlarını yerine getir.

- Lakin eğer referans tipteki davranış kendisi tarafından ezilmiş işe kendi sınıfındaki davranış kullanılır. Çünkü referanslar sınıflara dinamik bağlam ile bağlanır(derleme zamanında).

- Soyut sınıf ve arayüzlerin nesneleri üretilmesede somut ebeveynlerinin referansı olabilir.

```java
public class Şef extends Usta {

    public static void main(String[] args) {
        
        // Şef sınıfı 7 farklı tipe sahiptir(Çok şekillilik).
        // Hangi tipde ise onun davranışlarını yerine getirebilir.
        Şef p = new Şef();
        Workable w = p;
        Object o = p;
        Usta u = p;
        Kalfa k = p;
        Çırak c = p;
        İşçi i = p;

    }
}

class Usta extends Kalfa { ... }

class Kalfa extends Çırak { ... }

class Çırak extends İşçi { ... }

abstract class İşçi implements Workable { ... }

interface Workable { ... }
```
