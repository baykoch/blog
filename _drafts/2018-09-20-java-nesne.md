---
title: "Java "
last_modified_at:
categories:
  - java
tags:
  - java  
  - java  
  - java 
  - java 
toc: true
toc_label: "Java "
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
## Özellikleri (Attributes)
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