---
title: "Java Akış Kontrolü "
last_modified_at:
categories: 
  - java
tags:
  - java if
  - java while
  - java for
  - java switch
toc: true
toc_label: "Java Flow Control S."
author_profile: True
mathjax: false
---

Java doğal yapısında olarak *döngü ifaderi* ve *karar verme ifadeleri* vardı. Bununların yanında `break` gibi *dallanma ifadeleri* bulunur.

- Java Akış Kontrolü (**Control Flow Statements**)
  1. Döngü ifadeleri (*the looping statements*)
     - for ve for each (*ilerde bahsedilecek*)
     - while
     - do-while
  2.  Karar İfadeleri (*the decision-making statements*) 
     - if veya if - else 
     - switch 
  3. Dallanma ifadeleri (*the branching statements*)
     - break, continue, return

### Döngü ifadeleri (*the looping statements*)

#### While

`X` kontrol ifadesi doğru olduğu sürece `Y` bölümü

 çalışır.

```mathematica
while ( X ) {    
    Y
}
```
`0` ile `10` arasındaki sayıları toplayan örnek uygulama.

```java
public static void main(String[] args) {
		
		int index = 1;
		int toplam = 0;
		while (index <= 10) {        //Koşul
			toplam = toplam + index;
			index++;
		}
        System.out.println("1 + 2 ... 10 = "+ toplam);
}
```



#### do-while

`do-while` ifadesini `while` farkı ***an az bir kez*** çalışmasıdır. `X` kontrol ifadesi doğru olduğu sürece `Y` bölümü çalışır. `while` ifadesinin sonunda `;` **noktalı virgul** koyulmalıdır.

```mathematica
do {
     Y			
} while ( X );
```

Yukardaki aynı örneğin `do-while`  ile yazılmış hali:

```java
public static void main(String[] args) {
		
		int index = 1;
		int toplam = 0;
		do {
			toplam = toplam + index;
			index++;
		} while (index <= 10);
		System.out.println("1 + 2 ... 10 = " + toplam);

}
```



#### for

`for` ifadeleri diğer döngü ifadelerin tek yönde kontrol yapısı aksine başlangıc ve bitişle sınırlamaya zorlayan yapılardır.


```mathematica
for ( X  ;  Y ; Z )   {
      W
}
```

`X` : ilk değer ataması yapılır.

`Y`: Bitiş şartı

`Z` : Değişim ifadesi

`W`: Koşul sağlandığında çalışacak ifadeler

**Çalışma sırası** ilk başta `X`  çalışır daha sonra `Y` - `W` - `Z`  sırasında bir döngüde devam eder. 

```java
public static void main(String[] args) {
		
		int toplam = 0;
		for (int i = 1; i <= 10; i++) {
			toplam = toplam + i;
		}
		System.out.println("1 + 2 ... 10 = " + toplam);

}
```

`for` yapısının bazı özelliklerini sıralayalım.

1. `for` içerisinde iki tane noktalı virgül `;`zorunludur. 

   ```java
   for(;;) {
   	//Sonsuzluk
   }
   ```

2. İlk değer ataması `for` bloğunun dışında tanımlanabilir.

   ```java
   int i = 0;
   for (; i <= 10; i++) {
   	toplam = toplam + i;
   }
   ```

3. `for` kontol yapısında birleşik  `compound` ifadeler kullanılabilir. Örnekte biri artarak `i` biri azalarak `j` toplamı 10 eden sayılar.

   ```java
   for (int i = 0, j = 10 ; (i < 10 & j > 0); i++, j--) {
   	System.out.println("i = " + i + " j = " + j); // i:1 j:9 ... i:3 j:7
   }
   ```

### Karar İfadeleri (*the decision-making statements*) 

#### if or if-else

`if` bir ifadeye bağlı karar veren, `if-else`yapısı ile dallanma yapabilien yapılardır.

```mathematica
if (condition) {        1.İlk şart
			
} elseif(condition) {   2.İkinci şart (zorunlu değil) 
 .                      .
 .						.
 .						.
}else {}                N. Yukaradaki hiçbir şart sağalmazsa (zorunlu değil) 
```

**Örnek**: `random` foksiyonun  0 ile 100 aralığında hangi çeyreğe denk geldiğini bulan kod yazalım.

```java
Random r = new Random();
int k = r.nextInt(100);

if (k <= 25) {
	System.out.println("K 1.çeyrekte");
} else if (25 < k && k <= 50) {
	System.out.println("K 2.çeyrekte");
} else if (50 < k && k <= 75) {
	System.out.println("K 3.çeyrekte");
} else {
	System.out.println("K 4.çeyrekte");
}
```

Bazı özellikler:

1. Karar veya döngü  yapıların koşul ifadesinin sonuçu her zaman mantıksal işlemdir.

   ```java
   int x = r.nextInt(100);
   int y = r.nextInt(100);
   boolean z;
   if (z = x < y) {         // Z true veya false
      System.out.println(z);
   }
   ```

2. Bir satırlık kod için parantez `{}`kullanılmaya bilir ama tavsiye edilmez.

   ```java
   x = r.nextInt(100);
   if(x > 0.5)
   	System.out.println(x)
       
   if(x > 0.5)
   	int y;      // Hata !!! İf den sonra parantezsiz tip tanımlanamaz.  
   ```


#### Switch

