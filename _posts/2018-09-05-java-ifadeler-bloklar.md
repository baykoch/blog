---
title: "Java İfade,Cümle ve Blok Kavramları "
last_modified_at:
categories:
  - java
tags:
  - java expression
  - java block
  - java statement
toc: true
toc_label: "Java SE"
author_profile: True
mathjax: true
---

### İfade (Expression)

İfade yeni bir değer oluşturma veya atama işlemidir. İfadeler bazen tek bir atama işlemi olabileceği gibi karmaşık matematiksel ve fonksiyonel işlemlerin sonucunda olabilir. Tek bir ifaden veya birleşik birkaç ifadeden oluşabilir.  

- Yeni değer oluşturan ifadelere örnekler.

  ```mathematica
  5 / 2    
  7 % 3
  pi + (4 * 2)
  ```

- Atama işlemi ifadelerine örnekler.

  ```java
  final float pi = 3.14f
  int maxInt = 2_147_483_647
  boolean areYouKola = False
  ```

- Herhangi bir değer oluşturmayan ifadeler

  ```java
  int result = (a + b) / c  
  ```

- Birleşik (compound) ifadeler

   ```java
    boolean circle = (circumference > area) & radius > 0  //Birleşik bir ifade(expression)
    boolean compoundEx = (3 > 4) ? true : false; // false
   ```


Dikkat edilmesi gereken diğer önemli nokta ise ifadelerin değerleri çalışma zamanında `run-time` belirlenir.

```java
int maxInt = 2_147_483_647; // int alabileceği max değer ataması.
maxInt = 2_147_483_648;     // Hata! out of range
maxInt = maxInt +1;         // Çalışma zamanı değer belirlendiğinden hata vermeyecektir.
```

 Yukarıdaki kod parçasında:  

- ilk satırda `int` tipine atanabilecek maksimum değer atanmıştır.  

- İkinci satırda ise maksimum değeri bir fazlasının  atamasına hata verecektir.  

- Üçünü satırda hata vermeyecektir. Çünkü ifadeler çalışma zamanında belirlendiğinden sonucun hangi değer olduğunu Java bilemiyor. Bu duruma dikkat edilmezse bazen ölü bölge oluşabilir.

  ```java
  int test = 3;
  if (test > 8) {    //Java uyarmıyor.
       //Ölü bölge     
  }
  ```

### Cümleler (Statements)

`Statements` yazılım dilindeki anlamlı en küçük çalıştırabilir birimidir. Cümleler ifadelerin sonuna noktalı virgül eklenerek oluşturulur.  

- İfade cümleleri -Expression Statement-

  ```java
  counter = 2;                // tanımlama cümlesi
  counter++;                  // matematiksel cümle
  System.out.println(counter) // metot çağrı cümlesi
  Person ali = new Person();  // nesne oluşturma ifadesi
  ```

- Akış kontrol cümleleri -Control Flow Statement-

  - decision-making statements : `if-then`, `if-then-else` and`switch`
  - the looping statements :`for`, `while` and`do-while`

​       Akış kontrol cümleleri gelecek konumuz olacak.

### Bloklar

Blok sıfır veya daha fazla cümleden oluşan sınırları süslü parantezle belirtilmiş alanlardır.  Blok çeşitleri aşağıda sıralanmıştır. İleriki derslerde bahsedecektir.

- Değişken tanımlama *(Declaration block)*

- İlk değer atama *(İnitialization block)*

- Karar verme *(decision-making blocks)* `if-then`, `if-then-else` and`switch`

- Döngü blokları *(looping blocks)* `for`, `while` and`do-while`

- Metot blokları

- Sınıf tanımlama: Local class, nested class and  anonymous class

Bloklar ile  ilgili bazı önemli noktalara değinecek olursak: Bloklar kasamı (*scope*)  belirler ve birbirlerini kesmemelidir.
