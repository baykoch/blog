---
title: "Apache Commons Collection Kütüphanesi"
last_modified_at:
categories:
  - java
tags:
  - java Bag nedir
  - java BidiMap nedir
  - java MapIterator nedir
  - Apache Commons Kütüphanesi nedir
toc: true
toc_sticky: true
toc_label: "Commons Collections"
author_profile: True
---

Apache Commons yaralı faydalı kütüphaneler sunan yapıdır. Text işlemeden XML işlemeye, matematik modüllerinden geometri modüllere kadar bir çok alanda yazılmış kütüphane(*library*) dosyalarına sahiptir.

Bu yazımıza Java Collection yapısına ek yapılar sunan kütüphaneden([Commons Collections](https://commons.apache.org/proper/commons-collections/)) bahsedelim. Commons Collection onlarca yapı ve fonksiyon vardır. Bazıları:

| Yapı        | Tanım                                            |
| ----------- | ------------------------------------------------ |
| Bag         | Envanter yapısı sunar.                           |
| BidiMap     | Çift yönlü map yapısı sunar.                      |
| MapIterator | Java Map üzerinden direk iteratör almayı sağlar. |

### Bag

Bir üründen birden fazla olduğu yapılardır. Depo, envanter sepet gerektiren durumlarda kullanılır.

Bir depoda bulunan kitapları gösterelim.

 ```java
import org.apache.commons.collections4.Bag;
import org.apache.commons.collections4.bag.HashBag;

public class BagDemo {

    public static void main(String[] args) {
    
        // Sadece kitap alabilen Bag oluşturma.
        Bag<Book> depo = new HashBag<>();
        // Kitap nesnelerini üretme.
        Book b = new Book("Karamazov Kardeşler", "Dostoyevski" , 1866);
        Book b2 = new Book("Hacı Murat", "Tolstoy" , 1917);        
        // Depoya kitap ve sayılarını ekleme.
        depo.add(b, 100);
        depo.add(b2, 150);
        
        System.out.println(depo); // [100:Kitap ismi= Karamazov Kardeşler,150:Kitap ismi= Hacı Murat]
        // Depodan 75 tanesini silme.
        depo.remove(b2, 75);
        
        System.out.println(depo); // [75:Kitap ismi= Hacı Murat,100:Kitap ismi= Karamazov Kardeşler]
    }

}
class Book {
    String name;
    String authorName;
    int releaseYear;

    public Book(String name, String authorName, int releaseYear) {
        this.name = name;
        this.authorName = authorName;
        this.releaseYear = releaseYear;
    }

    @Override
    public String toString() {
        return "Kitap ismi= " + name;
    }
}
 ```

### BidiMap

Çift yönlü anahtarı ver, değeri al; değeri ver anahtarı al yapısına sahiptir. Ayrıca inverseBidiMap alınarak anahtar-değer yönü değiştirebilir.

```java
import org.apache.commons.collections4.BidiMap;
import org.apache.commons.collections4.bidimap.TreeBidiMap;

public class BidiMapDemo {

    public static void main(String[] args) {
        
        BidiMap<Integer, String> p = new TreeBidiMap<>();
        
        p.put(1, "Adana");
        p.put(25, "Erzurum");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");
        // Anahtar ve değer çift yönlü ulaşma
        System.out.println(p.get(25));  // Erzurum
        System.out.println(p.getKey("İstanbul")); // 34
        // Yadırma
        System.out.println(p);
        // Anahtar-değer yönün değiştirme
        BidiMap<String, Integer> p2 = p.inverseBidiMap();
        System.out.println(p2);    

    }
}
```

### MapIterator

Map üzerinden ancak Set ile sadece anahtar değerlerine ve Map.Entry ile hem anahtar hem değer nesnelerine geçiş sınıf yardımı vasıtasıyla iteratör yardımı ile sırayla ulaşılabilir . **MapIterator** yapısı ile Map üzerinden direk iteratör alınabilir.

```java
import org.apache.commons.collections4.IterableMap;
import org.apache.commons.collections4.MapIterator;
import org.apache.commons.collections4.map.HashedMap;

public class MapIteratorDemo {

    public static void main(String[] args) {

        IterableMap<Integer, String> p = new HashedMap<>();

        p.put(1, "Adana");
        p.put(25, "Erzurum");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");

        // Map.Entry ile ara geçiş sınıfı kullanılarak iteratör alma.
        Set s = p.entrySet();
        Iterator i = s.iterator();

        while (i.hasNext()) {
            Map.Entry<Integer, String> mp = (Map.Entry) i.next();
            int plaka = (int) mp.getKey();
            String şehir = (String) mp.getValue();
            System.out.println(plaka + "-" + şehir);
        }
        
        // MapIterator ile direkt iteratör alma.
         MapIterator<Integer, String> mi = p.mapIterator();
        
         while (mi.hasNext()) {
            
             Object key = mi.next();
             Object value = mi.getValue();
             System.out.println("key: " + key);
             System.out.println("Value: " + value);
          }
    }
}
```





