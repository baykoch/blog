---
title: "Java Sarmalayan Sınıflar ve BigInteger/BigDecimal Kullanımı"
last_modified_at:
categories:
  - java
tags:
  - java wrapper sınıflar
  - java BigInteger nedir 
  - java BigDecimal yuvarlama işlemleri
  - java boxing nedir
toc: true
toc_sticky: true
toc_label: "Java Wrapper"
author_profile: True
---

Wrapper ingilizce sarmalamak, ciltleme anlamı gelir. `Hediye paketi hazırlamak = wrapper gift`

Java 8 tane basit  tipin bulunduğunu bunların detayından burda bahsetmiştik. Sarmalayan (Wrapper) sınıf: basit tiplerin sınıf/nesne halini ifade eder.  İlkel tipler nesne merkezli programlama presibiyle çeliştiği için sarmalayan sınıflar oluşturulmuştur. Torba yapıları gibi birçok alanda kullanılmaktadır.

{% include figure image_path="/assets/images/java-wrapper.png" alt="java" caption=""%}

Sarmalayan sınıfların kurucu metotlarından bahsedilmeyecek çünkü bütün kurucu metotlar modası geçmiştir(**Deprecated**)

***Deprecated***: İlerde kullanımdan kaldırılacak olan kod bölümlerini ifade eder. Deprecated kodlar artık kullanılmamalıdır. Eski kodlara uyumluluğu sürdürmek için durmaktadır.

1. Sarmalatan sınıfların üzerinde bulunan `valueOf` statik metot ile basit tipten sarmayan tipe dönüştürülebilir.

   - Character: Sadece char alır.

   ```java
   Character tl = Character.valueOf('₺'); // char to Character
   ```

   - Boolean: boolean ve String değeri alabilir.

   ```java
   Boolean b = Boolean.valueOf(true);  // boolean to Boolean
   Boolean b2 = Boolean.valueOf("false"); // String to Boolean
   ```

   - Byte: byte ve String değeri alabilir.

   ```java
   byte i = 2;
   Byte byt = Byte.valueOf(i); // byte to Byte
   Byte byt2 = Byte.valueOf("23"); // String to Byte
   ```

   - Short: short ve String değeri alabilir.

   ```java
   short sp = 25;
   Short s = Short.valueOf(sp); // short To Short
   Short s2 = Short.valueOf("25"); // String to Short
   ```

   - Integer:  int ve String değeri alabilir.

   ```java
   int ip = 25;
   Integer in = Integer.valueOf(ip); // int to Integer
   Integer in2 = Integer.valueOf("25"); // String to Integer
   ```

   - Long: long ve String değeri alabilir.

   ```java
   long lp = 25l;
   Long l = Long.valueOf(lp); // long to Long
   Long l2 = Long.valueOf("25");// String to Long
   ```

   - Float: float ve String değeri alabilir.

   ```java
   float fp = 2.71f;
   Float f = Float.valueOf(fp); // float to Float
   Float f2 = Float.valueOf("25");// String to Float
   ```

   - Double: double ve String değeri alabilir.

   ```java
   double dp = 3.14;
   Double d = Double.valueOf(dp); // double to Double
   Double d2 = Double.valueOf("25");// String to Double
   ```

   - Uygun formatta değer girilmezse ` java.lang.NumberFormatException` hatası alınır.

   ```java
   Double d2 = Double.valueOf("hi"); // Hata!
   ```

2. Kutulama(**boxing**) yapılarak.

   - Java 1.5 sonra kurucu ve diğer değer atama metotları kullanılmadan direk atama operatörü kullanılarak basit tipleri sarmalayan nesne haline  getirilmesine kutulama (**auto-boxing**) denir. Benzer işlemle(ters yönde) sarmalayan tipten basit tiplere ise kutudan çıkarma (**auto-unboxing**) denir.

   ```java
   // Boxing
   Character ss = '₺'; // char to Character
   Boolean bb = true;  // ...
   Byte by= 25;
   Short st = 7;
   Integer ii = 25;
   Long ll = 40_535_135L;
   Float ff = 2.71f;
   Double dd = 3.14;
   // Unboxing
   char sp = ss; // Character to char
   boolean bp = bb; // ...
   // ...
   ```

3. Sarmalayan(wrapper) sınıflar  üzerinde bulunan `parse` metotları ile String değerlerden basit tipe çevrilebilir.

   ```java
   boolean b = Boolean.parseBoolean("true"); // String to boolean
   byte by = Byte.parseByte("7");              // String to byte
   short s = Short.parseShort("25");          // ...
   int i = Integer.parseInt("99");
   long l = Long.parseLong("40535135");
   float f = Float.parseFloat("2.71");
   double d = Double.parseDouble("3.14");
   ```

4.  Sayısal değerleri ifade eden (Short,Byte ...) Number miras almıştır. Number sınıfı üzerinden bulunan `intValue,floatValue` gibi metotlar ile sarmalayan sınıfların basit tip değerleri alınabilir. ***Number*** sınıf ile sınırlanrdışmış jenerik yapılarda sıkca kullanılır.

   ```java
   Double wrapD = Double.valueOf(3.14);
   double dp = wrapD.doubleValue();
   double dp2 = Double.valueOf(3.14).doubleValue();
   // ...
   ```

### BigInteger

Basit tipleri arasında en büyük tam sayı long tiptir. 64-bit uzunluğuna sahip olan long yazabileceğimiz en küçük tamsayı `-2^63`  ve en büyük tamsayı ise  `2^63 -1`  dir. Bu değerlerin ne olduğunu, sarmalayan  Long sınıf üzerinde bulunan sınıf değişkneleri yardımı ile görelim.

```java
System.out.println(Long.MAX_VALUE); //(+) 9.223.372.036.854.775.807
System.out.println(Long.MIN_VALUE); // -  9.223.372.036.854.775.808
```

long tamsayı tipinin  alabileceği bu max ve min  aralığı dışındaki tam sayılarla işlem yapmak istersek, ilkel sayı tipleri yetersiz kalacaktır. O nedenle java BigInteger sınıfını kurgulanmıştır. Bu sınıf tam sayılar bir üst-alt sınıra sahip değildir. Ayrıca tam sayılar yapılabilen bütün cebir işlemleri için metotlara sahiptir.

- BigInteger üzerinde bulunan `valueOf` metodu ile long değerler BigInteger çevrilebilir.

```java
BigInteger bInt =BigInteger.valueOf(9_223_372_036_854_775_807L); // long to BigInteger
```

BigInteger kurucusuna String ve byte dizi geçilerek nesnesi üretilebilir.

```java
// Using byte array contractor
byte[] bytes = { 123, 101, 002, 123, 127, 111, 123, 127, 111 }; // byte
byte[] bytesHex = { 0x12, 0x45, 0x25, 0x54, 0x12, 0x45, 0x25 }; // hex
byte[] bytesOct = { 0155, 075, 0125, 0145, 0115, 055, 0152 }; // octal
BigInteger i = new BigInteger(bytes);
System.out.println(i); // 2276228036801320419183
// Using String contractor
BigInteger j = new BigInteger("1232319223372036854775807");
System.out.println(j); // 2276228036801320419183
```

- BigInteger değişmez(immutable) değişkendir. Üzerinde yapılan herhangi manipülasyon işlemi yeni nesne üretilmesine sebeb olur.
- BigIntger *auto-boxing/auto-unboxing* sağlamaz. Number sınıf intValue ile basit tipi alınabilir.

```java
BigInteger x = new BigInteger("7");
// BigInteger to int
int i = x.intValue(); // Ok.
// BigInteger oto kutulama sağlamaz.
int j = x; // Hata!
```

- BigInteger sayılar üzerinde aritmetik (+, -, /, *) ve mantıksal (>. < ...) operatörler kullanılmaz.
- Yukarıdaki hatırlatmayı yaptıktan sonra BigInteger metotlarını kullanarak bazı cebir işlemleri yapalım.

```java
BigInteger x = new BigInteger("7");
BigInteger y = new BigInteger("3");

BigInteger sum = x.add(y);         // Toplama : 10
BigInteger diff = x.subtract(y);   // Çıkarma : 4
BigInteger div = x.divide(y);        // Bölme   : 2
BigInteger multi = x.multiply(y);  // Çarpma  : 21
```

- Bazı bitwise işlemleri:

```java
BigInteger x = new BigInteger("7"); // 111
BigInteger y = new BigInteger("3"); // 011

BigInteger and = x.and(y); // 011
BigInteger or = x.or(y);  // 111
BigInteger xor = x.xor(y); // 100
// ...
```

- EBOB ve modüler aritmetik işlemler yapılabilir.

```java
BigInteger x = new BigInteger("48");
BigInteger y = new BigInteger("24");
BigInteger gdc = x.gcd(y); // EBOB : 24
BigInteger mod = x.mod(y); // MOD  : 0
```

Bahsetmediğimiz  birçok fonksiyonu sahiptir. Api dokümantasyonuna bakabilirsiniz.

### BigDecimal

BigDecimal sınıfı, kesirli sayılarla yapılabilen bütün işlemleri için kurgulanan yapıdır. BigDecimal yazılmasında iki belirgin etken vardır:

1. Bilgisayar biliminde sayılar IEEE 754 standartlarına göre ifade edilir. IEEE 754 bazı sayı göstermede bazı kısıtlamalara sahiptir. Yani 0 ve 2^−126 arasındaki sayılar gösterilemez. Bu aralıkta yapılan işlemlerde hata alınabilir.

```java
double ieee = 0.1 * 3 - 0.3;
System.out.println(ieee); // işlemin sonucu neden "0" değil?
```

2. Çevrim(Cast) işlemlerinde yuvarlamalar yapılarak veri kayıplarına neden olur. Konu detayına [burdan](https://baykoch.github.io/blog/java/java-veri-tipleri/#tip-%C3%A7evrimleri-type-conversion) ulaşabilirsiniz.

Temel kurucuna Double, String, int, long tipinden veya char dizisi geçilerek nense üretilebilir. Ayrıca BigInteger geçilebilir.

```java
BigDecimal fromStr = new BigDecimal("3.14"); // from String
BigDecimal fromInt = new BigDecimal(25);     // from int
BigDecimal fromLong = new BigDecimal(227622803680132041L); // from long
BigDecimal fromDouble= new BigDecimal(3.14d); // from double
BigDecimal fromChar = new BigDecimal(new char[] { '2', '.', '7', '1' }); // from char array
// 100 bit uzunlukta rastgele asal sayı oluştur.
BigInteger bigInteger = BigInteger.probablePrime(100, new Random());
BigDecimal fromBigInteger = new BigDecimal(bigInteger); // from bigInteger
```

`valueOf` metodu ile long  ve double tipinde değer alınabilir.

```java
BigDecimal x= BigDecimal.valueOf(3.14159265); // from double
BigDecimal y= BigDecimal.valueOf(234324234L); // from long
```

- BigDecimal sayılar üzerinde aritmetik (+, -, /, *) ve mantıksal (>. < ...) operatörler kullanılmaz.

- Bazı aritmetik işlemler.

```java
BigDecimal x = new BigDecimal("4.2");
BigDecimal y = new BigDecimal("2.8");

BigDecimal sum = x.add(y);          // Toplama : 7.0
BigDecimal diff = x.subtract(y); // Çıkarma : 1.4
BigDecimal div = x.divide(y);     // Bölme   : 1.5
BigDecimal multi = x.multiply(y);// Çarpma  : 11.76
// CompareTo
System.out.println(sum.compareTo(new BigDecimal("6.0")) == 0);
```

- CompareTo ile karşılaştırma. `(x > y) +1, (x < y) -1 ve (x == y) 0` döndürür.

```java
BigDecimal x = new BigDecimal("4.2");
BigDecimal y = new BigDecimal("2.8");
int r = x.compareTo(y); // +1
```

- Ondalik sayının hassaslığı(pression) , ondalık kısmı(scale) ve sign (a = a / |a|, negatif -1/sınıf 0/pozitif 1)

```java
BigDecimal x = new BigDecimal("123.34244");
System.out.println(x.scale());     // 5  (34244)
System.out.println(x.precision()); // 8  (12334244)
System.out.println(x.signum());       // +1    
```

- Ondalık sayılar sıklıkla finansal işlemlerde yuvarlama sıkça kullanılır. Java 1.9 ile birlikte eski yuvarlama davranışları deprecated olmuştur. Artık `RoundingMode` kullanılmalıdır.
- Enum RadingMode yuvarlama tiplerine göz azalım.

| Enum Constant | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| CEILING       | En yakın büyük sayıya(+sonsuz doğru) yuvarlama yapar.  ( 0.333  ->   0.34, -0.333  ->  -0.33 ) |
| FLOOR         | En yakın küçük sayıya(-sonsuz doğru) yuvarlama yapar.  (0.333 -> 0.33, -0.333 -> -0.34,  2.3 -> 2 ,  -2.3-> -3 ) |
| UP            | Sıfırdan uzaklaş. (3.4 > 4 , -4.5 -> -5 )                    |
| DOWN          | Sıfıra doğru yuvarlama yapar.   (0.333  -> 0.33 , -0.333  -> -0.33, 2.3 ->2 , -2.3 -> 2) |
| HALF_UP       | (0,5 >= x ) yukarıya, (0,5 < x ) aşağıya yuvarlar.  0.5 or 0.6  ->  1.0,  0.4  ->  0.0 |
| HALF_DOWN     | (0,5 < x ) yukarıya, (0,5 >= x ) aşağıya yuvarlar.  0.5 or 0.4 ->  0.0 , 0.6  ->  1.0 |
| HALF_EVEN     | Eşit uzaklıkta(0,5) ise çift sayılara yuvarlanır. (2.5 -> 2, 1.5 -> 2) |
| UNNECESSARY   | Yuvarlama yapma.                                             |

```java
// CEILING
BigDecimal x = new BigDecimal("2.3");
x = x.setScale(0, RoundingMode.CEILING); // 3
// FLOOR
x = new BigDecimal("-2.3");
x = x.setScale(0, RoundingMode.FLOOR); // -3
// UP
x = new BigDecimal("2.3");
x = x.setScale(0, RoundingMode.UP);   // 3
// DOWN
x = new BigDecimal("2.3");
x = x.setScale(0, RoundingMode.DOWN); // 2
// HALF_UP
x = new BigDecimal("2.5");
x = x.setScale(0, RoundingMode.HALF_UP);// 3
// HALF_DOWN
x = new BigDecimal("2.5");
x = x.setScale(0, RoundingMode.HALF_DOWN); // 2
// HALF_EVEN
x = new BigDecimal("7.5");
x = x.setScale(0, RoundingMode.HALF_EVEN); // 8
x = new BigDecimal("6.5"); // 6
x = x.setScale(0, RoundingMode.HALF_EVEN);
```

- İlk girilen parametre hassaslığı ifade eder. 0:sadece tam sayı kısmı, 1:tam sayı ve bir ondalık kısmı 2 :tam sayı ve iki ondalik kısmı ...

```java
// Hassaslığı iki olarak belirtilmesi
x = new BigDecimal("1.235");
x = x.setScale(2, RoundingMode.HALF_EVEN); // 1.24
```


