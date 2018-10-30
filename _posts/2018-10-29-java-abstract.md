---
title: "Java Soyut Sınıf ve Metot Kavramı"
last_modified_at:
categories:
  - java
tags:
  - java  abstract class and method
  - java  soyut sınıf
  - java soyut metot
toc: true
toc_sticky: true
toc_label: "Java Abstract"
author_profile: True
---

Miras konusunda işçi sınıfını ve işçi sınıfından türeyen/miras alan çırak kalfa ve usta sınıfını ürettik.Ama işçi sınıfın nesnesi hiçbir zaman üretilmedi, zaten gerek yoktu.

Şablon/Kalıp görevi gören, nesnesi hiçbir zaman üretilemeyen sınıflara soyut sınıf(***abstract class***) denir.

Diğer bir nokta ise işçi sınıfında gerçekleştirilmiş([implementation](https://baykoch.github.io/blog/java/java-method/#kod-blo%C4%9Fu-code-implementation)) bir metot işçi sınıfını miras almış bütün sınıflar tarafından eziliyor(*[overrriding](https://baykoch.github.io/blog/java/java-inheritance/)*) ise işçi sınıfının davranış gerçekleştirmesine(*implementation*) gerek yoktur. Sadece arayüz (*[interface](https://baykoch.github.io/blog/java/java-method/#i%CC%87mza-signature-ve-aray%C3%BCz-interface)*) sağlamak yeterlidir. **Arayüz sağlamak, soyut yapmak demektir.** Soyut metotların(***abstract method***) kod bölümü yoktur. Noktalı virgül `;` ile biter.

- Soyut metotlar ancak soyut sınıflarda olabilirler.
- Soyut sınıfta hiçbir soyut metot bulunmayabildiği gibi istenildiği kadar soyut metot bulunabilir.
- Soyut metotlar devraldığı her alt sınıf tarafından kesinlikle ezilmelidir(*[overriding](https://baykoch.github.io/blog/java/java-inheritance/)*) yani davranışı yerine getirmelidir.
- Eğer devralan sınıf soyut metotları yerine getirmiyorsa(*implement*) kendiside soyut sınıf olmak zorundadır.
- Miras hiyerarşisinde soyut sınıfı(*örnekte işçi*) devralan sınıfın(*çırak*) soyut metotları yerine getirmesi durumda o sınıfı miras alan sınıfların(*kalfa veya usta sınıfı*) yerine getirmesi artık zorunlu değildir. İsterse yerine getirebilir.
- Soyut sınıfların her metodu soyut metot olmak zorunda değildir.
- Soyut metotlar sadece `public` ve `protected` olabilir; `final`,  `private`, `static` ve`synchronized` olamazlar. Çünkü  `final` veya `private` gibi metotlar ezilemezler.  Soyut sınıf istisna olarak statik `main` metodu içerebilir.
- Soyut sınıflar `final` olamaz. Çünkü `final` sınıflar devranılamaz.
- Soyut sınıfların nesnesi üretilemediğinden kurucuya sahip olamaz.

```java
public class Usta extends İşçi {

    public static void main(String[] args) {        
        // Soyut sınıfın nesnesi üretilemez.
        // İşçi p = new İşçi(); // Hata! Cannot instantiate the type İşçi
        Usta usta = new Usta(); // Soyut sınıfı miras alan sınıfların nesnesi üretilebilir.
    }    
    // Soyut metotlar devralan alt-sınıf tarafından ezilmesi/yerine getirmesi(implement zorunludur.
    @Override
    protected void work() {
        System.out.println("Usta çalışıyor.");

    }
}
// Soyut sınıf
abstract class İşçi {
    // Soyut metotlar ancak soyut sınıflarda bulunur.
    protected abstract void work();
    // Soyut sınıflarda davranışı yerine getirmiş(implement) metot veya metotlar bulunabilir.
    protected void info() {
        System.out.println("Gerçekleşmiş metot.");
    }
    // Soyut metotlar private,static ve synchronized olamazlar.
    //    private abstract void pMethod();// Hata!
    //    public static abstract void sMethod();// Hata!
    //    public synchronized abstract void synMethod();// Hata!
    
    // Soyut sınıf istisna olarak statik main metodu içerebilir.
    public static void main(String[] args) {}
    
}
// Soyut sınıf final olamaz.
// final abstract class İşçi {} // Hata!
```

**Neden soyut sınıf kullanırız?**

- Sınıf nesnesini  üretmek istemediğimiz veya üretmeye gerek olmadığı zaman.
  - Soyut sebze sınıfı ve onu miras alan sebze çeşitleri (domates,havuc...)
  - Soyut işçi sınıf ve onu miras alan çırak,kalfa,usta...
  - Soyut öğrenci sınıf ve onu miras alan ilkokul,ortaokul öğrencileri....
- Sınıfın metotları implement  gerek olmadığı zaman.
  - İşçi sınıfına work() metodun implement etmeye gerek yoktur. Çünkü çırak kalfa ve usta farklı işler yapmaktadır.
