---
title: "Java Jenerik"
last_modified_at:
categories:
  - java
tags:
  - java jenerik nedir
  - java raw type nedir
  - java bounded type nedir
  - java jenerik arayüz
toc: true
toc_sticky: true
toc_label: "Java "
author_profile: True
---

Generics sınıfları arayüzleri metotları ve veri yapılarını parametreştirmektir.

- Veri yapılarına(Collections) parametre girilerek sadece belirli tipler ile çalışmaya olanak sağlar.
- Sınıf arayüz ve metotlar parametreleştirilerek farklı veri tipleri ile çalışabilmesini sağlar.

Generics Javanın 1.5 sürümü ile geldi ve Java API’sinde birçok değişikliğe neden oldu. Ayrıca generecis her ne kadar basit gibi gözüksede biraz kafa karışıklığına sebep olabilir.  Konunun detayına girmeden önce jenerikte  kullanılan tip parametre isim, anlamları ve diğer bazı kavramları açıklayalım.

| Adlandırma | Açıklaması                                                   |
| :--------: | :----------------------------------------------------------- |
|     E      | Java API Collections yapılarında elemanı(Element) temsil eder. |
|     K      | Map gibi anahtar-değer çifti içeren yapılarda anahtar(*key*) tipini temsil eder. |
|     V      | Map gibi anahtar-değer çifti içeren yapılarda değer(*value*)  tipini temsil eder. |
|     N      | Sayı tiplerini temsil eder. ***Number*** sınıfın miras alan tipler(Double,Integer...) |
|  T-S-U-V   | Tipi bilinmeyen değerleri için kullanılan birinci/ikinci/üçüncü/dördüncü jenerik tip adlandırması |
|     ?      | Joker. Miras hiyerarşisinde bilinmeyen tipleri temsil eder(herhangi). |
|  extends   | Miras hiyerarşisinde alt sınıf/arayüzleri temsil eder. <? extends sınıf-adı> |
|   super    | Miras hiyerarşisinde üst sınıf/arayüzleri temsil eder. <? super sınıf-adı> |
|  Bounded   | Tipleri sınırlama.                                           |

Örnekler:

- ***E example***:

````java
class ListGenerics<E> {
   private List<E> l = new ArrayList<E>();
   // ...
}
````

- ***K-V example***:

```java
class MapGenerics<K,V>{
   private Map<K,V> map = new HashMap<K,V>();
    // ...
}
```

- ***N example***:

```java
class MapGenerics<N extends Number>{   
    // ...
}
```

- ***T S U V example***:

```java
public class GenericsClass<T, S> {
    private T t;
    private S s;
    // ...
}    
```
- ***? example***:

```java
// Number sınıfından miras alan herhangi bir tip (Double,Interger...)
class MapGenerics<? extends Number>{   
    // ...
}
```

- ***extends example***:

```java
// Student sınıfından alt sınıfları.
class MapGenerics<? extends Student>{   
    // ...
}
```

- ***super example***:

```java
// A sınıfının ebeveyn sınıfları
class MapGenerics<? super A>{   
    // ...
}
```

- **Jenerik yapılarda  ilkel tip(*int,double,boolean*...) kullanılmaz.**

```java
Set<int> meyveler = new HashSet<>(); // Hata!
Set<Integer> meyveler = new HashSet<>(); // Ok.
```

- **Miras ilişkisine sahip alt-sınıf üst sınıf yerine kullanılabilir. Fakat alt sınıf üst sınıfın yerine kullanılamaz.**(downcasting)

- Java SE 7 itibaren nesne üretilirken kurucu çağrısında jeneriğin tipinin belirtilmesine gerek yoktur.

```java
Box<Integer> integerBox = new Box<Integer>(); // Java SE 7 önce
Box<Integer> integerBox = new Box<>();    // Java SE 7 sonra kurucu çağrısında jeneriğin belirtilmesine gerek yok.
```

Collection konusunda jenerikler torbaları tek tür veri tipine özel yapmak için kullanıldı. Bu kullanım ile:

1. Spesifik tipden başka nesneler eklenmesini engelleyerek korumacı programlama (***defensive programming***) sağladı.
2. Jenerik ile tip belirtilmezse torba üzerinde yapılan ekleme çıkarma gibi işlemler Object tipi üzerinden gerçekleşir. Daha sonra veriler gerçek tipine çevrim (***cast***) yapılmak zorundadır. Jenerik kullanılarak çevrim(***cast***) işlemine gerek kalmaz.

```java
public class GenericsDemo {

    public static void main(String[] args) {
        
        Set meyvelerB = new HashSet();
        meyvelerB.add("Kivi");
        // add metodu object nesnesi kabul ettiği farklı veri tip eklenebilir.
        meyvelerB.add(23);
        System.out.println(meyvelerB); // [İncir, Kivi, Muz, 23]
        // Torbanın tipi String belirle.    
        Set<String> meyveler = new HashSet<>();
        meyveler.add("Kivi");
        // String'den farklı tipte değişken eklenemez.
        // meyveler.add(23);  // Hata!
    }
}
```

Jenerik bir sınıf tanımı yapalım. Farklı tiplerde iki nesne oluşturalım.

```java
public class GenericsClass<T, E> {
    private T t;
    private E e;

    public GenericsClass(T t, E e) {
        this.t = t;
        this.e = e;
    }
    @Override
    public String toString() {
        return "GenericsClass [T=" + t + ", E=" + e + "]";
    }

    public static void main(String[] args) {
        // Book nesnesi tanımlama
        GenericsClass<String, Integer> book = new GenericsClass<>("Otomatik Portakal", 1962);
        System.out.println(book); // GenericsClass [T=Otomatik Portakal, E=1962]
        // Yeniden farklı tipde jenerik sınıf kullanımı
        GenericsClass<Double, Boolean> jenerik = new GenericsClass<>(3.14, false);
        System.out.println(jenerik); // GenericsClass [T=3.14, E=false]
    }
}
```

### Metotlarda Jenerik

Metotlarda jenerik kullanılabilir. Farklı tipleri değerleri konsola yazdıran örnek.

```java
public class JenerikMetot {
    // Jenerik metot
    public static <T> void println(T value) {
        System.out.println(value);
    }

    public static void main(String[] args) {

        Integer i = 2;
        Double d = 3.14;
        String s = "Hello";
        Boolean b = true;

        println(i);// Integer değer = 2
        println(d);// Double değer = 3.14
        println(s);// String değer = Hello
        println(d);// Boolean değer = true
    }
}
```

- Bir jenerik metot arayüzü :  `<jenerik tipi> dönüş-tipi  metot-adi(parametre listesi) {}` jenerik tip dönüş değerinden önce tanımlanır.
- Metotların içinde jenerik nesnesi oluşturulamaz.
- Statik jenerik metot tanımlanabilir.

### Jenerikleri Sınırlama(Bounded Types)

Jenerikleri bazen sınırlamak  gerekebilir. Metoda karşılaştırma yapılıyorsa sadece Comparable tipler veya matematiksel işlemler için Number sınıfını miras alan tipler kullanılması sağlanabilir.

```java
<T extends Number>   // Sadece Number sınıfı miras alan tipler.(Double,Integer...)
<T extends Comparable>  // Sadece Comparable arayüzünü gerçekleştiren tipler.
```

Sayılar üzerinde ortalama hesaplayan jenerik sınıf yazalım.

```java
public class Calculator<T extends Number> {
    // Jenerik dizi
    T[] numbers;
    
    public Calculator(T[] numbers) {
        this.numbers = numbers;
    }
    // Ortalama hesapla
    public double getAverage() {

        double sum = 0.0;
        for (int i = 0; i < numbers.length; i++) {
            sum += numbers[i].doubleValue();
        }
        return sum / numbers.length;

    }
    public static void main(String[] args) {
        // Integer dizi geçme
        Integer[] intArray = { 1, 2, 5, 7, 9 };
        Calculator<Integer> cal = new Calculator<>(intArray);
        System.out.println(cal.getAverage()); // 4.8

        // Double dizi geçme
        Double[] doubleArray = { 1.3, 5.2, 5.7, 13.7, 11.9 };
        Calculator<Double> cal2 = new Calculator<>(doubleArray);
        System.out.println(cal2.getAverage()); // 7.56
    }
}
```

Eğer **Number** sınıfı extends ile belirlenmeseydi `numbers[i].doubleValue();`  satırında - **doubleValue** metodu Number sınıf üzerinde tanımlıdır- hata verecektir. Çünkü Java T  tipini Number olduğunu bilemez.

### Jenerik Joker (Wildcards Type)

Joker bilinmeyen tipleri temsil eder. Jenerikle kurgulanmış bir sınıftan iki ayrı nesne üretelim(İnteger ve Double) ve nesne üzerinden equals metodu çağıralım. Tiper uyumsuz(Double vs Integer) olduğundan hata verecektir.

```java
public class WildcardsDemo<T extends Number> {
    private T t;
    
    public WildcardsDemo(T t) {
        this.t = t;
    }
    
    public boolean equal(WildcardsDemo<T> x) {

        if (t.doubleValue() == x.t.doubleValue()) {
            return true;
        }
        return false;
    }
    
    public static void main(String[] args) {

        Integer i = Integer.valueOf(7);
        WildcardsDemo<Integer> x = new WildcardsDemo<>(i);
        Double d = Double.valueOf(7);
        WildcardsDemo<Double> y = new WildcardsDemo<>(d);
        
        // x Interger tipinde y  Double tipinde
        x.equal(y);  // Hata!

    }
}
```

Yukarıdaki problem, joker karakterini kullanarak çözülebilir.  `public boolean equal(WildcardsDemo<?> x) ` metoda geçilen sınıfın tipini joker(?) yapalım. Bunun anlamı Number sınıfından herhangi biri tip olabilir diyebiliriz.

```java
public class WildcardsDemo<T extends Number> {

    private T t;

    public WildcardsDemo(T t) {
        this.t = t;
    }
    // Joker ile Number miras alan herhangi bir tip olabilir.
    public boolean equal(WildcardsDemo<?> x) {

        if (t.doubleValue() == x.t.doubleValue()) {

            return true;
        }
        return false;
    }
    public static void main(String[] args) {

        Integer i = Integer.valueOf(7);
        WildcardsDemo<Integer> x = new WildcardsDemo<>(i);
        Double d = Double.valueOf(7);
        WildcardsDemo<Double> y = new WildcardsDemo<>(d);
        
        // x Interger tipinde y  Double tipinde
        System.out.println(x.equal(y));  // True

    }
}
```

Joker Collection yapılarında yaygın kullanılır.  List  değelerin konsola yazdıran metot yazalım.

```java
public class WildcardsDemo {
    // Farklı tipte değer alan list’in elemanlarını yazdırma
    public static void print(List<?> l) {
        for (Object i : l) {    
            System.out.print(" "+i);
        }
        System.out.println();
    }

    public static void main(String[] args) {

        List<Integer> li = Arrays.asList(1, 2, 3, 4);
        List<Double> ld = Arrays.asList(1.2, 2.3, 1.2);
        // Integer list yazdır.
        print(li); // 1 2 3 4
        // Double list yazdır.
        print(ld); // 1.2 2.3 1.2
    }
}
```

### Lower Bounded

Tip sınırlaması miras hiyerarşisinde yukarı doğru `super` ile yapılabilir. Örnekte sadece Kalfa ve Kalfa sınıfını miras alan alt-sınıflar listeye eklenebilir.

```java
public class LowerBounded {

    public static void main(String[] args) {
        // Lower Bounded
        List<? super Kalfa> p = new ArrayList<>();
        // Sadece Usta ve Kalfa eklenebilir.
        p.add(new Usta());
        p.add(new Kalfa());
        // Çırak ve İşçi eklenemez.
        // p.add(new Çırak()); // Hata !!
    }
}
class Usta extends Kalfa { }

class Kalfa extends Çırak { }

class Çırak extends İşçi { }

abstract class İşçi { }
```

### Jenerik Arayüz (Generics Interface)

Jenerik arayüzü tanımlanabilir.  Dikkat edilmesi gereken nokta arayüzü jenerik bir sınırlandırmaya(super or extends) sahipse  gerçekleştiren sınıf sınırlandırılan tipi tekrar bildirmelidir.

 ```java
public interface MaxMinUtility<T extends Comparable<T>> {
    T min();
    T max();
}
 ```

Yukarıdaki arayüzü gerçekleştiren sınıf(Test) Comparable arayüzünü belirtmelidir.

```java
class Test<T extends Comparable<T>> implements MaxMinUtility<T>{
    // ...    
}
```

Meyve sınıf  kurgulayalım. Sonra en çok ve en az kalori değerine sahip meyveyi bulalım. Hatırlatma meyve sınıfı Comparable iat comparto metodunu yerine getirmelidir. Meyve Sınıfı:

```java
public class Meyve implements Comparable<Meyve> {

    private String name;
    private int calorie;
    
    public String getName() {
        return name;
    }
    public Meyve(String name, int calorie) {
        this.name = name;
        this.calorie = calorie;
    }
    @Override
    public int compareTo(Meyve o) {
        if (calorie > o.calorie) {
            return 1;
        } else if (calorie < o.calorie) {
            return -1;
        }
        return 0;
    }
}
```

`MaxMinUtility` Test sınıf  yazalım ve kalorisi yüksek ve minimum olanı bulalım.

```java
class Test<T extends Comparable<T>> implements MaxMinUtility<T> {

    T[] array;

    public Test(T[] array) {
        this.array = array;
    }
    @Override
    public T max() {

        T max = array[0];
        for (int i = 0; i < array.length; i++) {
            if (array[i].compareTo(max) == 1) {
                max = array[i];
            }
        }
        return max;
    }
    @Override
    public T min() {

        T min = array[0];
        for (int i = 0; i < array.length; i++) {
            if (array[i].compareTo(min) == -1) {
                min = array[i];
            }
        }
        return min;
    }

    public static void main(String[] args) {
        // Meyve dizisi oluştur.
        Meyve[] meyveler = {new Meyve("Elma", 58),new Meyve("İncir", 80),new Meyve("Muz", 95)};
        // Jenerik sınıfı üretilmesi
        Test<Meyve> test = new Test<>(meyveler);
        Meyve max = test.max();
        Meyve min = test.min();
        System.out.println("Max value: " + max.getName() + " Min value :" + min.getName()); // Max value: Muz Min value :Elma

    }
}
```

Aynı Test sınıf kullanarak Integer değerler için  max ve min değeri bulalım. Sadece main metodu yazdım.

```java
public static void main(String[] args) {
        // Integer dizi
        Integer[] i = { 1, 3, 5, 2, 7 };
        Test<Integer> demo = new Test<>(i);

        int maxInt = demo.max();
        int minInt = demo.min();
        System.out.println("Max value: " + maxInt + " Min value :" + minInt); // 7, 1
            
}
```

Jenerik kullanarak az kod ile çok iş yaptık. Aksi halde Integer ve Meyve tipleri için farklı metodlar  yazılacaktı.

### Jeneriklerde Miras

- Jenerik tip jenerik olamayan sınıfı/arayüzü miras alabilir.

```java
public class  Rectangle <T,D> implements Drawable{
    T t;
    D d;
    // ...
    @Override
    public void draw() {
        System.out.println("Rectangle drawing...");        
    }
}
interface Drawable{
    void draw();
}
```

- Miras hiyerarşiden sadece aynı  tipi ile belirtilmiş nesneler birbirine referans olabilir.

```java
public class RectangleSolid<T, S, U> extends Rectangle<T, S> {

    U u;

    public RectangleSolid(T t, S s, U u) {
        super(t, s);
        this.u = u;
    }

    public static void main(String[] args) {

        RectangleSolid<Integer, Integer, Integer> solidInt = new RectangleSolid<>(3, 4, 5);
        RectangleSolid<Double, Double, Double> solidD = new RectangleSolid<>(3d, 4d, 5d);

        // Tip farkları belirtilmiş jenerikler farklı nesnelerdir.
        // solidInt = solidD; // Hata!
        Rectangle<Double, Double> recD = new Rectangle<>(3d, 2.1);
        Rectangle<Double, Double> recD2 = new Rectangle<>(3.4, 2.1);
        // Ancak aynı tiple üretilen Jenerik nesneler birbirine referans olabilir.
        recD = recD2; // Ok.
        recD = solidD; // Ok. Upcasting

    }
}
class Rectangle<T, S> {

    T t;
    S s;
    public Rectangle(T t, S s) {
        this.t = t;
        this.s = s;
    }
}
```

- instanceof operatörü jenerik sınıflarda doğru çalışmaz. Miras hiyerarşisinde  alt-üst sınıf fark etmeksizin sonuç daima `true`'dur. Downcasting ile gerçek tipe dönülmesi gereken durumlarda bu hususa dikkat edilmelidir.

```java
        RectangleSolid<Integer, Integer, Integer> solid = new RectangleSolid<>(3, 4, 5);
        Rectangle<Double, Double> rec = new Rectangle<>(3d, 2.1);
        // rec  RectangleSolid sınıfın nesnesi
        // olmamasına rağmen instanceof göre sonuç doğru.
        System.out.println(rec instanceof RectangleSolid);// true
        System.out.println(solid instanceof Rectangle);// true
```

- Miras alınan jenerik metotlar yeniden tanımlanabilir(overriding).

### Tip Silme (Type Erasure)

Java eski sürümleri uyumluluğu korumak için jenerik ifadelerini siler. Jenerik ifadelerin yerine:

1. Tip parametreleri (T-V-E...), sınırlı tipleriyle değiştirilir.

   ```java
   public class Point<T extends Number> {
      private T t;
       
      public T get() {
         return t;
      }   
   }
   ```

   Point Sınıfında jenerik ifadeler derleme zamanında  Number sınıf ile değiştirilir.

   ```java
   public class Point {
      private Number t;
       
      public Number get() {
         return t;
      }   
   }
   ```

2. Sınırlı tip açıkça belirtilmemişse Object tipleriyle değiştirilir.

   ```
   public class Point<T> {
      private T t;
       
      public T get() {
         return t;
      }   
   }
   ```

   Point Sınıfında jenerik ifadeler derleme zamanında  Object sınıf ile değiştirilir.

   ```java
   public class Point {
      private Object t;
       
      public Object get() {
         return t;
      }   
   }
   ```

### Tip Silme (Type Erasure) Gelen Belirsizlik

Jenerikler derleme zamanında silindiği için (farklı tipe sahip olmalarına rağmen) farklı imzaya sahip iki arayüz tanımlanamaz(overloading).

```java
public class GenericsProblem {
     // İmzaları farklı olmasına rağmen aynı isimli metot tanımlanamaz.
    public void call(List<String> meyveler) { }
    public void call(List<Integer> digits) { }
}
```

> Erasure of method call(List<String>) is the same as another method in type GenericsProblem

Belirsizlik jenerik parametreleri sınırlama ile çözülebilir.

```java
public class TypeErasure<T,S extends Number> {
        // S number ve T object sınıfı ile değiştirildiği için
        // call method overloading yapılabilir.
        public void call(T t) { }
        public void call(S s) { }
}
```

### Ham Tipler(raw type)

Raw Type jenerik ifadeleri parametsiz belirtmeksizin kullanılmasına denir. Örneğin  `list<String>` parametre tip iken `list` ham tiptir. Collection yapılarında kullanımı çok görülür.

Java eski 1.5 ve önceki sürümleri yazılmış kodlarda çalışırken tercih edilir.

Raw Type geçiş aşamasıdır. **Gerek kalmadığı sürece kullanılmamalıdır**. Çünkü çalışma zamanında hatalara yol açar.

***Derleme Zamanı (Compile Time):*** Program dosyalarının  makine koduna çevrilmesini ifade eder.

***Çalışma Zamanı (Runtime):*** Üretilen makine kodlarının hedef sistemde çalıştırılmasını ifade eder.

Örnekle konumuzu pekiştirelim.

```java
public class RawType<T> {

    T t;
    public RawType(T t) {
        this.t = t;
    }
    public T getT() {
        return t;
    }

    public static void main(String[] args) {
        // Parametre belirtilerek önerilen kullanım.
        RawType<String> normal = new RawType<>("Hello");
        // Kaçınılması gereken kullanım.
        RawType raw = new RawType<>(7);
        // Aşağıdaki işlem doğru derleme zamında gibi gözüksede runtime hata verir.
        String str = (String) raw.getT(); // Runtime exeption :java.lang.ClassCastException
        // Parametre belirtilerek yapılırsa zaten derleme zamanında hata verir.
        RawType<Integer> noRaw = new RawType<>(7);
        //str = (String) noRaw.getT(); // Hata! Cannot cast from Integer to String
    }
}
```

### Kısıtlamalar

1. İlkel tiplerde Jenerik yapılarda kullanılmaz.

   ```java
   List<int> digits = new ArrayList<>(); // Hata!
   ```

2. ***instanceOf*** operatörü jenerik nesneler üzerinde  kullanılmaz.

3. Jenerik sınıf değişkeni(static) tanımlanamaz.

   ```java
   public class NoStatic<T> {
       // Statik jenerik tip tanımlanamaz.
       private static T t; // Hata!
   }    
   ```

4. Jenerik tiplerin nesneleri oluşturlamaz.

   ```java
   public class NoInstance<T> {
       // Jenerik tipin nesnesi oluşturulamaz
       private  T item = new T();  // Hata!
   }   
   ```

   - Java Reflection kullanılarak `newInstance()` metodu ile nesnesi oluşturabilir.

5. Jenerik sınıflar Throwable arayüz ve türevlerini miras alamaz. Alt-üst tip sınırlama yapılırken kullanılabilir.

   ```java
   class NoName<T> extends Exception {} // Hata!
   class NoName<T> extends Throwable {} // Hata!
   class NoName<T extends Exception> {} // Ok.
   ```

   - Jenerik sıra dışı durum nesneleri fırlatılabilir fakat catch bloğu içinde kullanılmaz.

   ```java
   public <T extends Exception> void thowTest(T t) throws T {
           throw t; // Ok.
       }
   
   public <T extends Exception> void catchIt(T t) {
       try {
           thowTest(t); // call thowTest
       } catch (T e) {     // Hata!
           e.printStackTrace();
       }
   }
   ```

6. Farklı parametre tipi ile belirtilmiş jenerik tipli nesneler birbirine çevrilemez(cast).

   ```java
   Point<Integer> intObject = new Point<>();
   Point<Number> numberObject = new Point<>();
   // Miras ilişkisi olmasına rağmen çevrim(cast) yapılamaz.
   intObject = (Point<Integer>)numberObject; // Hata!
   ```

   - Joker kullanım durumunda çevrim yapılabilir.

   ```java
   public class Point<T> {
   
       T t;
   
       public RawType(T t) {
           this.t = t;
       }
       // Joker kullan durumunda çevrim yapılabilir.
       private static void add(Point<?> o) {
           Point<Integer> integerBox = (Point<Integer>)o; // Ok.
       }
       public static void main(String[] args) {
           Point<Number> numberObject = new Point<>(3);
           add(numberObject);
       }
   }
   ```

7. Tipe özgü jenerik referanslardan oluşan bir dizi oluşturulamaz. Joker ile oluşturabilir.

   ```java
   Point<Integer> [] a2 = new Point<Integer>[2]; // Hata!
   Point<?> [] a = new Point<?>[2]; // Ok
   ```

   - Görevi nesne değişkeni olan jenerik dizi tanımlanabilir.

   ```java
   public class Point<T extends Number,S> {
   
       T digits[]; // Jenerik tipte nesne değişkeni tanımlanabilir.
       S s;
       Point(T[] nums) {
           this.s = "Hello";  // Hata!
           this.s = 3;        // Hata!
           digits = new T[10];// Hata!
           // Dizi referans atanabilir.
           digits = nums; // Ok.
       }
   }
   ```


