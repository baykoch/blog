---

title: "Java Erişim Belirleyiciler"
last_modified_at:
categories:
  - java
tags:
  - java erişim belirleyiciler
  - java private
  - java public
  - java default
toc: true
toc_sticky: true
toc_label: "Java "
author_profile: True
---

Erişim belirleyiciler konusuna detayına girmeden önce, neden erişim belirleyiciler var konusunu irdeleyelim. Java’ya giriş dersimizden programlamanın aslında bir soyutlama olduğu ifade edildi. Peki, soyutlamayı nasıl sağlayacağız?  Evet Sarmalama (*Encapsulation*) yaparak. Yani sarmalama soyutlamış bilginin gerçekleşmiş veya uygulanmış halidir diyebiliriz.

Peki, nasıl ve neden?

Bir ürünü veya yazılım ancak onun parçaları her ne kadar kendi biliyor ve başkası bilmiyorsa başarılıdır. Bu parçaların birbirinden bağımsız bir şekilde değiştirebileceğini  ve aralarındaki bağımlılığın o kadar az olduğunu gösterir. Böylece yani bir güncellem yapmak yazlımın tamamını değiştirmek zorunda kalmalyız. Sarmala kendini diğerlerinden  gizleme demektir. Bu erişim belirleyiciler vasıtasıyla sağlanır.

İki tür erişim belirleyicisi vardır:

1. Sınıf üye değişkenlerini (*statik ve nesne değişkenleri*) ve metotları niteleyen:`Public`, `Default`(*varsayılan, boş bırakma*), `Protected` ve `Private`
2. Sınıflara erişim (*sınıfın arayüzünü niteleyen*): `Public`, `Default` (Varsayılan,boş bırakma)

### Sınıfın Üye Değişkenlerine Ve Metotlara Erişim (Dört  Yöntem)

***Public*** : Herkes tarafından erişilebilir.

***Default***: Varsayılan olarak bir belirleyici (Public,Protected,Private) yazmamaktır. Bu durumda sadece aynı paket bulunan sınıflar erişebilir. Dikkat! interface kullanılan default anahtar kelimesi ile alakası yok.

***Protected***: Bulunduğu paketteki sınıflar ve kendinden  türeyen (*aynı pakette veya farklı pakette olabilir*) sınıflar erişilebilir(inheritance).

***Private***: Herkese erişim kapalıdır. Sadece sınıfın içinden erişilebilir.

| Erişim Belirleyici (Modifier)                             | private | Default | Protected | Public |
| --------------------------------------------------------- | ------- | ------- | --------- | ------ |
| İç sınıflar (inner class)                                 | Evet    | Evet    | Evet      | Evet   |
| Bulunduğu paketteki sınıflar (Same package class)         | Hayır   | Evet    | Evet      | Evet   |
| Bulunduğu paketteki alt-sınıflar (Same package sub-class) | Hayır   | Evet    | Evet      | Evet   |
| Diğer paketteki sınıflar (Other package class)            | Hayır   | Hayır   | Hayır     | Evet   |
| Diğer paketteki alt-sınıflar (Other package sub-class)    | Hayır   | Hayır   | Evet      | Evet   |

### Sınıflara Erişim  (İki  Yöntem)

***Public*** : Her yerden yani bütün diğer paketlerden(**import** ile) erişilebilir. Bir .java dosyasında sadece bir sınıf public olabilir. Aynı dosya için alt alta yazılmış sınıflardan (*önerilmez*) sadece biri public olabilir.

***Default***: Varsayılan olarak belirleyici (**Public**) yazmamaktır. Bu durumda sadece aynı paket bulunan sınıflar erişebilir. **Dikkat**! *interface* kullanılan ***default*** anahtar kelimesi ile alakası yok.

### Hangi durumlarda tercih edilmeli?

***Public*** : Metotlar nesnelerin arayüzüdür ve bu arayüzle diğer sınıflarla konuşurlar. Yani metotlar genellikle public yapilir(İç çalışma metotları ve pakete üzgü metotlar hariç). Ayrıca static ve final değişkenlerde genellikle public yapilir. Diğer tüm değişkenler private yapılmalıdır. 

***Default***: Aynı pakette herkez tarafından ulaşılabilmesi için varsayılan yapılır. Bunun diğer bir amacı örneğin aynı işlevi yerine getiren metodu farklı sınıflarda tekrar yazılmasını engellemektir. 

***Protected***: Devralan sınıfların ulaşabilecekleri  protected yapılır. Genellikle sınıflar alt-sınıflara sahip olurlar bunun için başta protected yapılması önerilir.

***Private***: Sınıfa ait tüm üyeler ve iç kullanıma ait metotlar private yapilir.

### Örnek

A paketinde A sınıfı:

```java
package baykoch.javase.modifiers.A;

import baykoch.javase.modifiers.B.B;

public class A {
    
    public int x;    // Herkese açık
    int y;             // Sadece aynı paketteki sınıflara açık
    protected int w; // Alt sınıflara açık.
    private int z;     // Herkese kapalı. Kendine açık.
    
    // Herkese açık
    public void publicMethod() {
    }
    // Sadece aynı pakattekileri açık
    void defaultMethod() {
    }
    // Alt sınıflara açık.
    protected void protectedMethod() {
    }
    // Herkese kapalı. Kendine açık.
    private void privateMethod() {
    }
}
```
B paketinde B sınıfından A sınıfına üye değişkenlerine ve metotlarına ulaşmaya çalışalım.
```java
package baykoch.javase.modifiers.B;

import baykoch.javase.modifiers.A.*;

public class B{

    public static void main(String[] args) {
        
        int i;
        A p= new A(); // A(public) her yerden erişilebilir.
        C p2= new C();// Hata! C(default) farkı paketten erişilemez.
        
        i=p.x; // Public ulaşılabilir.
        i=p.y; // Hata! Default farklı pakete olduğu için ulaşılamaz.
        i=p.w; // Hata! Protected aynı sınıftan türememiş ve aynı pakette değil.
        i=p.z; // Hata! Private hiçbir yerden ulaşılmaz.
        
        p.publicMethod();    // Ulaşılabilir(public).
        p.defaultMethod();   // The method defaultMethod() from the type A is not visible (default).
        p.protectedMethod(); // The method protectedMethod() from the type A is not visible (protected).
        p.privateMethod();   // The method privateMethod() from the type A is not visible (private)
        
    }    
}
```

A paketinde C sınıfından A sınıfına üye değişkenlerine ve metotlarına ulaşmaya çalışalım.

```java
package baykoch.javase.modifiers.A;

class C {

    public static void main(String[] args) {

        int i;
        A p = new A();

        i = p.x; // Public ulaşılabilir.
        i = p.y; // Aynı pakete olduğu için ulaşılabilir.
        i = p.w; // Protected aynı pakete olduğu için ulaşılabilir. Fakat aynı sınıfından türememiş.
        i = p.z; // Hata! Private hiçbir yerden ulaşılmaz.

        p.publicMethod();    // Ulaşılabilir(public).
        p.defaultMethod();   // Ulaşılabilir(default).
        p.protectedMethod(); // Ulaşılabilir(protected).
        p.privateMethod();   // The method privateMethod() from the type A is not visible (private)

    }
}
```


