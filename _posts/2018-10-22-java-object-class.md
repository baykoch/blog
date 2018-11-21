---
title: "Java Object Sınıf Metotları"
last_modified_at:
categories:
  - java
tags:
  - java toString  metodu
  - java equals metodu 
  - java hashcode metodu
toc: true
toc_sticky: true
toc_label: "Java Object Class"
author_profile: True
---

Java miras olayına ilk bakış attıktan sonra artık object sınıfından bahsedebilir. Java üretilen her sınıf object sınıfını miras alır. Kullanıcı `extends` etmese bile JVM tarafından otomatik olarak eklenir.

Object sınıfı `java.lang` paketinde bulunur. 11 tane metoda sahiptir ve metotların 6’sı `final` metot olup ezilemez. Diğer 5 metot ezilebilir ve fonksiyonel kullanım için ezilmesi gerekir.
{% include figure image_path="/assets/images/java-object-class.png" alt="Java API" caption="Java SE 11 API'deki Object sınıfının metotlarına bir bakış"%}
Şimdi bu metotların bazılarını farklı senaryo göre inceleyelim.

### to.String()

`to.String()` metodu nesnenin string halini üretir. Eğer ezilmeden kullanılırsa sınıfın bulunduğu paket yani açık adresi (*paket yolu*) ve `@hash` kodunu verir. Hash kod her nesnenin JVM bölgesinde sahip olduğu eşsiz (primary key) anahtardir. 16-bit sistemde kodlanmıştır.

```java
public class Person {

    protected int id;
    protected String name;
    protected String surname;
    protected int age;

    public Person(int id, String name, String surname, int age) {
        this.id = id;
        this.name = name;
        this.surname = surname;
        this.age = age;
    }
    public static void main(String[] args) {

        Person pr = new Person(1,"Veli","Durmuş",37);
        // to.string() metot nesnenın hash kodu eklenmiş açık adresini verir.
        System.out.println(pr.toString()); //baykoch.inheritance.Person@7960847b
        
    }
}
```

`baykoch.inheritance.Person@7960847b`  kullanıcı için anlamsızdır ve sınıf hakkında (*durumları*) bilgi almak için  ezilmesi gerekir.

```java
public class Person {
    protected int id;
    protected String name;
    protected String surname;
    protected int age;

    public Person(int id, String name, String surname, int age) {
        this.id = id;
        this.name = name;
        this.surname = surname;
        this.age = age;
    }
    public static void main(String[] args) {

        Person pr = new Person(1, "Veli", "Durmuş", 37);
        // to.string() çağrısı
        System.out.println(pr.toString()); // Person [id=1, name=Veli, surname=Durmuş, age=37]
    }
    // toString metot nesnenin durumu(state) hakkında bilgi verir.
    @Override
    public String toString() {
        return "Person [id=" + id + ", name=" + name + ", surname=" + surname + ", age=" + age + "]";
    }
}
```

> Person [id=1, name=Veli, surname=Durmuş, age=37]

- **Sınıftan(*class*) bilgi almak için ezilmiş `toString()` metodu bulunmaldır.**

### hashCode()

Hash girilen değeri bir dizi işlemden geçirerek eşsiz sayı üreten foksiyondur. hash foksiyonları genellikle bilgisayar biliminde hashtable veri yapılarında kullanılır. Hashtable hash fonksiyonu ile üretilen sayının denk geldiği indise eklenmesiyle oluşur. Hashtable en önemli özelliği elemanlara ulaşma süresinin  O(1) zamanda gerçekleşmesidir. Java yerleşik bulunan String, Interger , Double ... gibi sınıflar hashCode metotdu ezerek kendi davranışlarını tanımlamışlardır. String  için `s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1]` fonkisyon değeri hesaplanır. 

- Kullanıcı tarafında oluşturulan sınıflar hashCode metodunu ezerek(overriding) hash davranışını belirtmelidir.
- Aşağıdaki kodda bazı değişkenlerin hash kodları (`int, boolean, String` ...) gösterilmiştir.

```java
public class HashDemo {

    public static void main(String[] args) {

       // Boolean değerlerin hash kodu true için 1231 false için 1237'dir.
		boolean b = true ;
		boolean b2 = false;
		Object t = b;  // Hash kodu almak için Object sınıfına cast edelim.
		Object f = b2;
		System.out.println( t.hashCode() ); // 1231
		System.out.println(f.hashCode() ); // 1237
		// int sayıların hash kodu kendisidir.
		int i = 25;
		Object intHash = i;
		System.out.println( intHash.hashCode() ); // 25
		// String değişknelerin hash kodu:
		// s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1] foksiyonuna göre hesaplanır.
		String s = "Türkiye";
		System.out.println(s.hashCode()); // 269050420

    }
}
```

### equals()

İki referans  tipli (*karmaşık*) değişkenin durumları (attributes) karşılaştırmak için kullanılır. `equals` ezilmeden kullanılırsa sadece iki nesnenin referanslarını karşılaştırır.

```java
public class Person {

    protected int id;
    protected String name;
    protected String surname;
    protected int age;

    public Person(int id, String name, String surname, int age) {
        this.id = id;
        this.name = name;
        this.surname = surname;
        this.age = age;
    }
    public static void main(String[] args) {

        Person pr = new Person(1, "Veli", "Durmuş", 37);
        Person pr2 = new Person(1, "Veli", "Durmuş", 37);
        // equals ezilmezse(overriding) sadece referansları aynı olup olmadığı kontrol edilir.
        boolean isEquals = pr.equals(pr2);
        // pr ve pr2 aynı durumlara sahip olsalarda farklı referanslara sahiptirler.
        System.out.println(isEquals); // false
    }
}
```

**Bütün  veya belirli özellikleri karşılaştırılabilmesi için `equals` metodu ezilmelidir(*overriding*).**

> Person sınıfında sadece aynı id sahip nesnelerin aynı nesne olduğunu senaryoya göre kodumuzu güncelleyelim.

```java
public class Person {

    protected int id;
    protected String name;
    protected String surname;
    protected int age;
    
    public Person(int id, String name, String surname, int age) {
        this.id = id;
        this.name = name;
        this.surname = surname;
        this.age = age;
    }
    public static void main(String[] args) {

        Person pr = new Person(1, "Veli", "Durmuş", 37);
        Person pr2 = new Person(1, "Ali", "Durmuş", 31);
        // equals ezilerek id göre karşılaştırma yapılması
        boolean isEquals = pr.equals(pr2);
        System.out.println(isEquals); // True
    }
    @Override
    public boolean equals(Object obj) {
        Person pr2 = (Person) obj;
        boolean isEquals = false;
        if (id == pr2.id) {  // pr.id == p2.id
            isEquals = true;
        }
        return isEquals;
    }
}
```



