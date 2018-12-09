---
title: "Java Operatör Kavramları "
last_modified_at:
categories:
  - java
tags:
  - java operator
  - java bitwise
  - java Arithmetic
  - java Logical
toc: true
toc_sticky: true
toc_label: "Java Operator"
author_profile: True
mathjax: true
---

 

Operator bir veya daha fazla girdi üzerinde işlem yapan buna mukabil bir sonuç üreten sembollerdir. Java 3 çeşit operatör vadır.

1. Tekli (*unary*) Operatör
   - Atama (*Assingment*) Operatörü

  2. İkili (*binary*)  Operatör
     - Aritmetik (*Arithmetic*) Operatörler
     - Kıyaslama (*Relational*) Operatörleri  
     - Bitwise Operators  
     - Matıksal (*Logical*) Operatörler
     -  Instanceof Operatörü

  3. Üçlü (*ternary*)  Operatör
     - Conditional Operator  

### Atama (*Assingment*) Operatörü

 Java diline en basit ve en temel operatördür. Yazılımcılar genellikle `eşittir` ile ifade eder. Sağdan sola doğu atama yapılır.  

```java
double pi = 3.14;          // Değer ataması
char turkLira = '₺';       // Değer ataması
boolean calculate = (x + y) / z && (y + z) / x && (x + z) / y; // Karmaşık ifade
Person ali = new Person(); //Refarans ataması
```


### Aritmetik (*Arithmetic*) Operatörler  

 Aritmetik operatörler matematiksel işlemlerde kullanılırlar.   Java’da Aritmetik Operatörler: ***Toplama, Çıkarma, Çarpma ,Bölme, Modül İşlemi, Bir attırma veya azaltma***  

```java
int x = 7;
int y = 3;
int result;

result = x + y; // Toplama      = 10
result = x - y; // Çıkarma      = 4
result = x / y; // Bölme        = 2
result = x * y; // Çarpma       = 21
result = x % y; // Modül İşlemi = 1
result = x++;   // Bir attırma  = 8
result = x--;   // Bir azaltma  = 6
```

Modul işlemi ek olarak ondalik sayılarda işlem yapabilir.

```java
double kalan = 0.8 % 0.3;
System.out.println(kalan); // 0.2....7
```

Attırma `++` ve Azaltma `--` operatörü işlenen değerin öncesinde veya sonrasında kullanılabilir.  Öncesinde kullanılırsa ilk başta cebir işlemi yapılır ve sonra atma işlemi yapılır. Sonrasında kullanılırsa ilk başta atama işlemi yapılır, sonrasında cebir işlemi yapılır.

```java
int x = 7;
int y = ++x;  // x = 8 ve y = 8
int z = x++;  // x = 9 ve z = 8  Dikkat! ilk atama işlemi yapıdı.

x = 7;
y = --x;      // x = 6 ve y = 6
z = x--;      // x = 5 ve z = 6  Dikkat! ilk atama işlemi yapıdı.        
```



Attırma ++ ve Azaltma -- operatörü ilgili diğer bir nokta ise aritmetik yüksetme işlemine tabi tutulmazlar.
{: .notice--danger}


#### Aritmetik Yükseltme

Aritmetik operatörler yaptıkları işlem sonucunda en az int türünde değer üretir. Yani int daha küçük tipler olan short ve byte işlem yapılırken cast yapılmak zorundadır. Aşağıdaki gibi bir işlem hata verecektir.

```java
short x = 2;
short y = 3;
short result = x + y; // Hata! Operatörler en az int tipinde değer üretir.
x = -x;               // Hata! X değerini + veya - yapmak dahi en az 'int' değeri üretir.
x = +x;                // Hata!
short result = (short) x + y;  // x + y sonucu int tipinde olduğu için `cast` yapılmalıdır.
```

`int` tipinden daha büyük tipler  ile yapılan işlemlerde ise:

1. En az bir `double` tip varsa sonuç operatör `double` sonuç üretir.

   ```java
   double x = 3.14D;
   float y = 3F;
   var result = x + y; // var'ın tipi double'dır.    
   ```

2. `double` tip yoksa ve en az bir `float`  varsa sonuç  `float`  olur.

   ```java
   float x = 3.14F;
   int y = 3;
   var result = x + y; // var'ın tipi float'tır.    
   ```

3. `float` tip yoksa ve en az bir `long`  varsa sonuç  `long`  olur.

   ```java
   long x = 1231L;
   int y = 3;
   var result = x + y; // var'ın tipi long'dur.    
   ```
4. `int`  veya `int`' den küçük tiplerin (*Short ve Byte*) üzerinde yapılan cebir işlemi `int` tipinde değer üretir.

### Kıyaslama (*Relational*) Operatörleri

Kıyaslama operatörleri 6 tane olup 4 tanesi sadece  sayısal değerler (*byte, short, int, long, float, double*) üzerinde işlem yapar.

 Sayısal değerler üzerinde işlem yapan operatörler.

| Operatör |                          Açıklama                           | Örnek (x = 3, y =2) |
| :------: | :---------------------------------------------------------: | :-----------------: |
|    >     |      Sağdaki sayısal değer soldaki değerden büyük mü?       |    (x > y)  true    |
|    <     |      Sağdaki sayısal değer soldaki değerden küçük mü?       |   (x < y)  false    |
|    >=    | Sağdaki sayısal değer soldaki değerden büyük veya eşit  mi? |    (x >= y) true    |
|    <=    | Sağdaki sayısal değer soldaki değerden küçük veya eşit  mi? |   (x <= y) false    |


```java
Random r = new Random(); // Rastgele nesnesi oluşturuldu.
        
int x = r.nextInt(99);  // x ve y'e 0 ile 99 değer arasından rastgele bir sayı seçildi.
int y = r.nextInt(99);
        
System.out.println("x is "+ x +", y is "+y); // x ve y'nin değeri
System.out.println("x > y is "+ (x > y));    // x büyük mü y'den?
System.out.println("x < y is "+ (x < y));    // x küçük mü y'den?
System.out.println("x >= y is "+ (x >= y));  // x büyük veya eşit mi y'den?
System.out.println("x <= y is "+ (x <= y));  // x küçük veya eşit mi y'den?
```
`char` tipinde iki karakteri karşılaştırabiliriz. Böyle bir karşılaştırmada her karakterin `unicode` sayısal değeri karşılaştırılır.

```java
char a = 'a'; // a'nın unicode değeri = U+0061
char b = 'b'; // b'nin unicode değeri = U+0062
System.out.println("a > b is "+ (a > b)); // false
```
Diğer kalan 2 operatör **eşit mi?**  `==` ve **farklı mı?** `!=`  operatörüdür. Yukarıda tabloda gösterilen operatörlerin aksine sayısal verilen yanında **referans** ve **boolean** üzerinde de işlem yapabilir.

| Operatör |                 Açıklama                  | Örnek (x = 3, y =2) |
| :------: | :---------------------------------------: | :-----------------: |
|    ==    |  Sağdaki değer soldaki değerden eşit mi?  |   (x == y) false    |
|    !=    | Sağdaki değer soldaki değerden farklı mı? |    (x != y) true    |

```java
Random r = new Random(); // Rastgele nesnesi oluşturuldu.
        
int x = r.nextInt(99);  // x ve y'e 0 ile 99 değer arasından rastgele bir sayı seçildi.
int y = r.nextInt(99);

System.out.println("x == y is "+ (x == y));  // x eşit mi y'e?
System.out.println("x != y is "+ (x != y));  // x farklı mı y'den?
        
//Boolean değerlerde işlemler
boolean isTrue = true;
boolean isFalse = false;
System.out.println("isTrue == isFalse is "+ (isTrue == isFalse));  //false
System.out.println("isTrue != isFalse is "+ (isTrue != isFalse));  //true
```

Bir karmaşık tipli nesneler arasında sorgulama yaparsak yanılabiliriz. Çünkü, aslında biz iki nesnenin referansları arasında işlem yaparız. Bu referanslar bir aynı nesneyi göstermediği sürece değerleri aynı olsada farkı nesneleri gösterir.

```java
//Karmaşık nense referanslarının karşılaştırılması
Person person1 = new Person("Ali");  // Ali isimli nesne
Person person2 = new Person("Ali");  // Ali isimli farklı bir nesne
System.out.println("person1 == person2 is "+ (person1 == person2));  // Değerleri aynı olmasına rağmen farklı nesneleri gösteriyor.
System.out.println("person1 != person2 is "+ (person1 != person2));  // True
```

###  Yeniden Yükleme (*OverLoading*)

 `Overloadling` yeniden yükleme operatörün farklı görevlerde kullanılmasını demektir. Java en bariz `overloading` operator `+` artıdır. Cebir işlemlerin yanında iki  `string` değeri birleştirme `concat` işleminde kullanılabilir.

```java
int x = 6;
int y = 3;
System.out.println("x + y = "+ (x + y)); // x + y = 9
System.out.println("x + y = "+ x + y);   // x + y = 63
        
String text = "Merhaba";
text = text + " Dünya";  
System.out.println(text); // "Merhaba Dünya"
```

> Bitwise  ve Mantıksal işlemlerde bir operatöre (`&`, `|`) farklı anlam yüklendiğini unutmayalım.

### Mantıksal (*Logical*) Operatörler

Mantıksal operatörler sadece boolean tipler üzerinde işlem yaparlar.

| Operatör | Açıklama            | Örnek (x = true, y = false) |
|----------|---------------------|-----------------------------|
| &        | AND işlemi          | x & y = false               |
| \|       | OR işlemi           | x \| y = true               |
| ^        | XOR işlemi          | x ^ y = true                |
| !        | NOT (Zıtlık) işlemi | !x = false, !y = true       |
| &&       | Kestirme AND işlemi | x && y = false              |
| \|\|       | Kestirme OR işlemi  | x \|\| y = true              |

```java
boolean x = false;
boolean y = true;
        
System.out.println("x & y is "+ (x & y));          // AND işlemi
System.out.println("x | y is "+ (x | y));          // OR işlemi
System.out.println("x ^ y is "+ (x ^ y));          // XOR işlemi
System.out.println("!x is "+ !x + ", !y is "+ !y); // NOT (Zıtlık) işlemi
```

`&&` ve `||` kestirme işlemlerdir. İki değer koşulu sağlamayan veya sağlayan bir değer bulduğunda ikinci değere bakılmaz. `&` ve `|`operatörlerden farklarını anlamak için  aşağıdaki örneği inceleyelim.

```java
public static void main(String[] args) {
    //AND ilk değer uymasa bile ikinci değer kontrol ediliyor.
    if ((numberOne() == 5) & (numberTwo() == 3)) {}  // Printed "numberOne","numberTwo"
    // ilk değer uymuyor zaten, ikinci değer kontrol edilmiyor.
    if ((numberOne() == 5) && (numberTwo() == 3)) {} // Printed "numberOne"
    
    // OR ilk değer uysa bile ikinci değer kontrol ediliyor.
    if ((numberOne() == 7) | (numberTwo() == 3)) {}  // Printed "numberOne","numberTwo"
    // ilk değer uyduğu için ikinci değer kontrol edilmiyor.
    if ((numberOne() == 7) || (numberTwo() == 3)) {} // Printed "numberOne"
    
    
}
    
public static int numberOne() {
    int x = 7;
    System.out.println("numberOne");
    return x;
}
public static int numberTwo() {
    int x = 5;
    System.out.println("numberTwo");
    return x;
}
```
> Sonuç olarak hız açısından `&&` ve `||` operatörleri tercih edilmelidir.

### Bitsel (*Bitwise*) Operatörler

Bit bazında işlem yapan bu operatörler genellikle gömülü sistemlerde kullanılır. Öncelikle operatörleri işlem tablosuna bakalım.

{% include figure image_path="/assets/images/java-bitwise.png" alt="Bitwise" caption=""%}

İkili sistemde negatif sayılar **İkinin Tümleyeni (Two’s Complement)** şeklinde gösterilir.  *Two’s Complement* adımları:

1. Sayının tersini alınır. (*one's complement*)
2. Tersi alınmış sayıya `1` eklenir.

   ```mathematica
   0000 0010 = 2
   1111 1101 = one's complement
           1
   +--------
   1111 1110 = -2 (two's complement)
   ```

Kaydırma işlemine geçmeden önce and, or , xor ve~ ile ilgili bir örnek yapalım. Yukarıdaki işlem tablosuna bakarak sonuçları test edebilirsiniz.

```java
int x = 43;  // 0b0010 1011
int y = 25;  // 0b0001 1001
System.out.println("x & y = "+ (x & y)); // AND işlemi = 9   = 0b0000 1001
System.out.println("x | y = "+ (x | y)); // OR işlemi  = 59  = 0b0011 1011
System.out.println("x ^ y = "+ (x | y)); // XOR işlemi = 50  = 0b0011 0010
System.out.println(" ~x   = "+ (~x));    // "~" işlemi = -44 = 0b1101 0100 (+44 Two's Complement)
```

`~x` neden `-44` olduğunu açıklayalım.

```mathematica
0010 1011 =  x (43)
1101 0100 = ~x bu sayı -44 eşittir.

Şimdi -44 sayısını hesaplayalım ve karşılaştırma yapalım.
0010 1100 = 44

1101 0011 = ~44 (one's complement)
        1
+--------
1101 0100 = -44 (two's complement)
```
#### Birleşik (Compound) Atama Operatörü

Birleşik atamalar daha az kod yazmak için geliştirmiş yapılardır.

| Operator | Kullanım Şekli | Açıklama     | Denk işlem   |  Örnek (x = 7,y = 3)  |
|----------|----------------|------------------------------------------|--------------|-----------------------|
| +=       | x += y         | x'i y ile toplar, x'e atama yapar.       | x = x + y    | = 10                  |
| -=       | x -= y         | x'den y'i çıkarır, x'e atama yapar.      | x = x - y    | = 4                   |
| *=       | x *= y         | x'i y ile çarpar, x'e atama yapar.       | x = x * y    | = 21                  |
| /=       | x /= y         | x'i y ile böler, x'e atama yapar.        | x = x / y    | = 2                   |
| %=       | x %= y         | x'i y'den kalanı bulur, x'e atama yapar. | x = x % y    | = 1                   |
| <<=      | x <<= 2        | x'i 2 bit sola kaydırma, x'e atama yapar.  | x = x << 2   | = 28                  |
| >>=      | x >>= 2        | x'i 2 bit sağa kaydır, x'e atama yapar.  | x = x >> 2   | = 1                   |
| &=       | x &= 2         | Bitwise AND işlemi ve x'e atama yapar.   | x = x & 2    | = 2                   |
| ^=       | x ^= 2         | Bitwise XOR işlemi ve x'e atama yapar    | x = x ^ 2    | = 5                   |
| \|=       | x \|= 2         | Bitwise OR işlemi ve x'e atama yapar     | x = x \| 2    | = 7                   |

#### Kaydırma İşlemi (Shift)

Üç tane kaydırma operatörü vardır. İkisi işaretli kaydırma yaparken biri işaretsiz kaydırma yapar. Bir bit sola kaydırma `<<` sayı 2 çarpmak, 2 bit sola kaydırma 3 ile çarpmak ... Benzer şekilde bir bit sağa kaydırma `>>`sayıyı 2'ye bölmek,  2 bit kaydırma ...

>  `>>>` işaretsiz kaydırma yapar.

```java
int x = 24;
System.out.println("x<<1 = "+ (x<<1)); // x = 48
System.out.println("x<<1 = "+ (x<<2)); // x = 96
        
x = 1024;
System.out.println("x>>1 = "+ (x>>1)); // x = 512
System.out.println("x>>2 = "+ (x>>2)); // x = 256

x = -4;
System.out.println("x>>>2 = "+ (x>>>1)); // x = 2147483646
System.out.println("x>>>2 = "+ (x>>1));  // x = -2
```

### Conditional Operator (? :)

Java bununa tek 3'lü operatör alan ifadedir. Eğer ifade doğru ise `?` den sonraki ilk değer, eğer yanlış ise ikinci değer `x` 'e atanır.

> değer x = (ifade) ? eğer ifade doğru ise : eğer ifade yanlış ise

```java
double pi = 3.14;
        
x = (pi == 3.14) ? 15 : 20;    // ifade doğru x = 15
System.out.println("x = "+ x);

x = (pi != 3) ? 15 : 20;
System.out.println("x = "+ x); // ifade yanlış x = 20
```

### Instanceof operatörü

`Instanceof` sadece karmaşık tipler üzerinde, işlem yapar. Kullanım amacı nesnenin hangi karmaşık tipten olduğu kontrol edilir.

```java
Person ali = new Person();
boolean typeTest = (ali instanceof Person); // ali nesnesi 'Person' tipinden mi?
System.out.println(typeTest);               // true
```
### Operatörlerde Öncelik (*Precedence of Java Operators*)
Operatörlerde öncelik, bulunduğu kategori ve değerlendirme sırası `Associativity` göre belirlenir.

```mathematica
x = 7 + 1 / 2        = (7 + (1 / 2)) Öncelik: /,* operatörleri +,- operatöründen önce işlenir.
x = y = z = w        = x = (y = (z = w)) Associativity: Atama operatörü soldan sağa doğru işlenir.
x = y++              = (x = y) then y++  Associativity: ++, -- operatörleri sağdan sola değerlendirildiği için ilk atama yapılıyor.
x = ++y              = (y++) then (x = y)
x = (y < z) ? 2 : 4  = Associativity: Sağdan sola doğru ifade değerlendiriliyor.
```



|        Katagori         |               Operatör               | Değerlendirme Sırası |
| :---------------------: | :----------------------------------: | :------------------: |
|         Postfix         |        () [] . (dot operator)        |     Soldan Sağa      |
|          Unary          |            ++  - -  !  ~             |   **Sağdan Sola**    |
|     Multiplicative      |                 * /                  |     Soldan Sağa      |
|        Additive         |                 + -                  |     Soldan Sağa      |
|          Shift          |            \>>   >>>  <<             |     Soldan Sağa      |
|       Relational        |              \ >=   <=               |     Soldan Sağa      |
|        Equality         |                ==  !=                |     Soldan Sağa      |
|       Bitwise AND       |                  &                   |     Soldan Sağa      |
|       Bitwise XOR       |                  ^                   |     Soldan Sağa      |
|       Bitwise OR        |                  \|                  |     Soldan Sağa      |
|       Logical AND       |                  &&                  |     Soldan Sağa      |
|       Logical OR        |                 \|\|                 |     Soldan Sağa      |
|       Conditional       |                 ? :                  |   **Sağdan Sola**    |
| Assignment and Compound | =  (+= -= *= /= %= >>= <<= &= ^= \|) |   **Sağdan Sola**    |

Dikkat tabloya dikkat edilirse tekli `unary`, şartlı `Conditional`  ve birleşik `Compound` (yukarıda konusu anlatıldı.) hariç diğer tüm operatörler soldan sağa doğru değerlendirilir.

Aşağıdaki kod parçaları her ne kadar mantıklı olmasa da öğrenmek ve örnek teşkil etmesi için maruz görülmeli.

```java
public static void main(String[] args) {
    int y = 16;
    int x;
    x = ( y++ / numberOne() << 1 + 2 == --y  ) ? 47 : 53;
    System.out.println(x);    
}

public static int numberOne() {
    return 8;
}
```



`x = ( y++ / operatör.numberOne() << 1 + 2 == --y  ) ? 47 : 53;` adım adım inceleyim.

1. İlk  dikkat edilecek nokta x'nin değeri şartlı (*Conditional*) ifadeye göre belirlenecek olmasıdır. (Sağdaki ifade doğru ise 47, yanlış ise  53)
2. `.` notasyonu ilk işlenir `operatör.numberOne() = 8 `.  ***(y++ / 8 << 1 + 2 == --y )***
3.  Sonra tabloya göre 16 / 8 = 2 .`y++` ifadesi sağdan işlendiği için attırılmadı.  ***(2  << 1 + 2 == --y )***
4.  Sonra `1 + 2 =3`.  ***(2  << 3 == --y )***
5. Sonra `2 << 3`=16 .  ***( 16 == --y )***
6. Dikkat!  `y++` işleniyor. `y = 17`. ***( 17 == --y )***
7.  Sağdaki işleme geçildi.`--y = 16`. ***( 16  == 16 )***
8.  İfade doğru çıktığı için **x'**in değeri `= 47` olur.

Diğer bir örnek.

```java
public static void main(String[] args) {
    int y = 3;
    int x = 2;
    int result = add(++x , x, y = 4 , y++); //add (3,3,4,4) geçilir. Add İşlemden sonra y değeri bir attırılır.
    System.out.println("x + y + z + w =" + result);  // 14
    System.out.println("x = " + x);                  // 3
    System.out.println("y = " + y);                  // 5

}

public static int add(int x, int y, int z, int w) {
    return x + y + z + w;

}
```

 Diğer bir anlaşılmakta güçlük çekilen `+` operatörünü `overload` olmasından kaynaklanan işlem önceliğidir. Aşağıdaki kodda ilk satırda soldan başladığı için ve `+`'nın solunda string olduğundan string birleştirme yapar.  

```java
System.out.println("TDK" + 2 + 3 ); // TDK23
System.out.println(2 + 3 + "TDK");  // 5TDK
```