---
title: "Java Torba Yapıları: 3.List ve Map Yapısı"
last_modified_at:
categories:
  - java
tags:
  - java List nedir
  - java ArrayList nedir
  - java LinkedList nedir
  - java Stack nedir
  - java Map arayüzü nedir
  - java HashMap nedir
  - java HashTree nedir
toc: true
toc_sticky: true
toc_label: "Java Collection"
author_profile: True
---
List düzenli sıralı nesneler tutan yapılardır. Dizilerden en büyük farkı uzunluklarının dinamik yapıda ve sıra ile ilgili kullanışlı davranışlara sahip olmasıdır.

- Aynı elemandan birden fazla bulunabilir.
  Elemanlar belirli bir sırada bulunur. Herhangi belirli bir indise eleman ekleme veya indisde bulunan elemanı çıkarma/silme işlemi yapabilir.
- List arayüzüne Collection arayüzünden aldığı metotların yanında indis kavramına uygun yeni  ek davranışlar tanımlanmıştır. Bazılarına göz atalım.  

| Modifier and Type  | Method                                             | Description                                                  |
| ------------------ | -------------------------------------------------- | ------------------------------------------------------------ |
| void               | add(int index,    E element)                       | Belirtilen(int index) indise ekleme yapar.                   |
| boolean            | add(E e)                                           | List sonuna ekleme yapar.                                    |
| boolean            | addAll(int index,       Collection<? extends E> c) | Belirtilen indisden itibaren torba eklemesi yapar.           |
| boolean            | addAll(Collection<? extends E> c)                  | Listenin sonu torba ekler.                                   |
| void               | clear()                                            | List elemanları temizler.                                    |
| boolean            | contains(Object o)                                 | Liste belirtilen elemanı içeriyor mu?                        |
| boolean            | containsAll(Collection<?> c)                       | Liste belirtilen torbayı içeriyor mu?                        |
| static <E> List<E> | copyOf(Collection<? extends E> coll)               | Belirtilen torbanın manipülasyon yapılamaz liste halinde verir. |
| E                  | get(int index)                                     | Belirtilen indexteki elemanı verir.                          |
| int                | indexOf(Object o)                                  | Belirtilen eleman hangi indiste? Listede bulunmuyorsa -1 döndürür. |
| boolean            | isEmpty()                                          | Liste boş mu?                                                |
| int                | lastIndexOf(Object o)                              | Belirtilen elemanından en sonda bulunan (tekrar eden eleman) ver? Listede bulunmuyorsa -1 döndürür. |
| ListIterator<E>    | listIterator()                                     | Listenin elemanlarının düzenli sıralı halinin iteratörünü verir. Sağa ve sola gidilebilir. |
| ListIterator<E>    | listIterator(int index)                            | Belirtilen indisted itibaren listenin elemanlarının düzenli sıralı halinin iteratörünü verir. |
| E                  | remove(int index)                                  | Belirtilen indexteki elemanı siler.                          |
| boolean            | remove(Object o)                                   | Belirtilen elemanından ilk bulduğunu siler.                  |
| `boolean`          | removeAll(Collection<?> c)                         | Torbaki elemanrı listeden siler.                             |
| default void       | replaceAll(UnaryOperator<E> operator)              | Fonksiyonel(lambda) ifadenın sonucuna uygun elemanları siler. |
| boolean            | retainAll(Collection<?> c)                         | Liste elemanlardan sadece belirtilen torbadaki bulunan elemanları sakla diğerleri sil. |
| E                  | set(int index,    E element)                       | Belirtilen indexteki elemanı `element` ile değiştir.         |
| int                | size()                                             | List buluna elemanlarının toplam sayısını ver.               |
| default void       | sort(Comparator<? super E> c)                      | Comparator ara-sınıfı geçilerek compare() metodunun davranışına göre sıralama yapılabilir. |
| List<E>            | subList(int fromIndex,        int toIndex)         | Belirtilen aralıklarda alt liste oluşturma.                  |

> Buradaki davranışlar gecekleştirmesi olan  ArrayList,LinkedList sınıfların konusunda örnek verilecektir.

`List` arayüzünü temelde gecekleştirmesi(implements)  3 tane  sınıf vardır. **ArrayList**,**LinkedList** ve Vector. `Vector` miras alan Stack sınıfı bulunur. `Vector` eşzamanlı(synchronized) çalıştırdığı için performans problemine sahiptir. Kullanılabilirlik açısından pek fazla tercih edilmez. `Stack` yapısı her ne kadar list arayünü geçekeştirse yapısı itibariyle kendi özgü yapısı vardır. List üzerinde davranışlar kullanılmaz. İlerde kısaca Stack metotlarından bahsederiz.

### ArrayList ve LinkedList Sınıfları

**Arraylist** dizi dinamik halidir. **LinkedList** bağlı(*double linked list*) listedir. Yani bir eleman sağındaki ve solundaki elemanı bilir. LinkedList kapasite kavramı muğlaktır. Başlangıç kapasitesi verilemez.

 ***ArrayList Kurucuları***:

| Constructor(ArrayList)               | Description                                         |
| ------------------------------------ | --------------------------------------------------- |
| ArrayList()                          | 10 elemanlı boş liste oluşturma.                    |
| ArrayList(int initialCapacity)       | Başlangıç kapasitesi girilerek boş liste oluşturma. |
| ArrayList(Collection<? extends E> c) | Torba geçilerek liste oluşturma.                    |

ArrayList örnekleri:
```java
public class ListDemo {

    public static void main(String[] args) {
        
        int[] array = {2,3,4,3,5,1};
        List l = new ArrayList();
        for (int i = 0; i < array.length; i++) {
            l.add(array[i]);
        }
    
        // Listi yazdıralım.
        System.out.println(l);
        
        // 0 inside -1 ekleme [-1, 2, 3, 4, 3, 5, 1]
        l.add(0,-1);  // [-1, 2, 3, 4, 3, 5, 1]
        
        // 2 indisteki elemanı getirir.
        System.out.println(l.get(2)); // 3
        
        // 3 hangi indiste?
        System.out.println(l.indexOf(3)); // 2
        
        // 0 indiste buluna elemanı sil.
        System.out.println(l.remove(0)); // -1 silindi. [2, 3, 4, 3, 5, 1]
        
        // 0 indiste bulunan 2 -1 ile değiştir.
        System.out.println(l.set(0, -1)); // -1 silindi. [-1, 3, 4, 3, 5, 1]
        
        // Liste boş mu ?
        System.out.println(l.isEmpty()); // False
    
        // 0 ile 2 arasında bir alt-liste oluştur.
        System.out.println(l.subList(0,2)); // [-1, 3]
        
        // Retain list
        List retainList = new ArrayList();
        retainList.add(5);retainList.add(3);
        // Retain 2,3 hariç diğerlerini sil.
        l.retainAll(retainList); // Son hali [3, 3, 5]

        // ListIterator sağa ve sola gidilebilir.
        ListIterator i = l.listIterator();
        i.hasNext();
        System.out.println(i.next());
        i.hasNext();
        System.out.println(i.previous());
        
        l.clear(); // Listeyi Temizler.
    }    
}
```

 ***LinkedList Kurucuları:***

| Constructor (LinkedList)              | Description                      |
| ------------------------------------- | -------------------------------- |
| LinkedList()                          | Boş liste oluşturur.             |
| LinkedList(Collection<? extends E> c) | Torba geçilerek liste oluşturma. |

 **LinkedList** bağlı liste olduğu için bağlığı ilgilendiren birçok davranışa sahiptir. Liste başındakini getirme (getFirst), *sondaki* silme (*removeLast*)... gibi  `api` dokümantasyonu bakılabilir. Bazılarına örnek verelim.

```java
public class LinkedListDemo {

    public static void main(String[] args) {
        
        int[] array = {2,3,4,3,5,1};
        
        LinkedList l = new LinkedList();
        for (int i = 0; i < array.length; i++) {
            l.add(array[i]);
        }
        
        // Listi yazdıralım.
        System.out.println(l);
        
        // Listenin başına ekleme
        l.addFirst(-1); // [-1, 2, 3, 4, 3, 5, 1]
        // Listenin sonuna ekleme
        l.addLast(-1); //[-1, 2, 3, 4, 3, 5, 1, -1]
        
        // Listenin başındaki elemanı getir ve sil
        System.out.println(l.remove()); // -1  l: [2, 3, 4, 3, 5, 1, -1]
        
        // Listenin başına eleman ekleme
        System.out.println(l.offerFirst(1)); // true l:[1, 2, 3, 4, 3, 5, 1, -1]
        
        // Listenin başındaki elemanı getir ama silme
        System.out.println(l.peek()); // 1     
    }
}
```

### ArrayList vs LinkedList

ArrayList performan listesi aşağıdaki gösterilmiştir. Tabloyu yorumlarsak iki belirgin kıstasa göre seçil yapılır.

1. ArrayList elemanı ulaşma O(1) iken LinkedList en kötü durumda O(n)'dir.

2. Eğer sadece listenin sonuna ekleme çıkarma işlemi yapılacaksa Arraylist kullanılmalıdır. Fakat ortaya veya başa eklem çıkarma işlemleri yapılacaksa LinkedList kullanılmalıdır. Çünkü ArrayList x indisine eklem yaptığında x’den sonraki elemanları bir sola kaydırır.

| List       | get  | add  | contains | next | remove(0) | iterator.remove |
| ---------- | ---- | ---- | -------- | ---- | --------- | --------------- |
| ArrayList  | O(1) | O(1) | O(n)     | O(1) | O(n)      | O(n)            |
| LinkedList | O(n) | O(1) | O(n)     | O(1) | O(1)      | O(1)            |

### Stack

Stack son eklenen ilk çıktığı(*Last in-First out*) yapıdır. Birbirinin üstüne istiflenmiş veriler gibi düşünülebilir.  Alt kısımda bulunan verilere erişmek için en sondan(son eklenen) başlayarak sırayla çıkarılır.

Birtane parametre almayan kurucuya sahiptir.

| Constructor | Description          |
| ----------- | -------------------- |
| Stack()     | Boş yığın oluşturur. |

Beş tane kendine özgü davranışa sahiptir. Unutulmamalıdır ki **Stack** her nekadar list gereçleştirese list ait davranışlar yığın yapısı gereğince  kullanışsızdır. Bu yüzden stack api üzerinden işlem yapılmalıdır.

| Modifier and Type | Method           | Description                                                  |
| ----------------- | ---------------- | ------------------------------------------------------------ |
| boolean           | empty()          | Yığın boş mu?                                                |
| E                 | peek()           | Yığının son elemanını(en üstteki) silmeden getir.            |
| E                 | pop()            | Yığının son elemanını(en üstteki) sil ve getir.              |
| E                 | push(E item)     | Yığına eleman ekleme                                         |
| int               | search(Object o) | Yığında bir elemana kaç elemandan sonra ulaşılabilir. Eleman yoksa -1 döndürür. |

Metotlara örnek verelim ve bu kısmı sonlandıralım.

```java
public class StackDemo {
    
    public static void main(String[] args) {
        
        String [] meyveler = {"Muz","Kivi","Nar","Şeftali"};
        Stack s = new Stack();
    
        for (int i = 0; i < meyveler.length; i++) {
            // Yığına eleman ekle.
            s.push(meyveler[i]);
        }
        // Yığını yazdıralım.
        System.out.println(s); // [Muz, Kivi, Nar, Şeftali]
        
        // Yığın boş mu?
        System.out.println(s.empty()); // False
        
        // Son eklenen elemanı getir.
        System.out.println(s.peek()); // Şeftali
    
        // Son eklenen elemanı getir ve sil.
        System.out.println(s.pop()); // Şeftali s:[Muz, Kivi, Nar]
        
        // Kivi'ye kaç eleman sonra ulaşılabilir.
        System.out.println(s.search("Kive")); // 2
    }
}
```

## Map

**Map**(Eşleştirme) bir anahtara bir değer gelecek şekilde dizayn edilmiş veri yapılarıdır. Anahtar ile ilgili veriye ulaşılır.

- Anahtar **Set** nesneleri biçiminde tutulur ve eşsizdir.(Set yapıları tekrar eden yapılara izin vermez.) Değerler ise **Collection** nesneleri biçiminde tutulur ve birden fazla olabilir.

Java SE 11 itibariyle 37 tane metot sahiptir. Bazı temel metotları tablo ile verelim.

| Modifier and Type | Method                                               | Description                                                  |
| ----------------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| boolean           | containsKey(Object key)                              | Belirtilen anahtarı içeriyor mu? True or False               |
| boolean           | containsValue(Object value)                          | Belirtilen değeri içeriyor mu? True or False                 |
| V                 | get(Object key)                                      | Belirtilen anahtar ile eşleşen değeri verir yoksa null geri döndürür. |
| Set<K>            | keySet()                                             | Anahtarların Set halini verir.(Anahtarlar Set nesnesi biçimde tutulur.) |
| V                 | put(K key,    V value)                               | Anahtar ve değer ikilisi ekleme. ***İlgili anahtar ile eşleşen değer varsa yenisi ile değiştirir.*** |
| V                 | remove(Object key)                                   | Anahtara eşleşen değeri siler. Değer bulunmuyorsa null döndürür. |
| default boolean   | remove(Object key,       Object value)               | Değeri silme.                                                |
| default V         | replace(K key,        V value)                       | Değeri güncelleme.                                           |
| default boolean   | replace(K key,        V oldValue,        V newValue) | Anahtar ile eşleşen değeri(oldValue) yeni değer(newValue) ile değiştirir. |
| Collection<V>     | values()                                             | Değerleri torba halini verir.                                |

### HashMap

Map arayüzünü gerçekleştiren sınıflardan en sık kullanılan yapıdır.HashMap map arayüzünde bulunan bütün metotlara sahiptir.

- `null` değerlere ve anahtara izin verir.
- Ekleme çıkarma arama gibi davranışlar ***O(1)*** zaman karmaşıklığına sahiptir.
- Belirli bir sıralama düzenini garanti etmez. Her ekleme işleminde sırası değişebilir.

| Constructor                                           | Description                                                  |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| HashMap()                                             | Yeni boş, 16 elemanlı bir HashMap oluşturma. ***Load factor(0.75)**. |
| HashMap(int initialCapacity)                          | Başlangıç kapasitesi belirtilerek boş HashMap oluşturma. ***Load factor(0.75)**. |
| HashMap(int initialCapacity,        float loadFactor) | Başlangıç kapasitesi ve load factor belirtilerek  boş HashMap oluşturma |
| HashMap(Map<? extends K,? extends V> m)               | Map ekleyerek yeni HashMap oluşturma.                          |

- **\*Load factor:** Doluluk oranı olarak bilinen kıstas, HashMap belirtilen değere (default değer 0.75) ulaştığında kapasitesi 2/3+1 oranında genişler. Örnek vermek gerekirse 16 iken 12 eleman ulaştığında(0.75) kapasite(2/3+1) 25'e çıkarılır.

```java
public class HashMapDemo {

    public static void main(String[] args) {
        
        Map p = new HashMap();
        
        p.put(1, "Adana");
        p.put(25, "Erz");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");
        // Map yazdıralım
        System.out.println(p); // {1=Adana, 34=İstanbul, 6=Ankara, 25=Erzurum, 27=Gaziantep}
        
        // Key karşılık gelen değer silinir. Yoksa null döndürür.
        System.out.println(p.remove(6)); // {1=Adana, 34=İstanbul, 25=Erzurum, 27=Gaziantep}
        
        // Put eğer anahtar ile eşleşen bir değer bulunuyorsa eski değer döndürülür
        // ve yenisi ile değiştirilir. Erz Erzurum ile güncellenmiştir.
        System.out.println(p.put(25,"Erzurum")); // Erz
        
        // Anahtar ile eşleşen değere ulaşma
        System.out.println(p.get(25)); // Erzurum
        
        // Anahtar ile eşleşen değere güncelleme
        System.out.println(p.replace(27,"Antep")); // {1=Adana, 34=İstanbul, 25=Erzurum, 27=Antep}
    
        // Değerden var mı?
        System.out.println(p.containsValue("İstanbul")); // True
        
        // Anahtarları Set aktarma
        Set keySet = p.keySet();
        // Set iterator alıp yazdırma.
        Iterator i = keySet.iterator();
        while (i.hasNext()) {
            System.out.print(" "+i.next());   // 1 34 25 27            
        }
        
        // Değerleri Collection yapısını aktarma ve iterator alma
        Collection l = p.values();
        i =l.iterator();
        while (i.hasNext()) {
            System.out.print(" "+i.next());   // Adana İstanbul Erzurum Antep        
        }                
    }
}
```
### Map.Entry

Map içindeki anahtar-değer çiftleri ile ilgili işlemleri yapan metotlara sahiptir. Map arayüzün üzerinde bulunan `Map.entrySet()` metodundan alınarak anahtar-değer çiftlerine sırayla ulaşılabilir.

| Modifier and Type | Method              | Description                                  |
| ----------------- | ------------------- | -------------------------------------------- |
| boolean         | equals(Object o)  | Belirtilen nesne için eşitlik kontrolü yapar. |
| K               | getKey()          | Anahtar değerini ver.                        |
| V               | getValue()        | Değeri ver.                                  |
| V               | setValue(V value) | Değeri değiştir.                             |

```java
public class MapEntryDemo {

    public static void main(String[] args) {
        
        Map<Integer, String> p = new HashMap<>();
        
        p.put(1, "Adana");
        p.put(25, "Erzurum");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");
        
        Set s = p.entrySet();
        Iterator i = s.iterator();
        
        while (i.hasNext()) {
            // iterator sıradaki çift Entry değeri alınır.
            Map.Entry<Integer, String> mp = (Map.Entry) i.next();
            // Anahtar değerine ulaşma
            int plaka =  (int) mp.getKey();
            // Anahtar ile eşleşen değere ulaşma
            String şehir = (String) mp.getValue();
            System.out.println(plaka + "-" + şehir);
        }
    }
}
```

### TreeMap

TreeMap anahtar verilerine göre elemanları sıralı tutan veri yapılarıdır. SortedMap ve NavigableMap miras alır.

- TreeMap TreeSet gibi Red-Black Tree gerçekleştirmesidir.

- TreeMap `null` değere izin verir. Ama `null` anahtar değerine izin vermez.

- SortedSet sıralama yapılabilen yapıda olduğu için SortedSet eklenen elemanlar ya Comparable arayüzünü gerçekleştirmeli yada SortedSet kurucusuna Comparator arayüzünü yerine getiren (implements) uygun ara sınıf gecilmelidir. TreeSet konusunda bahsedildiği için tekrar etmemek adına örnek vermeyeceğim.

HashMap plaka ve şehir örneği verelim.

```java
public class TreeMapDemo {

    public static void main(String[] args) {
        
        Map p = new TreeMap();
        
        p.put(1, "Adana");
        p.put(25, "Erzurum");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");
        // TreeMap anahtar değerine göre sıralama yapar.
        System.out.println(p); // {1=Adana, 6=Ankara, 25=Erzurum, 27=Gaziantep, 34=İstanbul}                
    }
}
```

### LinkedHashMap

LinkedHashMap ekleme sırasını garanti eder. Elemanları ekleme sırasına göre dizer.

```java
public class LinkedHashMapDemo {

    public static void main(String[] args) {
        // HashMap
        Map<Integer, String> p = new HashMap<>();
        p.put(1, "Adana");
        p.put(25, "Erzurum");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");
        // LinkedHashMap
        Map<Integer, String> l = new LinkedHashMap<>();
        l.put(1, "Adana");
        l.put(25, "Erzurum");
        l.put(34, "İstanbul");
        l.put(27, "Gaziantep");
        l.put(6, "Ankara");
        
        // HashMap eklendiği sırayı korumaz.
        System.out.println(p); // {1=Adana, 34=İstanbul, 6=Ankara, 25=Erzurum, 27=Gaziantep}
        // LinkedHashMap eklendiği sırayı korur.
        System.out.println(l); // {1=Adana, 25=Erzurum, 34=İstanbul, 27=Gaziantep, 6=Ankara}

    }
}
```

### HashMap vs HashTable vs LinkedHashMap vs TreeMap

- **HashMap** *unsynchronized* yapıda iken *HashTable* eşzamanlı(*synchronized*), yapıdadır. Eşzamanlı çalışan yapılar thread lerle birlikte kullanılır ve performans problemine sahiptir.

- **HashMap** null kullanımına izin verir. **HashTable** null anahtar ve değerlere izin vermez.

- **HashTable** pek de iyi olmayan performansa problemine sahiptir. Bu yüzden `thread` yapıları ile kullanılacaksa yerine ***ConcurrentHashMap*** tercih edilmelidir.

- **LinkedMap** `Double List` ve `Map` yapısını birleştiren yapıdır. HashMap'den farkı eleman eklenirken(*put*) eklenme sırası kurur.

- **TreeMap** elemanları anahtar değerine göre sıralı tutar. **HashMap** göre daha erişim pahalıdır.

| Map               | get      | containsKey | next     |
| ----------------- | -------- | ----------- | -------- |
| HashMap           | O(1)     | O(1)        | O(h/n)   |
| LinkedHashMap     | O(1)     | O(1)        | O(1)     |
| ConcurrentHashMap | O(1)     | O(1)        | O(h/n)   |
| TreeMap           | O(log n) | O(log n)    | O(log n) |

- ***h*** : Toplam kapasite
