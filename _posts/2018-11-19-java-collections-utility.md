---
title: "Java Collections Utility Sınıfı ve Dönüşümler"
last_modified_at:
categories:
  - java
tags:
  - java Collections metotları nedir
  - java Shuffle metodu nedir
  - java list dizi dönüşümü
toc: false
toc_sticky: false
toc_label: "Java Collections"
author_profile: True
---

**Collections Utility** Sınıfı torba yapıları üzerinde kullanışlı ekstra  davranışlar sağlar.  **Java SE 11** itibariyle **65** tane davranışa sahiptir.  

- Metotlar bazıları sadece List,Set ve Map üzerinde çalışabilir.
- **null** collection girilemez. Aksi halde `NullPointerException` fırlatır.

***Max(), Min(), shuffle(), Sort()*** ve ***Fill()*** metotlarına göz atalım.

```java
public class CollectionsDemo {

    public static void main(String[] args) {

        int[] array = { 2, 3, 4, 3, 5, 1 };
        List l = new ArrayList();
        for (int i = 0; i < array.length; i++) {
            l.add(array[i]);
        }
        // Max değeri verir.
        System.out.println(Collections.max(l)); // 5
        // Min değeri verir.
        System.out.println(Collections.min(l)); // 1
        // Listeyi Karma
        Collections.shuffle(l); // [4, 2, 1, 3, 5, 3]
        // Listeyi küçükten büyüğe doğru sıralar.
        Collections.sort(l); // [1, 2, 3, 3, 4, 5]
        // Listeyi tek bir nesneyle doldurma
        Collections.fill(l, -1); // [-1, -1, -1, -1, -1, -1]        
    }
}
```

- Bazı metotlar torbanın(map,list ve set) değiştirilemez hali verir.(***unmodifiable***)

```java
public class CollectionsDemo {

    public static void main(String[] args) {

        Map p = new HashMap();
        
        p.put(1, "Adana");
        p.put(25, "Erzurum");
        p.put(34, "İstanbul");
        p.put(27, "Gaziantep");
        p.put(6, "Ankara");
        
        Map up = Collections.unmodifiableMap(p);
        // Map torbası artık değiştirilemez.
        up.put(35, "İzmir");  //Hata! java.lang.UnsupportedOperationException
    }
}
```

- Bazı metotlar torbanın eş zamanlı(***synchronized thread-safe***) halini verir.

### Dönüşümler (Array to list or vice versa)

**Arrays.asList()**: Karmaşık nesne dizileri List haline dönüştür.

- İlkel tipler(int,double...) dizini kendisi bir eleman olarak ekler. Yani dizi bulunan değerleri tek tek eklemez.

```java
public class ConversionDemo {

    public static void main(String[] args) {
        
        // Karmaşık tipli dizileri listeye çevirir.
        String[] meyveler = { "Kivi", "Nar", "İncir" };
        List l = Arrays.asList(meyveler);
        System.out.println(l); // [Kivi, Nar, İncir]
        // Wrap dizi örneği
        Integer[] digits = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        List d = Arrays.asList(digits);
        System.out.println(d);// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
        //İlkel tiplerde dizinin kendisi bir eleman olarak ekler.
        int[] primitive = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
        List p = Arrays.asList(primitive);
        System.out.println(p); // [[I@512ddf17]
    }
}
```

**Object toArray()**: **Collection** üzerinde bulunan metot torbanın **Object**  dizi halini verir.  ***Arrays.copyOf*** metodu kullanılarak ilgili gerçek tipe dönülebilir.

**T[]     toArray( T[] a )**: İlgili nesne tipini ve uzunluğunu parmatre girilerek dizi hali çevrilebilir.

```java
public class ConversionsDemo {

    public static void main(String[] args) {

        Set<String> hs = new HashSet<String>();
        hs.add("Kivi");
        hs.add("Muz");
        hs.add("İncir");
        hs.add("Nar");
        //toArray metodu kullanarak Object diziye çevirme.
        Object[] m =  hs.toArray();
        System.out.print("toArray() :");
        for (int i = 0; i < m.length; i++) {
            System.out.print(" "+m[i]);
        }
        // Object String gercek tipine dönülmesi
        String[] realType = Arrays.copyOf(m, m.length, String[].class);
        
        //toArray(T[] a) metodu kullanılarak diziye çevirme.
        String[] s = (String[]) hs.toArray(new String[hs.size()]);
        System.out.print("\ntoArray(T[] a) :");
        for (int i = 0; i < s.length; i++) {
            System.out.print(" "+s[i]);
        }
    }
}
```


