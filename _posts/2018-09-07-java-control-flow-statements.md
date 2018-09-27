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
toc_label: "Java Flow Control"
author_profile: True
mathjax: false
---

Java doğal yapısında olarak *döngü ifaderi* ve *karar verme ifadeleri* vardı. Bununların yanında `break` gibi *dallanma ifadeleri* bulunur.

- Java Akış Kontrolü (*Control Flow Statements*)
  1. Döngü ifadeleri (*the looping statements*)
     - for ve for each (*ilerde bahsedilecek*)
     - while
     - do-while
  2.  Karar İfadeleri (*the decision-making statements*) 
     - if veya if - else 
     - switch 
  3. Dallanma ifadeleri (*the branching statements*)
     - break, continue, return

## Döngü ifadeleri (*the looping statements*)

### While

`X` kontrol ifadesi doğru olduğu sürece `Y` bölümü çalışır.

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



### do-while

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

### for

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

## Karar İfadeleri (*the decision-making statements*) 

### if or if-else

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


### Switch

`Switch` yapısı `if-else if` iafeldrini daha toplu ve hızlı olan yapılarıdır. Kontrol yapısında değere göre dallanma yapılır. 'case' kısımlarında **sabit** olmalıdır. `switch` yapısının desteklediği tipler: *byte, short, char, and int , enum , string sınıfı ve ilkel tiperin sarmanmış -wrap- sınıfları (Character, Byte, Short, and Integer)*

**Not:** *Wrap* sınıfları ve *string* sınıfı hariç karmaşık tipleri desteklemez. Ayrıca `boolean ` tiplerini de desteklemez.

```java
int day = 2;
switch (day) {
	case 1:
		System.out.println("Monday"); break;
	case 2:
		System.out.println("Tuesday"); break;
	case 3:
		System.out.println("Wednesday"); break;
	case 4:
		System.out.println("Thursday"); break;
	case 5:
		System.out.println("Friday"); break;
	case 6:
		System.out.println("Saturday"); break;
	case 7:
		System.out.println("Sunday"); break;
	default:
		System.out.println("Invalid day"); break;
}
```

`Switch` yapısında dikkat edilmesi gereken durumlar:

- `case`  hiçbir değer aynı olamaz.

- `break` yazılmaz ise `break` buluncaya kadar çalısır.

  ```java
  String currency = "TL";
  switch (currency) {
  	case "TL":
  		System.out.println('₺');    // Break konulmadığı için TL ve Euro ikiside yazılır.
  	case "Euro":
  		System.out.println('£');
  		break;
  	case "Dolar":
  		System.out.println('$'); break;
  }
  ```

- `default` hiçbir durum çalışmadığında çalısan kısımdır. Yeri önemli değildir; başta, ortada veya sonda bulunabilir. Son olarak zorunlu değildir.
- `case` kesinlikle sabit olmalıdır. (Dikkat ! *final* ile tanımlanmış tip olabilir.) 

## Dallanma ifadeleri (*the branching statements*)

### break, continue

`break` bulunduğu bloğun çalışmasını sonladırırken, `continue` ise sade bulunduğu adımın çalışmasını sonlandırır.

`break` kullanılabildiği akış yapıları: `for`,`while`,`do-while`ve `switch`

`continue` kullanılabildiği akış yapıları: `for`,`while` ve `do-while`

```java
// 0 ile 20 arasındaki çift sayılar yazdıralım.
for (int i = 0; i <= 20; i += 2) {

	if (i == 4) {          
		continue;         // Sadece 4. adım kırıldığından 4 basılmayacak. 
	} else if (i == 10) { 
		break;            // 10. adımda blok kırıldığından 10 ile 20 arasındaki çift sayılar basılmayacak.
	}
	System.out.println("i = " + i); // i = 0 2 6 8 
}
```

### break ve continue etiket (*label*) ile kullanımı

`break`işararetlemiş  blogun kırılmasına  sağlar. Aşağıdaki kod parçasında birden fazla `3` olamasına rağmen ilk bulunduğu zaman aramaı bırakacaktır. `f:` kaldırıp sadece `break` kalsaydı bulmaya devam edecekti.

```java
int[][] dizi = { { 0, 1 }, { 3, 3 }, { 4, 3 } };
int find = 3;
f: for (int i = 0; i < dizi.length; i++) {  // İlk sayı bulunduğunda kırılacak.

	for (int j = 0; j < 2; j++) {
                 
		if ( dizi[i][j] == find ) {
			System.out.println((i) + ".satır " + (j) + ".sütünda bulundu!");
			break f;      // Dış döngüyü sonlandırır. 
            //continue f; // Sadece iç döngüyü sonlandırır.
		}
				
	}
}
```

Yukarıdaki kod parcasında `break` yerine `continue` yazılsaydı, sadece bulduğu satırı atlayacaktı. Yani,  ilk değeri 2. satırda `{ 3, 3 }` bulacak 2.satırın 2. sütününe bakmadan diğer `{ 4, 3 }` satırına atlayacaktı.

### return

`return` bir metotdan çağrıldığı yere dönmeyi sağlar.  Metot türüne göre bir değer geri dönderebilir veya döndermez. Eğer bir değer geri döndermiyorsa kullanılmasına zorunlu olmayıp isteğe bağlı sade halinde `return;` kullanılabilir. 

```java
public static void main(String[] args) {
      methodOne();
      int result = methodTwo(3);
      System.out.println(result);
}
public static void methodOne() {
		System.out.println("Değer döndürmeyen metot");
		// return 2; !!! Hata 
		return;    //İsteğe bağlı
}
public static int methodTwo(int i) {
		return i*i; 	// Sayının karesi 
		// i+=2;        // Ölü kod return'den sonra çalışmaz!!!
}
```

### goto

Java'da `goto` anahtar kelimesi bulunmasına rağmen  sakıncalı görüldüğünden kullanılmaz.


