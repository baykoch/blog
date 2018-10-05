---
title: "Java Nesne Değişkenleri"
last_modified_at:
categories:
  - java
tags:
  - java durumu
  - java attribute
  - java sınıf değişkeni
  - java Object Variable
toc: true
toc_label: "Java Attribute"
author_profile: True
---

Javada sınıflar; sınıf değişkenleri,nesne değişkenleri, kurucu metod ve davranış metotlarında oluşur. Zorunlu olmamakla birlikte bileşenlerinin sırası ve diğer özellikleri kabaca aşağıda gösterilmiştir.

```java
<niteleyici> class <Sınıfİsmi> {
 
	<Özellikleri (Attributes)>
	<Kurucu Metot (Contraction Method)>
	<Davranış Metot (Behavior Method)>

}
```
## Özellik (Attribute)
Özellikler sınıfın durumunu(nasıl,ne kadar, hangi vs) tanımladığı için bunların tümüne sınıfın durumu`state` denir. Yani bir `Person()` sınıfın durumu nedir ? Adı soyadı, adresi yaşı ve cinsiyeti gibi
```java
public class Person {
    private String name;
    private String surname;
    private String address;
    private int age;
    private boolean gender;
}
```
Sınıfın özellikleri iki alt başlığa ayrılır ve bu değişkenlerin toplamına üye değişkenleri (members variable), veri üyeleri (data variable) veya alanlar(fields) denir. 

1. Nesne Değişkenleri (*Object Variable*)
2. Sınıf Değişkenleri (*Class Variable*)

### Nesne Değişkenleri (Object Variable)

Nesnelerin özellikleri ifade ederler. Karmaşık veya basit tip olabilirler. Genellikle sınıfın başında tanımlanırlar. İlk değerleri tanımlandığı yerde atanabildiği gibi herhangi bir metod  (genelde kurucu metot) içinde atanabilir. Tanımlandığı yerde `initialization` atama yapmak bu sınıftan oluşturulan her nesne için aynı değer alması anlamına gelir ki pek önerilmez. Zaten ilk değer tanımlandığı yerde atanacaksa `Sınıf değişkenleri` kullanılmalıdır.

### Nesne oluşturmak

Nasıl canlılar anatomik özellikleri dna üzerindeki değerlerden oluşturuyorsa(protein sentezi), program dünyasında nesnelerde sınıflardan oluşturulur. Yani sınıflar birer şablon nesneler ise sınıflardan kılavuz alarak oluşturulmuş varlıklardır. Javada nesneye hayat vermek için, sırayla **referansın tipi** *sınıf ismi* **atama** operatörü( `=`)  *anahtar kelimesi* (`new`) ile **şablon sınıf** belirtilmesi gerekir. Bu adım tek bir satırda yapılabileceği gibi bir adımda yapılabilir. 

> Referans tip nesneİsmi = new ŞablonSınıf();
>
> Person ali = new Person();

Uyarı: Şablon sınıf her zaman referans tipiyle aynı olmayabilir. Daha sonra kalıtım anlatırken bahsedeceğiz. Şimdilik aynı tipte olduğunu kabul edelim.
{: .notice--warning}

```java
Person ali = new Person(); // Tek adımda
Person veli;               // İlk adım: Referans tipi tanımlama
veli = new Person();       // Diğer adımlar: Nesneyi oluşturma ve referansa bağlama
```
Nesnelerin refransı yığın (`stack`)  yaşarken, nesnenin özellikleri öbek (`heap`) yaşar. 
Referanslar ayrık zamanda farklı aynı tipte nesneleri gösterebilir. Bundan dolayıdır ki bir nesneni aynı zamanda birden çok referansı olabilir. Tek bir referans üzerinden yapılan işlemler diğer referanslara da yansır. Referansı koparılan bir nesneye ulaşılamaz ve `JGC` tarafından yok edilir.(Bundan kasıt nesnenin işgal ettiği bellek bölgesi işletim sistemine geri iade edilir.)

Sınıfın özelliklerine `.` notasyonu ile ulaşılır. 

> referans.değişkeninadı
>
> String str = ali.name;

Daha önceki derslerinizde nesnelerin karmaşık tipli olduğu, ilk değer atamazsak bile nesnenin *kararsızlığı önlemek anlamlı hale getirmek için* JVM  ilk değerler atadığından bahsetmiştik. *Nitekim olağan (`default`) değerler atanması nesnenin yeni kullanılmamış yeni olduğunun göstergesidir*. Yerel (`local`) değişkenlere ilk değer atanmaz çünkü **kullan-at** mantığı da çalışırlar.

```java
public class Person {
    
     String name;
     int age;
     public static void main(String[] args) {
        // Kullanıcı değer atamadığı için Jvm olağan (default) değerler atar.
        Person ali = new Person(); 
        String name = ali.name;              // nesnenin özelliğine -bir durumuna- ulaşma
        System.out.println("Name : "+name);  // null
        
    }
}
```
Java olağan (`default` ) değerler tablosu:

| Veri Tipi              | İlk Değer |
| ---------------------- | --------- |
| byte                   | 0         |
| short                  | 0         |
| int                    | 0         |
| long                   | 0L        |
| float                  | 0.0f      |
| double                 | 0.0d      |
| char                   | '\u0000'  |
| boolean                | false     |
| String (or any object) | null      |

Koşulan bilgisayarın donanımına bağlı olarak nesne oluşturmanın sınırı yoktur. İstenildiği kadar nesne oluşturulabilir. Önemli olan her nesnenin bir iş nesnesine karşılık gelmesi, bir anlam ifade etmesidir. Okul hayatını simüle ediyorsak, öğrenci ve öğretmen yanına futbolcu nesnesi oluşturuyorsa bu anlamsız olacaktır.
Diğer bir kıstas ise nesnelerin takibi daha ziyada veritabanı işlemleri için **eşsiz özelliklere** (*primary key*) sahip olması beklenir.

Eğer bir nesnenin özellilerin biri veya birkaçı karmaşık veri tipinden oluşuyorsa bunlara **bileşik nesne** (*compound object*) denir. Bu nesnenin özellikleri aslında referans değerlerdir. En azından karmaşık tipler için böyle diyebiliriz. **Bileşik nesneler** birbirleri üzerinde bulunuyorsa aralarında ***birebir*** ilişki vardır. Birbirlerine *sahiptirler*. ***Birebir*** ilişkide kişi evini biliyor ama ev sahibini bilmiyorsa bu bir hatadır!
```java
public class Person {
	
	 String name;
	 int age;
	 Home myHome;

	public static void main(String[] args) {
		
		Person ali = new Person(); 
		ali.name = "Ali K.";
		ali.age = 21;
		
		System.out.println(ali.myHome); 		 // null, Ali evini bilmiyor.
		
		Home alisHome = new Home();
		alisHome.Address = "219 st...";
		
		
		ali.myHome = alisHome; 					 // Ali evini biliyor
		alisHome.owner = ali;  					 // Ev sahibini biliyor
		
		System.out.println(ali.name);            // Ali K.
		System.out.println(alisHome.owner.name); // Ali K.
		
		alisHome.owner =  null;      			 // Ev sahibini bilmiyor.
		
		System.out.println(ali.name);            // Ali K.
		
		System.out.println(alisHome.owner);      // null, Evin sahibi yok.
		// java.lang.NullPointerException hatası verir. null person() `name` özelliği yok. 
		System.out.println(alisHome.owner.name); 
		
		
	}
}
class Home {
	String Address;
	Person owner;
}
```
Yukarıdaki kod da görüldüğü üzere durum `state` yönetimi çok önemlidir. Eğer aralarındaki ilişki birebir kurgulanmış ise birbirini kesinlikle bilmelidir. Aksi takdirde ölümcül hatalarla karşılaşılabilir.

Özetlersek bir nesne başka nesnelerin özellikleri(attribute) bulunması referans aracılığıyla sağlanır. Bu nesneden aslında bir tane var olup referansı ile birçok yerde ile olabileceğini gösterir. 

> Esasında **nesne-merkezli** yazılımın gayeside budur: Referans üzerinden haberleşen nesneler oluşturmak.

Bir örnek ile nesneler arasında ilişkileri görelim. Basit bir kütüphane kurgulayalım.

- Kütüphane Sınıfı

  ```java
  public class Library {
  
  	String name;
  	Section[] section;
  
  }
  ```

- Bölüm sınıfı

  ```java
  public class Section {
  	
  	String name;
  	Book [] books;
  	
  }
  ```

- Kitap sınıfı

  ```java
  public class Book {
  	
  	String name;
  	Author author;
  	Section section;
  }
  ```

- Yazar Sınıfı

  ```java
  public class Author {
  	
  	String name;
  	Book [] books;
  }
  ```


Dikkat edilirse hemen hemen hepsinin arasında bir bağlantı var. 

1. `Library` ile `section` arasında: **1**’den **N** kadar,
2. `section` ile `books` arasında: **1**’den **N** kadar,
3. `Book` ile `section` arasında: **Birebir**,
4. `Book` ile `author` arasında: **Birebir**,
5. `Author` ile `book` arasına arasında: **1**’den **N** kadar  bağlantı var. 

İki tane kitap nesnesi,  diğer sınıflardan birer nesne oluşturup referans ile  örümcek ağını kuralım.


```java
public class LibraryTest {

	public static void main(String[] args) {

		// Kütüphane nesnesi oluşturuldu.
		Library lib1 = new Library();
		lib1.name = "Halk Kitabevi";

		// Bölüm nesnesi oluşturuldu.
		Section sec1 = new Section();
		sec1.name = "Türk Edebiyatı";

		// Kitap 1 ve 2 nesneleri oluşturuldu.
		Book book1 = new Book();
		book1.name = "Saatleri Ayarlama Enstitüsü";
		Book book2 = new Book();
		book2.name = "Huzur";

		// Yazar nesnesi oluşturuldu.
		Author aut1 = new Author();
		aut1.name = "Ahmet Hamdi Tanpınar";

		// Kütüphane bölümü oluşturuldu ve sec1 bağlandı.
		lib1.section = new Section[2];
		lib1.section[0] = sec1;

		// 1. kitabın yazarı ve bölümü bağlandı.
		book1.author = aut1;
		book1.section = sec1;

		// 2. kitabın yazarı ve bölümü bağlandı.
		book2.author = aut1;
		book2.section = sec1;

		// Yazarın kitapları oluşturuldu ve kitaplara bağlandı.
		aut1.books = new Book[2];
		aut1.books[0] = book1;
		aut1.books[1] = book2;

		// Bölümün kitapları oluşturuldu ve kitaplara bağlandı.
		sec1.books = new Book[3];
		sec1.books[0] = book1;
		sec1.books[1] = book2;

		// lib1.section[0].books[0] ile sec1.books[0] aynı nesneyi gösterir.
		System.out.println("Sonuç = " + (lib1.section[0].books[0] == sec1.books[0]));

		// laut1.books[1] ile sec1.books[1] aynı nesneyi gösterir.
		System.out.println("Sonuç = " + (aut1.books[1] == sec1.books[1]));

	}

}
```

Toplamda beş tane nesne oluşturuldu. Birbirini içeren her bir nesne için yeniden nesne oluşturulamadı. Aralarındaki sahiplik referans ile sağlandı.



