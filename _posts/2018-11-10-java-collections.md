---
title: "Java Torba Yapılarına Giriş"
last_modified_at:
categories:
  - java
tags:
  - java iterable nedir
  - java iterator nedir
  - java comparable nedir
  - java comparator nedir
toc: true
toc_sticky: true
toc_label: "Java Collection"
author_profile: True
---

İçinde birden fazla öğe barındıran yapıları torba(*collection*) denir.  Java Collection Framework kullanıcılara verileri saklamayı sağladığı gibi veriler üzerinde manipülasyon yapması olanak tanır.

Collections veri üzerinde arama, sıralama ekleme manipülasyon (değiştirme), silme gibi işlemler sunar.

Collections data structure dersleri öğretilen algoritma yapıları üzerine inşa edilmiştir. Data structure dersini almak/kavramak torba yapılarını anlamayı daha kolaylaştırdığı gibi kullanabilmek için zorunlu değildir.

Java Collection Framework(JCF) 3 kısımdan oluşur.

1. **Arayüzler** (interface) : JCF’nin Soyut veri tipleri temsil ederler. `interface` manipüle edilerek envai çeşit torba yapıları oluşturulur.
2. **Sınıflar** (Class) : Arayüzlerin yerine getirilmiş(*implements*) sınıflardır. Aşağıdaki resimden arayüz ve sınıflar gösterilmiştir.
3. **Algoritmalar** : İşlevsel  -sıralama ,arama gibi- yardımcı yapılar.

{% include figure image_path="/assets/images/java-collection.png" alt="Collection" caption="Java Torba(collection) Yapıları"%}

`collection` arayüzünü miras alan ve yerine getiren yapılar(*resimde sol taraf*) doğrusal yapıdadır. ***Doğrusal yapılar*** elemanları dizili şekilde tutan tobralardır. Dışarıya her ne kadar iç kısımları farklı olsada dizi gibi gözükürler.

`map` arayüzünü miras alan ve yerine getiren yapılar(*resimde sağ taraf*) sözlük yapıdadır. Yani girilen değere karşılık bir değer veren/eşleştiren fonksiyon eğilimindedir.

### Collection Arayüzü (*interface*)

Direkt gerçektişirmesi yoktur. Collection arayüzünü devlan *`List, Queue ve Set`* gerçekleştirmesi (implement) bulunur. Java SE 11 itibariyle üzerinde tanımlı 20 tane metot bulunur. Önemli olan bazılarına göz aşınalığı olsun diye açıklayalım. Torbalar işlendikce davranışlar örnekleneçektir.

| Modifier and Type      | Method                                | Description                                                  |
| ---------------------- | ------------------------------------- | ------------------------------------------------------------ |
| boolean                | add(E e)                              | Torbaya bir eleman ekle. Ekleme işlemi başarılı olursa `true` başarısız olursa `false` döndürür. |
| boolean                | addAll(Collection<? extends E> c)     | Torbaya torba ekle. Ekleme işlemi başarılı olursa `true` başarısız olursa `false` döndürür. |
| void                   | clear()                               | Torbana bulunan tüm elemanları temizle/sil                   |
| boolean                | contains(Object o)                    | Elaman var mı? Bulursa `true` döndürür.                      |
| boolean                | containsAll(Collection<?> c)          | Torba var mı? Bulursa `true` döndürür.                       |
| boolean                | equals(Object o)                      | Arana değere eşit(söz dizimi) eleman var mı?                 |
| int                    | hashCode()                            | Torbanın 10 sistemde hash kodunu verir.                      |
| boolean                | isEmpty()                             | Torba boş mu?                                                |
| Iterator<E>            | iterator()                            | Torbanın `iterator` halini verir.                            |
| boolean                | remove(Object o)                      | Varsa tek bir elemanı silme.                                 |
| boolean                | removeAll(Collection<?> c)            | Varsa torbayı silme.                                         |
| default boolean        | removeIf(Predicate<? super E> filter) | Verilen `Predicate` kuşulu sağlayan elemanları sil.          |
| boolean                | retainAll(Collection<?> c)            | Belirli elemanları al, diğerlerini sil.                      |
| int                    | size()                                | Kaç tane eleman içeriyor?                                    |
| default Spliterator<E> | spliterator()                         | Torbanın [`Spliterator`](file:///home/baykoch/Documents/docs/api/java.base/java/util/Spliterator.html)  halini verir. |
| Object[]               | toArray()                             | Torbayı diziye çevir.                                        |
| <T> T[]                | toArray(T[] a)                        | Torbayı istenilen tipdeki diziye çevir.                      |

Ayrıca yukarıda bahsedilmeyen dosya girdi/çıktı işlemlerini ilgilendiren sonraki derslerde bahsedilecek `stream() parallelStream()` gibi metolar bulunur.

`Collection` davranışları(metotları), Java'nın en temel sınıf olan Object üzerinden çalışır. Çok şekillilik konusunda bahsedilen yerine geçebilme prensibine göre işler(**upcasting**). Olumsuz tarafı ise kendine özgü ait davranışları yerine getirememesidir. **`instanceof`** operatörü yardımı ile `downcasting` yapılarak gerçek tipe dönülür.

> `add()` metodu ile herhangi bir `upcasting` yapılmış nesne eklediğimiz düşünelim. Nesneyi geri aldığımız hangi nesne olduğunu anlamak için yeniden **instanceof** operatörü yardımı ile downcasting yapmamız gerekir.

## Iterator ve iterable Arayüzü

- `iterable` elemanları üzerinden tek tek geçilebilen demektir. Collection üzerinde geçilebilen yapıda olduğu için üzerinde `iterator()` davranışı bulunur.

`Collection/Set` arayünün üzerinde **bana elemanı ver** davranışın olmamasının **nedeni** yapının buna uygun olmamasıdır. Bu yüzden elemanlar ancak sırayla `iterator()` kullanılarak alınabilir.

***java.util.Iterator metotları:***

| Modifier and Type | Method                                       | Description                                                  |
| ----------------- | -------------------------------------------- | ------------------------------------------------------------ |
| default void      | forEachRemaining(Consumer<? super E> action) | Geriye kalan elemalar için tanımlanan işlemi(**lambda**) yerine getirir. |
| boolean           | hasNext()                                    | Sırada bir eleman var mı?                                    |
| E                 | next()                                       | Sıradaki elemanı verir.                                      |
| default void      | remove()                                     | Sıradaki elemanı siler.                                      |


iteratör bilgilendirme görevi gören aracıdır. Yani collection üzerindeki elemanları sırayla verir/bilgilendirir. Torba üzerinde bir ekleme çıkarma gibi işlem gücüne sahip değildir. Fakat iteratör alınmış bir torbanın üzerinde meydana gelen bir değişiklik iteratör çalışmasına durmasına neden olur. Bunun için java 1.8 ile iteratör üzerinden silme remove() metodu eklenmiştir.

**Özetle**:

- iteratör alınmış bir torba üzerinde bulunan metotlar ile **ekleme çıkarma gibi işlemler yapılamaz**.

- Eğer çıkarma işlemi yapılacaksa iteratör üzerindeki bulunan `remove` metodu kullanılmalıdır.

- `hasNext` çağrısından sonra next çağrısı yapılmalıdır. Çünkü sıradaki eleman olmayabilir(null).

- `hasNext` eleman kalmadıktan sonra `add` işlemi yapılabilir.

**Aklınıza şu soru takılabilir neden `remove` metodu var ama `add` metodu yok**. Çünkü iteratör ile alınan torba sıralı veya sırasız şekilde olabilir. Örnekle anlatalım:

>  Elemanları [1,2,3,4,5] olan bir torba olsun eğer iteratör 3 sırada ise eklenen yeni eleman iteratör bulunduğu sıradan daha önceki sıralara eklenmiş olabilir. İteratör son halinin [1,8,2,3,4,5] olduğunu varsayarsak yeni eklenen 8 elemanına asla ulaşamaz.

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class IteratorDemo {
    
    public static void main(String[] args) {
        Set<String> meyveler = new HashSet<>();
        meyveler.add("Elma");
        meyveler.add("Muz");
        meyveler.add("Ayva");
        meyveler.add("Nar");
        
        // Torbadan iteratör alma
        Iterator i = meyveler.iterator();
        
        // iteratör alınmış bir torba üzerinde işlem yapılamaz.
        //meyveler.add("Portakal"); // Hata! java.util.ConcurrentModificationException
        //meyveler.remove("Muz");   // Hata! java.util.ConcurrentModificationException
        
        // iteratör üzerinden remove yapılabilir.
        i.remove("Ayva");
        
        // Elemanları sırayla alama
        while (i.hasNext()) {
            System.out.println(i.next());
        }
    
        // Ancak iteratör tüm elemanların üzerinden geçildikten sonra
        // torba üzerinden ekleme çıkarma yapılabilir.
        meyveler.add("Kivi");
        meyveler.remove("Nar");
        
        System.out.println(meyveler);
    }
}
```

Java Api incelenirse `collection` arayüzünü ` java.lang.Iterable` arayüzünden `extends` edildiği görülür. Iterable arayüzün kendine has metotları vardır. Amacı yerine getiren (implements) nesnelerin for-each alınabilmesini sağlar.

***java.lang.Iterable metotları:***

| Modifier and Type      | Method                              | Description                                                  |
| ---------------------- | ----------------------------------- | ------------------------------------------------------------ |
| default void           | forEach(Consumer<? super T> action) | Her elemalar için tanımlanan işlemi(**lambda**) yerine getirir. |
| Iterator<T>            | iterator()                          | Belirtilen(T) tip de elemanların iteratörü alınır.           |
| default Spliterator<T> | spliterator()                       | Belirtilen(T) tip de elemanların `Spliterator` alınır.       |

- Iterable foreach nesneleri almak, iterator göre daha sağlıklı ve düzenlidir.

```java
import java.util.HashSet;
import java.util.Set;

public class IterableDemo {

    public static void main(String[] args) {
        Set<String> meyveler = new HashSet<>();
        meyveler.add("Elma");
        meyveler.add("Muz");
        meyveler.add("Ayva");
        meyveler.add("Nar");

        //for-each  ile tüm iterable torbaların üstünden geçilebilir.
        for (String string : meyveler) {
            System.out.println(string);
        }
        
        // Iterable üzerindeki forEach ile lambda fonksiyonel kod yazılabilir.
        // Aşağıdaki lambda kod parçasında elemanların hashCode gösterilmiştir.
        meyveler.forEach(s -> {
            System.out.println(s + "'s hash code:" + s.hashCode());
        });
    }
}
```

### Iterable ve iterator

Iterable torbanın üzerinden geçilebilen olduğunu belirtir/sağlar. iterator ise nesnelerin üzerinden geçen yapıdır. Zaten ancak iterable üzerindeki iterator() metodu ile iteratör alınabilir. Ek olarak Iterable arayüzü kendine has forEach(lambda) ve spliterator (alt yapırında iterator kullanır) metodu sağlar.

İterable olan her nesne foreach yapısıyla kullanılabilir.

Şimdi 3 farklı halini gösteren bir örnek yazalım.

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class IterableDemo {

    public static void main(String[] args) {
        Set<String> meyveler = new HashSet<>();
        meyveler.add("Elma");
        meyveler.add("Muz");
        meyveler.add("Ayva");
        meyveler.add("Nar");

        // foreach iterable torbanın üstünden geçme.
        for (String string : meyveler) {
            System.out.println(string);
        }
        /* foreach iterator kullanır. İki kod parçası birbirine eşittir.
        for (Iterator iterator = meyveler.iterator(); iterator.hasNext();) {
            System.out.println(string);
            
        }
        */

        // İterable üzerindeki forEach(lambda) ile torbanın üstünden geçme.
        meyveler.forEach(s -> {
            System.out.println(s);
        });

        // İteratör alarak(İterable üzerinden alınıyor) torbanın üstünden geçme
        Iterator i = meyveler.iterator();
        while (i.hasNext()) {
            System.out.println(i.next());
        }
    }
}
```

### Comparable ve Comparator Arayüzü

**Comparable** arayüzü sınıflara sıralanabilir özelliği sağlar. Yani **Comparable** arayüzünü miras lan veya gerçekleştiren sınıfların nesneleri sıralanabilir. Java API **Comparable** arayüzü incelenirse yerine getiren yüzlerce sınıf olduğu görülür. Bazılarını yazalım `BigDecimal, BigInteger, Boolean, Byte, ByteBuffer, Calendar, Double , String, Date`  …

Kısaca nesneleri karşılaştırılabilen(*öncelik sonralık*) sınıflar sıralanabilirler. İki tarih değeri (*bugün dünden büyüktür*), iki metin (*a b’den küçüktür*) ...

Comparable sadece bir tane davranışa sahiptir.

***int compareTo(T o)*** : İki nesneyi karşılaştırır.

- Eğer karşılaştıran ilk metin büyükse  aralarındaki uzaklığın pozitif sayı değerini verir.
- Küçükse uzaklığın negatif sayı değerini verir.
- Eşitse 0 döndürür.
- Sayılayılar için:

```java
public class ComparableDemo {
    
    public static void main(String[] args) throws InterruptedException {
    
        // Metinleri karşılaştırma
        String s1 = new String("ab");
        String s2 = new String("xc");
        System.out.println(s1+" vs "+s2+" :" +s1.compareTo(s2));
        // Nümerik değerlerin karşılaştırılması
        Double d1 = Double.valueOf("3.14");
        Double d2 = Double.valueOf("4.18");
        System.out.println(d1+" vs "+d2+" :" +d1.compareTo(d2));
        // Tarih karşılaştırma
        Date dt1 = new Date();
        Thread.currentThread();
        Thread.sleep(100);
        Date dt2 = new Date();
        System.out.println(dt1+" vs "+dt1+" :" +dt1.compareTo(dt2));        
    }    
}
```

- **Boolean** değerler `compareTo` ile karşılaştırılabilir. (*True > False*)

Kullanıcı tarafından oluşturulan sınıfları sıralamak için iki seçenek mevcuttur.

1. **Comparable** arayüzü gerçekleştirmeli(implements)
2. **Comparator** arayüzü gerçekleştirmeli(implements)  

> Kitap sınıf oluşturalım çıkış tarihine göre compareTo metodunu ezerek (overriding) karşılaştıralım.

- `Comparable` arayüzünü gerçekleştiren(*implements*) `Book` sınıfı

```java
public class Book implements Comparable {
    String name;
    String authorName;
    int releaseYear;
    public Book(String name, String authorName, int releaseYear) {
        this.name = name;
        this.authorName = authorName;
        this.releaseYear = releaseYear;
    }
    @Override // Yılların karşılaştırılması
    public int compareTo(Object o) {
        Book p = null;
        if (o instanceof Book) {
            p = (Book) o; // Gerçek tipi dönülmesi
        }
        int r = 0;
        if (this.releaseYear > p.releaseYear) {
            r = 1;
        } else if (this.releaseYear < p.releaseYear) {
            r = -1;
        }
        return r;
    }
    @Override
    public String toString() {
        return "Book [ismi=" + name + ", yılı=" + releaseYear + "]";
    }
}
```

- `ComparableDemo` test sınıfı:

```java
public class ComparableDemo {
    
    public static void main(String[] args) throws InterruptedException {
        
        Book b = new Book("Karamazov Kardeşler", "Dostoyevski" , 1866);
        Book b2 = new Book("Hacı Murat", "Tolstoy" , 1917);
        // Yıllara göre book nesnelerin karşılaştırılması
        System.out.println(b+" vs "+b2+" :" +b.compareTo(b2)); // -1
    }    
}
```

Modül,kütüphane sınıfları veya satın alınan  sınıfların kod içeriğini bilinmiyorsa **instanceof** operatörü ile `Comparable` olup olmadığı kontrol edilir. Eğer `Comparable` değilse `Comparable` üzerindeki `compareTo` metodu kullanılamaz.

Bu gibi durumlarda `Comparator` arayünü gerçekleştiren ara sınıf oluşturularak karşılaştırma yapılır.

`Comparator` 18 tane metot vardır. Birçoğu fonksiyonel yapıda java 1.8 ile eklenmiştir.  Bu bölümde en  temel `compare` metodu ele alalım.

***int compare(T o1,  T o2)*** : Ezilerek(*Overriding*) tanımlanan kıstasa göre **o1** ve o2 **nesnelerini**  karşılaştırır.

Kitap sınıf oluşturalım çıkış tarihine göre `Comparator` arayünü gerçekleştiren `BookComparator` ara sınıf yardımı ile **compare** metodunu ezerek (*overriding*) karşılaştıralım.

- Book sınıfı:

```java
public class Book{
    String name;
    String authorName;
    int releaseYear;
    public Book(String name, String authorName, int releaseYear) {
        this.name = name;
        this.authorName = authorName;
        this.releaseYear = releaseYear;
    }
    public int getReleaseYear() {
        return releaseYear;
    }
    public void setReleaseYear(int releaseYear) {
        this.releaseYear = releaseYear;
    }
    @Override
    public String toString() {
        return "Book [ismi=" + name + ", yılı=" + releaseYear + "]";
    }
}
```

- `Comparator` arayüzünü gerçekleştiren(*implements*) `BookComparator` sınıfı

```java
public class BookComparator implements Comparator {
    
    @Override
    public int compare(Object o1, Object o2) {
        // Gerçek tipi dönülmesi
        Book b = (Book) o1;
        Book b2 = (Book) o2;
    
        int r = 0;
        if (b.getReleaseYear() > b2.getReleaseYear()) {
            r = 1;
        } else if (b.getReleaseYear() < b2.getReleaseYear()) {
            r = -1;
        }
        return r;
    }
    public static void main(String[] args) {
        
        Book b = new Book("Karamazov Kardeşler", "Dostoyevski" , 1866);
        Book b2 = new Book("Hacı Murat", "Tolstoy" , 1917);
        // Book nesnesin Comparable olup olmadığı kontrol edildi.
        System.out.println(b instanceof Comparable); // false
        // Comparator arayüzünü gerçekleştiren ara sınıf
        BookComparator bc = new BookComparator();
        // compare metodu ile karşılaştırma
        System.out.println(b+" vs "+b2+" :" +bc.compare(b,b2)); // -1
    }
}
```

