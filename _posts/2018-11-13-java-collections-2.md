---
title: "Java Torba Yapıları: 2.Set Yapısı"
last_modified_at:
categories:
  - java
tags:
  - java HashSet nedir
  - java TreeSet nedir
  - java SortedSet nedir
  - java NavigableSet nedir
toc: true
toc_sticky: true
toc_label: "Java Collection"
author_profile: True
---

Collection arayüzü miras alan iki temel `List ve Set` arayüzü bulunur. Bu kısımda **Set** arayünü yerine getiren torbalarından bahsedilecek.

Aynı elemandan birden fazla bulunmayan kümedir. Set arayüzü Collection devraldığı davranışlara yeni metot eklemez sadece `add` metodunun aynı elemandan birden fazla eklenemeyecek şekilde işlevini değiştir. Bunu yaparken nesnelerin hash kodunu ve eşitlik durumunu kontrol eder.

Set arayüzünü gerçekleştiren HashSet ve TreeSet iki sınıf vardır.

### HashSet

Aynı elemandan birden fazla bulunmayan, elemanları belirli bir sırada olmayan kümedir. Elemanlar Set içinde rastgele sırada bulunur. Dinamik hashtable yapısı üzerinde inşa edilmiştir. Hash table her elemanı bir dizi işlemden geçirerek uygun boş bir indise eklenmesiyle oluşur. Hashtable en önemli özelliği elemanlara ulaşma süresinin  O(1) zamanda gerçekleşmesidir.

- HashSet dizilim yeni eleman eklenmesiyle değişebilir.

- HashSet dizme kavramı olmadığından **iterator** yardımı ile elemanlar sırayla alınır.

| Constructor                                             | Description                                                  |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| `HashSet()`                                             | Yeni boş, 16 elemanlı bir set üretme. **\*Load factor(0.75)**. |
| `HashSet(int initialCapacity)`                          | Başlangıç kapasitesi belirtilerek boş set üretme.**\*Load factor(0.75)**. |
| `HashSet(int initialCapacity,        float loadFactor)` | Başlangıç kapasitesi ve load factor belirtilerek  boş set üretme |
| `HashSet(Collection<? extends E> c)`                    | Torba eklerek yeni set üretme(Torbadaki tekrar eden elemanlar atılır). |

- **\*Load factor:** Doluluk oranı olarak bilinen kıstas, HashSet belirtilen değere (default değer 0.75) ulaştığında kapasitesi 2/3+1 oranında genişler. Örnek vermek gerekirse 16 iken 12 eleman ulaştığında(0.75) kapasite(2/3+1) 25'e çıkarılır.

```java
public class HashSetDemo {
    
    public static void main(String[] args) {
        
        Set<String> s1 = new HashSet<String>();
        s1.add("Kivi");
        s1.add("Muz");
        s1.add("İncir");
        // Tekrar eden eleman eklenemez.
        if (!s1.add("Kivi")) {
            System.out.println("Tekrar eden eleman");
        }
        // Eklenen elemanlar rastgele tutulur.
        System.out.println(s1); // Kivi İncir Muz
      
        // Torba ekleyelim.        
        List<Double> l = new ArrayList<>();
        l.add(3.14);
        l.add(2.43);
        l.add(3.14); // Arraylist tekrar eden eleman eklenebilir.
        
        // List içinde tekrar eden değerler eklenmez.
        Set s= new HashSet(l);
        // iteratör yardımı ile elemanların alınması
        Iterator i =s.iterator();
        while (i.hasNext()) {
            System.out.println(i.next()); // 3.14 2.43        
        }      
    }
}
```

**HashSet ekleme işlemi yaparken:**

1. *Değişkenlerin hash kodunu kontrol eder **eğer farklı ise ekler***.
2. *Yok eğer hash kodu aynı ise **equals** ile eşitlik karşılaştırması yapılır, sonuç farklı ise ekler, aynı ise eklemez.*

#### Neden hash code aynı ise equals çağrılır?

Java  farklı nesneler aynı hash koda sahip olabileceğinden iki nesnenin aynı olup olmadığından emin olamaz. equals ile değerleri kontrol edilir.

#### How to Add Native Object in HashSet

Java içinde var olan sıralanabilen (Data,String,Double...) değer eklenlenirken **HashSet** `AbstractSet` aldığı **[hashCode](https://baykoch.github.io/blog/java/java-object-class/)** ve [**equals**](https://baykoch.github.io/blog/java/java-object-class/) metotları kullanarak ekleme işlemini kontrol ediliyor.

Peki ya kullanıcı tarafından oluşturulan sınıflar ekleme işlemi neye göre ve nasıl yapılacak? Sonuçta **HashSet** tekrar eden elemanların bulunmamalıdır. Bu durumda kendi oluşturduğumuz sınıflarda `Object` sınıfından miras alınan  **[equals](https://baykoch.github.io/blog/java/java-object-class/)** ve **[hashCode](https://baykoch.github.io/blog/java/java-object-class/)** metotlarını ezmeliyiz. Aksi halde **HashSet** iki nesne aynı olsa bile eklemeye devam edecektir.

> Bir sınıfta bulunan öğrencilerin kaydını tutalım. Öğrenci nosu kıstasına göre ekleme işlemini yapalım.

- Tekrar eleman(*duplicate check*)  kontrolun sağlıklı çalışması için hashCode ve equals ikiside davranışlarının gerçekleştirilmesi(implement) zorunludur.
- ***Student Sınıf:*** Öğrenci no.suna göre `hashCode` ve `equals` metotları ezilmiştir.(overriding)

```java
public class Student {

    private String name;
    private int no;

    public Student(String name, int no) {
        this.name = name;
        this.no = no;
    }
    // HashSet sağlıklı çalışabilmesi içi hashCode ve equals metodu ezilmelidir.(overriding)
    @Override
    public int hashCode() {
        return no;
    }
    @Override
    public boolean equals(Object o) {
        if (o == this)
            return true;
        if (o == null)
            return false;
        if (!(o instanceof Student))
            return false;
        // Öğrenci no.suna göre karşılaştırma
        Student s = (Student) o;
        if (s.no != no) {
            return false;
        }
        return true;
    }
    @Override
    public String toString() {
        return "Student [name=" + name + ", no=" + no + "]";
    }
}
```

- ***Test Sınıfı:***

```java
import java.util.Set;

public class HashSetDemo {
    
    public static void main(String[] args) {
    
        Set<Student> st = new HashSet<>();
        Student s1 = new Student("Ali K.", 1);
        st.add(s1);
        Student s2 = new Student("Veli Z.", 2);
        st.add(s2);
        Student s3 = new Student("Seda Y.", 3);
        st.add(s3);
        // Hash kodları aynı ise birde equals ile değerleri kontrol edilir.
        // Çünkü farklı değer aynı hash koda sahip olabilir.
        Student s4 = new Student("Seda Y.", 3);
        st.add(s4);  // Ekleme yapmaz.
    
        System.out.println(st); // Ali, Seda, Veli
    }
}
```

### TreeSet

**TreeSet** *HashSet* yapısından  farklı olarak elemanları sıralı bir şekilde saklar. TreeSet **NavigableSet** ve **SortedSet** arayüzleri yerine getirir. Data Structures dersinde anlatılan [Red-Black Tree](https://en.wikipedia.org/wiki/Red%E2%80%93black_tree) gerçekleştirlmiş halidir. Red-Black Tree yapıları `O(lgn)`  zaman karmaşıklığı sahiptir. Yanı eleman ekleme çıkarma gibi işlerler logaritma 2 tabanında N süresinde gerçekleşir. Örnek verirsek **16** elemanlı bir **TreeSet** arana değer en fazla (*`log2^16 = 4`*) 4 deneme sonra bulunur.

- TreeSet null eleman eklenmesine izin verir.
- Elemanları sıralı bir şekilde tutar.
- Tekrar eden elemanlar eklenmez.

```java
public class TreeSetDemo {
    
    public static void main(String[] args) {

        Set<String> s1 = new TreeSet<>();
        s1.add("Kivi");
        s1.add("Muz");
        s1.add("İncir");
        // Tekrar eden eleman eklenemez.
        if (!s1.add("Kivi")) {
            System.out.println("Tekrar eden eleman");
        }
        // Eklenen elemanlar sırayla tutulur.
        System.out.println(s1); // Kivi İncir Muz

        // Torba ekleyelim.
        List<Double> l = new ArrayList<>();
        l.add(3.14);
        l.add(2.43);
        l.add(4.1);
        l.add(3.14); // Arraylist tekrar eden eleman eklenebilir.

        // Torbada tekrar edilen elemanlar eklemez.
        Set s = new TreeSet(l);
        // iteratör yardımı ile elemanların alınması
        Iterator i = s.iterator();
        while (i.hasNext()) {
            System.out.println(i.next()); // Elemanlar sıralı: 2.43 3.14 4.1
        }
    }
}
```

TreeSet sınıfı SortedSet ve NavigableSet arayüzlerini gerçekleştirdiğden bahsetmiştik. Şimdi bu arayüzlerde buluna metotlara göz atalım ve kullanımına örnek verelim.

- ***SortedSet Interface*** : TreeSet sıralama özelliği sağlar.

| Modifier and Type      | Method                                   | Description                                                  |
| ---------------------- | ---------------------------------------- | ------------------------------------------------------------ |
| Comparator<? super E>  | comparator()                             | Set buluna elemanlar Java nenslerinden(Data,String ...) oluşuyorsa ise null. değeri kullanıcı oluşturduğu(Öğrenci,Araba ...) nesneler ise comparator hali döndürülür. |
| E                      | first()                                  | Sıralamadaki ilk elemanı verir.                              |
| SortedSet<E>           | headSet(E toElement)                     | Sıralamada `toElement` değerinden önce bulunan elemanları verir. |
| E                      | last()                                   | Sıralamadaki son elemanı verir.                              |
| default Spliterator<E> | spliterator()                            | Torbanın [`Spliterator`](file:///home/baykoch/Documents/docs/api/java.base/java/util/Spliterator.html)  halini verir. |
| SortedSet<E>           | subSet(E fromElement,       E toElement) | Belirtilen iki değer(fromElement, toElement ) dahil olmak üzere arasındaki elemanları verir. |
| SortedSet<E>           | tailSet(E fromElement)                   | Sıralamada `fromElement` değerine eşit ve `fromElement` sonra bulunan elemanları verir. |

> SortedSet  sıralama yapılabilen yapıda olduğu için SortedSet eklenen elemanlar ya Comparable arayüzünü  gerçekleştirmeli  yada SortedSet kurucusuna Comparator arayüzünü yerine getiren (implements)  uygun ara sınıf gecilmelidir.

- Aşağı örnekte SortedSet String türünden değerler(meyveler) ekleyelim. Dikkat String sınıfı Comparable arayüzünü gerçekleştirildiğinden comparator() arayüzü null dönecektir.

```java
public class SortedSetDemo {
        
    public static void main(String[] args) {
        
        SortedSet<String> ss = new TreeSet<>();
        ss.add("Kivi");
        ss.add("Muz");
        ss.add("İncir");
        ss.add("Kayısı");
        ss.add("Elma");
        ss.add("Ananas");
        ss.add("Ananas"); // Tekrar eden eleman eklenemez.
        
        // Sıralamayı yazdıralım
        System.out.println(ss); // [Ananas, Elma, Kayısı, Kivi, Muz, İncir]
        
        // String sınıfı Comparable arayüzü gerçekleştirildiğinden(implement)
        // comparator() null verecektir.
        Comparator c = ss.comparator();
        System.out.println(c); // null
        
        // Sıralamadı ilk elemanı verir.
        System.out.println(ss.first()); // Ananas
        
        // Sıralamadı son elemanı verir.
        System.out.println(ss.last()); // İncir
        
        // Kayısı önce bulunan elemanları verir.
        System.out.println(ss.headSet("Kayısı")); // [Ananas, Elma]
        
        //  Sıralamada Kayısı değerine eşit ve Kayısı'dan sonra bulunan elemanları verir.
        System.out.println(ss.tailSet("Kayısı")); // [Kayısı, Kivi, Muz, İncir]
        
        //  Sıralamada Elma ile Muz (dahil olmak üzere) arasında bulunan elemanları verir.
        System.out.println(ss.subSet("Elma", "Muz")); // [Elma, Kayısı, Kivi]        
    }
}
```

- ***NavigableSet Interface*** : SortedSet miras alarak sıralama üzerinde gezinti yapabilme davranışları( lower, floor, ceiling...) sağlar.

| Modifier and Type | Method                                                       | Description                                                  |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| E                 | ceiling(E e)                                                 | Girilen elemana eşit veya en yakın büyük elemanı verir. Yoksa `null` döndürür. |
| Iterator<E>       | descendingIterator()                                         | Sıralamanın tersi yönünde Iterator nensesi verir.            |
| NavigableSet<E>   | descendingSet()                                              | Sıralamanın tersini verir.                                   |
| E                 | floor(E e)                                                   | Girilen elemana eşit veya en yakın küçük elemanı verir. Yoksa `null` döndürür. |
| `NavigableSet<E>` | headSet(E toElement,        boolean inclusive)               | Sıralamada `toElement` değerinden önce bulunan elemanları verir. `inclusive` **true** ise toElement dahil eder. |
| E                 | higher(E e)                                                  | Girilen elemana  en yakın büyük elemanı verir. Yoksa `null` döndürür. |
| E                 | lower(E e)                                                   | Girilen elemana en yakın küçük elemanı verir. Yoksa `null` döndürür. |
| E                 | pollFirst()                                                  | İlk elemanı alır ve torbadan siler.                          |
| E                 | pollLast()                                                   | Son elemanı alır ve torbadan siler.                          |
| NavigableSet<E>   | subSet(E fromElement,       boolean fromInclusive,       E toElement,       boolean toInclusive) | Belirtilen iki değer(fromElement, toElement ) dahil olmak **(inclusive true ise)** üzere arasındaki elemanları verir. |
| NavigableSet<E>   | tailSet(E fromElement,        boolean inclusive              | Sıralamada `fromElement` değerinden sonra bulunan elemanları verir. `inclusive` **true** ise `fromElement` dahil eder. |

```java
public static void main(String[] args) {
        
        NavigableSet<Double> ns = new TreeSet<Double>();
        
        ns.add(2.0);
        ns.add(2.3);
        ns.add(4.0);
        ns.add(3.0);
        ns.add(6.2);

        // Sıralamayı yazdıralım
        System.out.println(ns); // [2.0, 2.3, 3.0, 4.0, 6.2]

        // Sıralamanın tersi yönünde İterator nesnesi verir.
        Iterator<Double> i =ns.descendingIterator();
        while (i.hasNext()) {
            System.out.print(i.next()+", "); // [6.2, 4.0, 3.0, 2.3, 2.0]    
        }
        // Sıralamanın tersini verir.
        System.out.println(ns.descendingSet()); // [6.2, 4.0, 3.0, 2.3, 2.0]
        
        
        // 2.1 eşit veya en yakın büyük değer
        System.out.println(ns.ceiling(2.1)); // 2.3
        
        // 2.1 eşit veya en yakın küçük değer
        System.out.println(ns.floor(2.1)); // 2.0
        
        // 4 en yakın büyük elemanı verir.
        System.out.println(ns.higher(4d)); // 6.2
        
        // 4 en yakın küçük elemanı verir.
        System.out.println(ns.lower(4d)); // 3.0
        
        // 4 en yakın küçük elemanı verir.
        System.out.println(ns.lower(4d)); // 3.0
        
        // 3 den küçük elemanları verir.
        System.out.println(ns.headSet(3d, true)); // true 3.0 dahil  [2.0, 2.3, 3.0]
        System.out.println(ns.headSet(3d, false)); // false 3.0 dahil değil [2.0, 2.3]
        
        // İlk elemanı alır ve torbadan siler.
        System.out.println(ns.pollFirst()); // 2.0 ve torbadan siler.
        System.out.println(ns);             // [2.3, 3.0, 4.0, 6.2]
        
    }
}
```

### How to Add Native Object in HashSet and Constructor

TreeSet koruculara göz atalım. Daha sonra kullanıcı tarafından oluşturan doğal sıralama özeliliği bulunmayan nesnelerin nasıl TreeSet'de kullanılacağından bahsedelim.

| Constructor                                 | Description                                                  |
| ------------------------------------------- | ------------------------------------------------------------ |
| `TreeSet()`                                 | Torbaya eklenecek elemanlar(Data,String ...) doğal sıralamaya sahipse kullanılır. |
| `TreeSet(Collection<? extends E> c)`        | Comparable arayüzünü yerine getirmiş torba ekleyerek yeni TreeSet üretme. |
| `TreeSet(Comparator<? super E> comparator)` | Comparable arayüzünü yerine getirmeyen sınıfın komparatörü(comparator) (ara sınıf) geçilerek yeni boş TreeSet üretme. |
| `TreeSet(SortedSet<E> s)`                   | SortedSet eklerer  yeni TreeSet üretme.                      |

- SortedSet  sıralama yapılabilen yapıda olduğu için SortedSet eklene elemanlar ya Comparable arayüzünü  gerçekleştirmeli  yada SortedSet kurucusuna Comparator arayüzünü yerine getiren (implements)  uygun ara sınıf geçilmelidir.

- ***TreeSet eklenecek değerler kullanıcı tarafında oluşturulmuş ise TreeSet kullanabilmesi için ya `Comparable` arayüzünü gerçekleştirilerek `compareTo()` metodu ezilmeli yada `Comparator` arayüzü yerine getiren bir ara sınıf  oluşturup `compare()` metodu ezilmelidir(overriding).***

- ***Ayrıca aynı eleman kontrolünün yapılabilmesi için `equals` ve `hashCode` metotları ezilmelidir.***
-  `equals`  true döndüren nesnelerin compare() veya compareTo metotları 0 döndürülmelidir iki nesne aynı olduğu anlaşılsın.
- Comparable arayüzü yerine getiren örnek: compareTo metodu öğrenci no'ya göre ayarlandı.
  - Öğrenci no büyük ise 1, küçük ise -1 ve aynı ise 0 değeri dönderir.

```java
public class Student implements Comparable {

    private String name;
    private int no;

    public Student(String name, int no) {
        this.name = name;
        this.no = no;
    }
    @Override
    public int hashCode() {
        return no;
    }
    @Override
    public boolean equals(Object o) {
        if (o == this)
            return true;
        if (o == null)
            return false;
        if (!(o instanceof Student))
            return false;
        // Öğrenci no.suna göre karşılaştırma
        Student s = (Student) o;
        if (s.no != no) {
            return false;
        }
        return true;
    }
    // compareTo öğrenci noya göre düzenlendi.
    @Override
    public int compareTo(Object o) {
        Student other = (Student) o;
        int r = 0;
        if (no == other.no)
            r = 0;
        else if (no < other.no)
            r = -1;
        else
            r = 1;
        return r;

    }
    @Override
    public String toString() {
        return "Student [name=" + name + ", no=" + no + "]";
    }
}
```

- Test Sınıfı:

```java
public class TreeSetDemo {
    public static void main(String[] args) {

        Set<Student> ts = new TreeSet<>();
        Student s1 = new Student("Ali K.", 1);
        ts.add(s1);
        Student s2 = new Student("Veli Z.", 4);
        ts.add(s2);
        Student s3 = new Student("Seda Y.", 3);
        ts.add(s3);
        Student s4 = new Student("Seda Y.", 3); // Tekrar eden eleman eklenemez.
        ts.add(s4);
        // Yazıdıralım
        System.out.println(ts); // [Ali K., no=1], [name=Seda Y., no=3], [name=Veli Z., no=4]
    }
}
```

- Comparator metodu öğrenci no'ya göre ayarlandı.  arayüzü yerine getiren örnek: StudentComparator ara sınıf oluşturalım.Comparator metodu öğrenci no.ya göre ayarlandı.

```java
public class StudentComparator implements Comparator{

    @Override
    public int Comparator(Object o1, Object o2) {
        // Gerçek tipi dönülmesi
        Student s = (Student) o1;
        Student s2 = (Student) o2;
        int r = 0;
        if (s.getNo() > s2.getNo() ) {
            r = 1;
        } else if ((s.getNo() < s2.getNo() )) {
            r = -1;
        }
        return r;
    }    
}
```

- Student sınıfını yeniden yazmıyorum. Student sınıfındaki Comparable arayüzü gerçekleşmediğini yani comparaTo metoduna sahip olmadığını varsayalım.
- Test Sınıfı Comparator parametre geçerek TreeSet örneğini yazalım.

```java
public class TreeSetDemo {
    public static void main(String[] args) {
        // StudentComparator TreeSet gecelim.
        Set<Student> ts = new TreeSet<>(new StudentComparator());
        
        Student s1 = new Student("Ali K.", 1);
        ts.add(s1);
        Student s2 = new Student("Veli Z.", 4);
        ts.add(s2);
        Student s3 = new Student("Seda Y.", 3);
        ts.add(s3);
        Student s4 = new Student("Seda Y.", 3); // Tekrar eden eleman eklenemez.
        ts.add(s4);
        // Yazıdıralım
        System.out.println(ts); // [Ali K., no=1], [name=Seda Y., no=3], [name=Veli Z., no=4]    
    }
}
```

### HashSet vs TreeSet

- İki yapıda tekrar eden elemanlar bulunmaz.

-  Kullanılacak verilerde  sıralama önemliyse TreeSet kullanılır. Aksi halde HashSet tercih edilir. Unutmayalım ki HastSet O(1) TreeSet O(lgn2) göre çok daha hızlıdır. Veriler büyüdükçe HastSet daha iyi performans verecektir.

|                       | add      | contains | next     |
| --------------------- | -------- | -------- | -------- |
| HashSet               | O(1)     | O(1)     | O(h/n)   |
| LinkedHashSet         | O(1)     | O(1)     | O(1)     |
| CopyOnWriteArraySet   | O(n)     | O(n)     | O(1)     |
| EnumSet               | O(1)     | O(1)     | O(1)     |
| TreeSet               | O(log n) | O(log n) | O(log n) |
| ConcurrentSkipListSet | O(log n) | O(log n) | O(1)     |

***h is the table capacit***