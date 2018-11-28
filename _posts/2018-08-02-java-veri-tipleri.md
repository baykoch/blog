---
title: "Java Veri Tipleri"
last_modified_at:
categories:
  - java
tags:
  - java data type
  - java primitive
toc: true
toc_sticky: true
toc_label: "Java Data Type"
author_profile: True
---

Java değişkenlerin tiplerinin belirtilmesi zorunludur. Yani Python diline munhasır şekilde bir değişken oluşturup, ilk başta sayı atayıp sonra metin atamayız. Java'da veri tipleri 3 başlık altında toplanır:

{% include figure image_path="/assets/images/java-type.png" alt="data type" caption=""%}

## Basit Veri Yapıları
Basit tipler karmaşık olmayan `class and interface`’lerden türetilmeyen tiplerdir. Atomik yapıda, başka değişkenlerden türetilmemiştir. Bellek kullanımı  azdır. Array gibi yapılar ile birlikte kullanıldıklarında referans yani karmaşık tiplere göre daha hızlıdırlar. Sekiz adet olan basit tiplerin karmaşık tipleri vardır. Bunlara sarmalanmış yapılar olarak bilinir. Mesela sık kullanılan `**String**` tipi bir karmaşık tiptir. `String` `char` basit tipini üzerine inşa edilmiştir.

**Pratik Bilgi:**
​    "Karmaşık tiplerde değerin adresini tutarken, basit tiplerde ve String tipinde değerin kendisini tutar" gibi düşünülebilir.
{: .notice--info}

```java
char turkLira; // Değişken tanımlandı. Değer atanmadı.
int cityCode;  // Değişken tanımlandı. Değer atanmadı.
Human refOne;  // Referans tanımladı. Herhangi bir nesneye bağlanmadı.
        
turkLira = '₺'; //Değer atandı. değişken '₺' değerini tutuyor.
cityCode = 25;  //Değer atandı. değişken 25 değerini tutuyor.
refOne = new Person("Nadi", 20); //Referans nesneye bağlandı. Nesnenin adresini gösteriyor.
System.out.println(refOne);     //Nesne adresi: "baykoch.javase.b1.Human@5c8da962"
```

### Boolean
Mantıksal veri tipleridir. Önermelerde veya bayrak durumlarını kontrol etmek için kullanılır. `True` ve `False` olmak üzere 2 değerine sahiptir.

### byte
8 bit işaretli değişkendir.1 bir işareti artı veya eksi, 7 bit ile sayının değeri belirlenir. Bellek kullanım miktarının önemli olduğu yazılımlarda veya sayıları sınırlamak istendiği durumlarda tercih edilir.

### short  
16 bit ifade edilir. Byte kullanımı bilgi az bellek gerektiren durumlarda kullanılır.

### int
Programlarda en çok kullanılan tip olan `int` 32 bit ile ifade edilir. En sağdaki bit işaret biti olmak üzere  diğer 31 bit  -2^31 ile  2^31 arasında tam sayı değerlerlerini ifade edebilir. Java Se 8 sonra number sınıftan türetilmiş sınıf hali olan **Integer** tipinde işaretsiz metotlar eklenmiştir. İleri konularda sarmalanmış veri tiplerinden bahsedilecektir.

Hex,octal ve binary sayıları göstermek için aşağıda belirtilen notasyonları kullanılır.

- Hex     : `0x`
- Octal   : `0`
- Binary  : `0b`

Örnek olarak `64` sayısının farklı sayı sistemlerinde kullanımı gösterilmektedir.

```java
int intValue = 64;      // onlu sistemde            : 64
int binInt = 0b1000000; // ikili sistemde           : 64
int ocInt = 0100;       // sekizli sayı sistemi     : 64
int hexInt = 0x40;      // onaltılı sayı sisteminde : 64
```

### long

64 bit ile ifade edilir.Sayı belirtmek için sayın sonuna `L` eklenir.

### float and double

Float 32 bit ve double 64 bit ile ifade edilir. Daha çok kesinlik gerektiren  işlemlerde kullanılır. Ondalık sayılar Java'da her zaman `double` olarak kabul edilir.Bu yüzden  karışıklıkları önlemek, işlem hatalarını aza indirmek için  `long`, `float`, `double` gibi tiplerin sonlarına sayının tipini belirlemek için sırayla `l` ,`f`,`d` harfleri eklenebilir.

```java
double d;
d = 8 / 3;  // Sonuç 2.0
d = 8d / 3; // Sonuç 2.6666666666666665

float pi = 3.14;  // Hata ondalık sayılar her zaman double'dır.
float pi = 3.14f; // `f` ile sayının float olduğu belirtildi.

// Sayının tipini belirtilmesi
double kimlikNo = 12_141_516_400;  //(int) out of range hatası  
double kimlikNo = 12_141_516_400D; //Sayın tipini d belirtme
```
Okunabildiği attırmak sayılar arasında `_` alt-tire kullanılabilir.  

- Noktadan önce veya sonra  
- Farklı sayı türlerini belirtmek için kullanılan `0x,0b, 0` önce veya sonra  
- Sayısal değerin türünü belirtmek için kullanılan `l` ,`f`,`d` önce veya sonra  
- Sayısal değerin  sonunda  

`_` alt-tire kullanılmaz.

```java
// Hatalı alt-tire kullanımları
float piNumber = 3_.1415F;
float piNumber2 = 3._1415F;
int hexN = 0_x52;
int hexN = 0x_52;
long socialSecurityNumber1 = 999_99_9999_L;
int lastPre = 52_;
```
#### IEEE 754

Bilgisayar biliminde sayılar IEEE 754 standartlarına göre ifade  edilir. IEEE 754 bazı sayı göstermede bazı kısıtlamalara sahiptir. Yani `0` ve `2^−126` arasındaki sayılar gösterilemez. Bu aralıkta yapılan işlemlerde hata alınabilir.

```java
double ieee = 0.1 * 3 - 0.3;
System.out.println(ieee); // işlemin sonucu neden "0" değil?
```

Real time, sağlık veya fınans küsuratların çok önemli olduğu işlemlerde bu gibi hatalar ölümcül olabilir. Bilgisayarın doğasından kaynaklanan kısıtlamaları aşmak için `BigDecimal` sınıfı yazılmıştır. Bu sınıf ile bir sayının ondalık kısmını sınırlama, hangi basamakta aşağı veya yukarı yuvarlama işlemine karar verme gibi bir çok işlem yapılabilir.   `BigDecimal` sonra bahsedeceğiz.

### char

16 bitlik unicode biçiminde tanımlanmıştır.

```java
// TL simgesi unicode
char turkLiraUnicode = '\u20BA'; // u20BA = ₺
char turkLira = '₺';
```
Basit veri tiplerinin kapsam aralıkları:

| Type    | Size in Bytes                    | Range                                                   |
| ------- | -------------------------------- | :------------------------------------------------------ |
| byte    | 1 byte (8 bit)                   | -128 to 127                                             |
| short   | 2 bytes (16 bit)                 | -32,768 to 32,767                                       |
| int     | 4 bytes (32 bit)                 | -2,147,483,648 to 2,147,483, 647                        |
| long    | 8 bytes (64 bit)                 | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| float   | 4 bytes (32 bit)  *IEEE 754*     | ±3.40282347E+38F                                        |
| double  | 8 bytes (64 bit)  *IEEE 754*     | ±1.79769313486231570E+308                               |
| char    | 2 byte                           | 0 to 65,536 (işaretsiz)                                 |
| boolean | Uzunluğu sanal makineye bağlıdır | true or false                                           |

### Final Keyword

`Final` anahtar kelimesinin bir  çok kullanım tipi vardır. `Final` anahtar kelimesi ile tanımlanmış bir değişkene ilk değer ataması yapıldıktan sonra değiştirilemez.

```java
final float pi = 3.14f;
pi = 3.145f;           //Hata The final local variable pi cannot be assigned
```

## Karmaşık Veri Tipleri

Karmaşık veri tipleri  sınıftan veya arayüz üretilir.  Aynı sınıf veya arayüzden üretilen tipler ayni tipe sahiptir.   Bellekte belirli bir alanı tutan nesnelere onun referansı ile ulaşılır. Referans bir bakımı eve yani nesneye ulaşmamızı sağlayan sanal adrestir.   C dilinde işaretçi ‘pointer’  fiziksel  adresi belirlerken Java’da referans  fiziksel adresi belirtmez.  

- Bir nesnenin birden fazla referansı olabilir.  

  ```java
  // Ali nesnesine refOne veya refTwo referansı ile ulaşabilir.
  Human refOne = new Human("Ali", 23);
  Human refTwo = refOne;
  ```

- Bir nesne aynı anda sadece bir referans tutar.

- Bir nesnenin referansı kaybolursa nesneye ulaşılamaz.

   ```java
   Person refOne = new Person("Ali", 23);
   Person refTwo = new Person("Veli", 23);
   refOne = refTwo;  // Ali nesnesine artık ulaşılamaz.
   ```

- Basit tipler ve `String`tipi  değiştirebilir `Mutable` tiplerdir. -`String` hariç- Basit ve `String` değişkenlerin yapılan işlemler sonucunda nesne yeniden üretilir.

  ```java
  String mutableString = "Java";
  mutableString = mutableString.concat("Se");  // "JavaSE" nesne katarı üretildi
                  
  int mutableInt = 78;
  mutableInt = mutableInt + 2; //80 değeri üretildi.
  ```

  Peki, `78` ve `Java` değişkenlerine ne oldu? Bu değişkenler *Java Garbage Collection* tarafında imha edildi.

- Karmaşık tipler değiştirebilir `Immutable` tiplerdir. Karmaşık nesne üzerinde herhangi bir işlem yeniden nense üretmez. Kendi üzerinde güncellenir.

  ```java
  Person refOne = new Person("Ali", 25); // Ali kişisi oluşturuldu ve refOne bağlandı
  Person refTwo = refOne; // refTwo Ali nesnesine bağlandı.
  refTwo.setName("veli"); //Ali nesnesinin ismi Veli olarak güncellendi.
  System.out.println(refOne.getName()); // "Veli" aynı nesneyi işaret ediyor.
  System.out.println(refTwo.getName()); // "Veli" aynı nesneyi işaret ediyor.
  ```

  {% include figure image_path="/assets/images/java-ref.png" alt="java type" caption=""%}

Java üretilen değişkenlere ilk değer ataması `initialization` yapılması zorunlu değildir. Java derleyici `initialized`  edilmemiş değişkenlere `default` değer atar.  

**Not:**
Initialization: ilk değer ataması yapmaktır.
{: .notice--warning}

| Veri Tipi              | İlk Değer  |
|------------------------|------------|
| byte                   | 0          |
| short                  | 0          |
| int                    | 0          |
| long                   | 0L         |
| float                  | 0.0f       |
| double                 | 0.0d       |
| char                   | '\u0000'   |
| boolean                | false      |
| String (or any object) | null       |

Eğer referans değeri koparılmış yanı değeri `null` olan bir karmaşık nesneye ulaşmak istediğinizde hata `java.lang.NullPointerException` alırız.

```java
Person refOne = new Person("Ali", 20); //Bir kişi üretildi ve refOne referansına bağlandı.
refOne = null;                         //Referans adresini kopardık.

System.out.println(refOne);            // Referans değeri `null`
System.out.println(refOne.getAge());   // Hata! refOne artık nesnenin adresini göstermiyor.
```

## Scope (Kapsam)

Bir değişkenin ulaşılabilirlik alanı onun kapsamını belirler. Üstlendikleri rol bakımında Java’da değişkenler 3 ayrılır.  

1. Nesne Değişkenleri (object variables)
2. Sınıf Değişkenleri (class variable)
3. Yerel Değişkenleri (local variable)

Javada aslında `global` değişkeni kavramı yoktur, üye değişkenleri  vardır. Nesne ve sınıf değişkenlerine `member or instance variable` üye değişkenleri denir. Bu değişkenler bulunduğu sınıf içinde `global` dır. İleride daha detaylı bir şekilde bahsedeceğiz, şimdilik `member variable` kısaca biraz bahsedelim.  

Sınıf bir şablon olduğunu ve sınıftan türetilen `object` nesne ile hayat bulduğundan bahsetmiştik. Üretilen bir nesnenin durumunu ifade eden `attribute` özelliklerin tümüne nesne değişkenleri denir. Nesne değişkeninin kapsamı önüne aldığı kısıtlayıcı göre belirlenir.  

Sınıf değişkenleri üretilen nesneye bağlı değildir. Üretilen tüm nesneleri temsil eder. Sınıf değişkenleri tanımlama da bir çok amaç olabilir. En basitinden bir nesneden kaç tane üretildiğini bulmak için kullanılabilir.

```java
public class Person {
    //Sınıf değişkeni
    public static int countPerson; // Üretilen toplam nesne sayısı
    //Nesne değişkenleri
    private String name;          
    private String surname;
    private String adress;
    private int age;

    public Person() {             // Default nesne kurucu
        countPerson++;            // Her nesne üretildiğinde bir arttır.
    }
    
}    
```

Main test metodu yazalım.

```java
Person ali = new Person();  // 1. nesne
Person veli = new Person(); // 2. nesne
        
System.out.println(Person.countPerson); // = 2, iki tane nesne oluşturma.
```

### Yerel Değişkenleri (local variable)

Yerel değişkenliği metotların içinde tanımlanan değişkenlerdir. İsimlendirme kurallarında metot için de tanımlanan değişkenin isminin üye değişkeni ile aynı olmasının sakıncalı bir yaklaşım olduğundan bahsetmiştik. Bu gibi bazı püf noktaları sıralayalım.

- Bir bloğun alt kapsamlarında aynı isimde değişken tanımlanamaz.

   ```java
   int localOne;    
   for (int i = 0; i < 3; i++) {
       i++;
       int localOne;   // Hata! bloğun alt bloğunda aynı değişken tanımlanamaz.
   }
   ```

- Aynı seviyedeki bloklar içinde aynı  isimde değişken tanımlanabilir.

  ```java
  for (int i = 0; i < 3; i++) {  // for içinede `i` değişkeni tanımlanmış   
      ...
  }
  while (localOne > 0) {         // Aynı seviyedeki while içinde `i` tanımlanabilir.      int i;
  }
  ```

- [Java başlama sırası](https://baykoch.github.io/blog/java/java-initializing/#ba%C5%9Flatma-s%C4%B1ras%C4%B1-initialization-order):

  ```java
   private static int localOne = 4;      // 1.instance(sınıf değişkeni) variable
   
   public static void main(String[] args) {
       
       System.out.println(localOne);     // 2. print = 4
        int localOne = 7;
           
        if (localOne != 0) {
             System.out.println(localOne); // 3. print = 7
        }
        scopeOne();         // 4. `scopeOne` metodu cağrılıyor.
        scopeTwo(localOne); // 5. `scopeTwo` metoduna `localOne` değişkeni gönderiliyor.
   }
   
   public static void scopeOne () {
        System.out.println(localOne);  // 6. print = 4
   }
   
   public static void scopeTwo (int localOne) {
        System.out.println(localOne); // 7. print = 7
   }    
  ```

  >4<br/>7<br/>4<br/>7



## Tip Çevrimleri (Type Conversion)

 Farklı türde tipleri birbirine dönüştürülmesine tip çevrimi denir. Java kuvvetli tipli dil olduğunda her türlü çevirime izin vermediği gibi çevrim işleminde birçok kontrol yapar. Karmaşık tiplerde çevrimleri OOP kısımlarından bahsederken değineceğiz. Bu seviyede karmaşık tiplerde çevrimleri anlatmak mantıksız olacaktır.  

 Basit tiplerde çevrimle devam edelim. 3 türlü tip çevrimi vardır.

1. İmkansız Çevrim
2. Daraltan Çevrim (Narrowing)
3. Genişleten Çevrim (Widening)

```java
boolean impossible = 0;       // imkansız çevrim
double wide = 173.2f;            // genişleten çevrim float to double
float narrow = wide;           // daraltan çevrim, double to float bilgi kaybı olabileceğinden hata verecektir.   
float narrow = (float) wide; //Ancak kullanıcının `cast`, yani zorlaması ile yapılabilir.
```



 `Boolean` tipinde arasında bir çevrim imkansızdır. Benzer şekilde `short` ve  `byte` ile `char` arasında çevrim olmaz. `Char` işaretsiz, `short` ve `byte` işaretlidir.

 Tamsayılar rasyonel sayılara çevrilebilirler.    

 Genişleten `wide conversion` çevrimlerde kullanıcının `cast` yapmasına gerek yoktur. Genellikle bilgi kaybı da olmaz. Genellikle diyoruz çünkü bazı durumlarda olabilir.  

{% include figure image_path="/assets/images/java-type-conversion.png" alt=" type conversion" caption=""%}

 Kırmızı ile gösterilen yerlerde bilgi kaybı olabilir.

1. Maksimum `int` sayısını `float`a çevirme yaparken ondalık sayı kısımları kaybolur.

2. `long` 64 bit uzunlukta olduğundan  32 bit `float` çevirmede veri kaybı olur.
3. Maksimum `long` sayısını `double` tipine çevrim yaparken ondalık sayı kısımları kaybolur.

```java
int intMax = 2_147_483_647;
float lossPrecisionFloat = intMax;   //Son 2 basamak bilgi kaybı oldu. ...47 to ...50
System.out.println("int to float  :"+lossPrecisionFloat); //2.14748365E9
        
long longMax = 9_223_372_036_854_775_807L;
lossPrecisionFloat = longMax;        //Son 10 basamakta yuvarlama yapıldı. ...720.236.854.775.807 to ...720.000.000.000
System.out.println("long to float  :"+lossPrecisionFloat); //9.223372E18

double lossPrecisionDouble = longMax; //Son 4 basamakta yuvarlama yapıldı. ...75.807 to 76.000
System.out.println("long to double  :"+lossPrecisionDouble); //9.223372036854776E18    
```

 Daraltan çevrimler bilgi kaybı yaşatacağı için doğrudan değişkenleri birbirine eşitleyerek yapılmaz. `Cast` yani dönüşüm işlemine tabi tutulmalıdır.

```java
float pi = 3.14f;
int piNarrow = (int) pi;   //Ondalık kısım 0.14 kayboldu.
System.out.println(piNarrow);  // 3
```
