---
title: "Java Diziler"
last_modified_at:
categories:
  - java
tags:
  - java array sınıfı
  - java multidimensional arrays
  - java diziler
  - java foreach
  - java array metotları
toc: true
toc_sticky: true
toc_label: "Java Arrays"
author_profile: True
---
Java diziler sabit uzunluğa sahip aynı türden (ilk veya karmaşık) elemanların tutulduğu veri yapılarıdır. Diler birer nesnedir ve bir arayüze (metotlara) sahiptir. Bu metotlardan konun ilerleyen evrelerinde bahsedilecek.
Java'da diziler Java'da bulunan diğer veri yapılarına göre  `collections` daha  hızlıdır. Bunun iki temel sebebi vardır.
1. **Homojen:** Aynı türden elemanlardan oluşması.
2. **Statik Yapı:** Uzunluğu sabit olması.
```
Dizinin Tipi  Dizi Belirteçi `[]` Dizinin İsmi;
int [] array;
String array[];
...
```
Diziler çoğul nesneler olduğundan **isimlerininde çoğul** *yazılmasında* fayda var. Dizi belirtecinin`[]` nerede bulunduğu pek önem arz etmez. Dizin boyutları `int` türünde olmalı, ilk tanımlamada veya sonra mutlaka belirtilmelidir.

Uzunluğu belirtilen bir dizin ilk değer ataması yapılmasa bile  `JVM` tarafından `default`  değerler atanır.

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

Dizilere anlamlı değer vermek ilk değerde bırakmamak sağlıklı bir program için önemlidir.

```java
String strArray[] = new String[5]; // Jvm "Null" ataması yapar.
int[] numArray = new int[5];       // Jvm "0" ataması yapar.
Boolean bolArray = new Boolean[2]; // Jvm "false" ataması yapar.
for (int i = 0; i < numArray.length-1; i++) { // Dikkat length-1 !
    System.out.print(strArray[i]);         // Null ...
    System.out.println(numArray[i]);       // 0 ...
    System.out.println(bolArray[i]);       // false false
}
```

Dizilerin hücrelerine indis ile ulaşılır. İndis 0 dan başlar `length-1` 'e kadar devam eder. `length`  dizinin uzunluğunu veren fonksiyondur. Ayrıca dizinin band genişliği dışında bir noktaya ulaşmaya çalışmak **hata** verecektir.  

```java
int[] numArray = {1,2,3,4,5};     // Array = 1 2 3 4 5
int arrayLength= numArray.length; // Index = 0 1 3 4 5 -- 5 tane
System.out.println("Length of array = "+arrayLength); // Dizinini Uzunluğu = 5
// !!!Bazı "ArrayIndexOutOfBoundsException" hataları
System.out.println("ArrayIndexOutOfBoundsException = "+numArray[arrayLength]); // [5] hücresi mevcut değil.
System.out.println("ArrayIndexOutOfBoundsException = "+numArray[-1]);
```

Dizinin uzunluğu ve idis sayısı : `int,shot,byte,char`  olabilir. `int` tipler `float,long,double` olamaz.

```java
// Dizinin uzunluğu "float long double" tipinde olamaz.
long lengthNumber = 10;
int[] digits = new int[lengthNumber]; // Hata !
// Dizinin hücrelerine  "float long double" tipiyle ulaşılamaz.
double indexD = 3.0;
float indexF = 2.0f;
long indexL = 3;
int[] digits = {0,1,2,3,4,5,6,7,8,9};
int a= digits[indexD];  // Hata !
int a= digits[indexF];  // Hata !
int a= digits[indexL];  // Hata !
```

### foreach

Dizinin elemanlarına ulaşmak için `for,while ve do-while` kullanılabilir. Bu döngülerin yanında daha pratik  yapı olan `foreach` tercih edilebilir. for (foreach) yapısı:

```
for ( Dizinin Tipi : Dizinin İsmi) {...}
```
```java
int[] numArray = {1,2,3,4,5};
for (int i : numArray) {   // for dizini uzunluğu kadar yani 5 kez çalışacaktır.
    System.out.println(i); // 1 2 3 4 5
}
```

**Dikkat**  `foreach` yapısının içinde diziyi `initializing` değer atama yapılamaz!

```java
Random r = new Random();
int[] intArray = new int[4];    // ilk değer 0 0 0 0

for (int i : intArray) {
    intArray[i] = r.nextInt(5); // initializing yapılmıyor!
    System.out.println(i);      // 0 0 0 0
}
```

Eğer dizi tanımlandığında  ilk değerler biliniyorsa `{}` arasında yazılabilir.  

```java
char [] currencies = { '₺','£','$' };
int[]      digits = { 0,1,2,3,4,5,6,7,8,9 };
byte [] byteArrays= { 0b0111,0b0101,0b0010 };
String [] elements = { "He","Ne","Ar","Kr","Xr" };
        
Person ali= new Person();
Person veli= new Person();
Person [] people= { ali,veli };      // Complex type array
```

### Çok Boyutlu Diziler (*Multidimensional Arrays*)

Çok boyutlu dizi tek boyutlu bir dizinin her hücresine dizi konularak elde edilir. Benzer işleyişle hücreye konulan dizinin içine bir dizide koyulabilir. Bu yöntemle çok boyutlu diziler elde edilmiş olur.

Tanımlana çok boyutlu dizinin ilk bölümü **kesinlikle** belirtilmelidir. İlk boyutu girilmemiş bir dizinin sonraki boyutları **verilemez**. Çünkü diğer boyuttaki dizilerin uzunlukları farklı olabilir.

```java
int[][] multiIntArrays = new int[3][];                    // ilk boyut belirtilmelidir.
String[][][] multiStringArrays = new String[2][5][10]; // Boyutlar farklı olabilir.
// İlk boyut uzunluğu belirtilmeden diğer boyutların uzunlu girilemez.
char[][] multicharArrays = new char[][3];               // Hata  !!
byte[][][] multiByteArrays = new byte[][][3];           // Hata  !!
String[][][] multiStringArrays = new String[2][][3];   // Hata  !!
short[][][] multiShortArrays = new short[2][3][];      // Doğru !!
```

Diziler referans tipinde olduğundan birbirlerine bağlanabilir.

```java
int[] x = {1,2,3};
int[] y = {4,5,6};
int[] z = {7,8,9};
        
int[][] digits= { x, y, z };
```

## Array Class Methods

`Arrays` sınıfının bazı metotlarını tanıyalım. Metotları `import` yapmadan `java.util.array.Metotİsmi()` şeklinde kullanabilir veya `import java.util.Arrays;` yapıp `Arrays.Metotİsmi()` şeklinde kullanılabilir. Okunabilirlik açısından `import`   tercih edilebilir.

Not:
Dizi işlemlerinde indis değerlerini`length`  ilişkilendirmek hata oranını  aza indirecektir.
{: .notice--warning}


### toString()

Tek boyutlu dizini elemanlarını (`ilkel tipler ve String`) ekrana basar.

```java
String[] students = {"Ali","Veli"};
System.out.println(java.util.Arrays.toString(students)); // [Ali, Veli]
```
`import` ile kullanımı.

```java
import java.util.Arrays;
public class JavaArrays {
    
    public static void main(String[] args) {
        String[] students = {"Ali","Veli"};
        System.out.println(Arrays.toString(students)); // [Ali, Veli]
    }
}
```
### sort()

Diziyi artan düzende sıralama yapar.


```java
int[] digits = { 8, 9, 4, 3, 2, 7, 6, 5, 0, 1 };
Arrays.sort(digits);
System.out.println(Arrays.toString(digits)); // [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

Dizinin belirli bir aralığı sıralanabilir.

```java
int[] digits = { 8, 9, 4, 3, 2, 7, 6, 5, 0, 1 };
Arrays.sort(digits,5,digits.length);  // Son 5 elemanın sıralanması          
System.out.println(Arrays.toString(digits)); // [8, 9, 4, 3, 2, 0, 1, 5, 6, 7]
```

### copyOf() and copyOfRange()

Belirtilen dizini bütün veya belirli bir aralığını farklı bir diziye kopyalar.

```java
int [] digits = { 8, 9, 4, 3, 2, 7, 6, 5, 0, 1 };
int [] copyArray;
// copyOf()
copyArray = Arrays.copyOf(digits, digits.length);
System.out.println(Arrays.toString(copyArray));  // [8, 9, 4, 3, 2, 7, 6, 5, 0, 1]
// copyOfRange()
copyArray = Arrays.copyOfRange(digits,0,(digits.length-5));
System.out.println(Arrays.toString(copyArray));  // [8, 9, 4, 3, 2]
```

### fill()

Dizinin bütün veya belirli bir aralığını  yeni bir değer ile yer değiştirir.

```java
int[] digits = { 8, 9, 4, 3, 2, 7, 6, 5, 0, 1 };
        
Arrays.fill(digits,0 ,3 ,-1);                // 0-3 ile arasını -1 ile doldurur.
System.out.println(Arrays.toString(digits)); // [-1, -1, -1, 3, 2, 7, 6, 5, 0, 1]

Arrays.fill(digits, -1);                     // Dizini hepsini -1 ile doldurur.
System.out.println(Arrays.toString(digits)); // [-1, -1, -1, -1, -1, -1, -1, -1, -1, -1]
```

### binarySearch()

Sıralı bir dizide  aranan değerin bulunduğu indisini verir. Eğer dizi **dizide bulunmuyorsa** olsaydı `-(sıralanmış dizide olabileceği indis + 1 )` verir.

```java
int[] digits = { 80, 90, 40, 30, 20, 70, 60, 50, 00, 10 };
Arrays.sort(digits);    
int index = Arrays.binarySearch(digits,15); // 15 dizide yok eğer olsaydı 2 sırada olurdu.-(2+1)
System.out.println(index); // -3
index = Arrays.binarySearch(digits,90); // 90 sayısı 9 sırada
```

### equals()

İki dizinin tamamen, sırası sıranına birbirine eşit olup olmadığını sorgular. Aynı değerler içerse **fakat** farklı dizilime sahip ise `false` verecektir.

```java
int[] digits = { 8, 9, 4, 3, 2, 7, 6, 5, 0, 1 };
int[] digits2 = { 8, 9, 4, 3, 2, 7, 6, 5, 0, 1 };
Boolean isEqual = Arrays.equals(digits, digits2);
System.out.println(isEqual); // True
```



