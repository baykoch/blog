---
title: "Java İsimlendirme ve Şekil Rehberi (Style Guide)"
last_modified_at:
categories: 
  - java
tags:
  - java style guide
  - java isimlendirme
toc: true
toc_label: "Java SE"
author_profile: True
mathjax: true
---

Hani bir tabir vardır: Ancak aynı dil ve duyguları sahip kişiler birbirleri ile iyi anlaşabilirler. Hatta aydı dili bilmekte yetmez dilin kurallarına hakım olmak gerekir. Bir bakıma programlama dünyasında da işler böyledir.  

Peki, neden ?

- Yazılımların maliyetini yaklaşık %75  ürünün bakımına harcanır.
-  Genellikle herhangi bir yazılımın bakımını, yazılımın yazarları tarafından yapılmaz.
-  Bu nedenle bakım sürdürülebilmesi ve yazılımın ihtiyaçlara göre güncellenebilmesi için kodun okunabilirliği çok önemlidir.

### Dosya Organizasyonu Nasıl Olmalı

1. Bir yazılım dosyasıda (.**class**) her bölümün arası bir satır boşluk olmalı  
2. Bir yazılım dosyasıda 2000 satırdan fazla kod yazmaktan kaçınılmalı

Java Dosyası aşağıda belirtilen sıra izlenmeli:

1. Başlangıc yorumları. “/** ... */ ” parametreleriyle oluşturulur ve içeriği aşağıdaki kurala göre yazılır.  

```java
/**
 * Sınıfİsmi (Classname)
 * 
 * Versiyonu  (Version information)
 *
 * Tarih (Date)
 * 
 * Telif uyarısı (Copyright notice)
 */
```

2. Paket ifadeleri: Paketler isimleri küçük harfle yazılmalı kelimeler arasına nokta konulmalıdır. Paket isimleri arasına tire (*hypens*) ve alt-tire (*underscores*) konmaz. 
3. Import ifadeleri: İmport kullanılırken sadece ilgili kütüphane import edilmedir.Kütüpheneni hepsi ile ilgili moduleun import edilmesi arasında bir performans farkı yoktur.

```java
pacgake com.baykoch.javase.b2  //Doğru kullanım
pacgake com.baykoch.javase.b_2 //Yanlış kullanım

import java.util.*;           //Tavisye edilmez
import java.util.HashMap;     //Okunanilirk acısında iyi
```

4. Class ve Interface Bölümü

- Class/interface dükümantasyon yorumu  ( ""/** ... **/"")
- Class veya Interface ifadeleri
- Class/interface uygulama yorumu (implementation) ""/** ... ** / "", İsteğe bağlıdır. Implementation yorumu ilgili sınıf ve interface genelini içeren yorum yazılmamalı ve sadace bu bölümde uygulanacak kısımlarla ilgili yorum yapmaya  dikkat edilmeli.
- Class ( static) değişkenler  “Private , public ve protected “
- Durum değişkenleri (Istance Attrıbutes)
- Kurucular (Constructors)
- Metotlar  

Örnek basit bir sınıf içeriği:

```java
/*
 * @(#)Circle.java        v1.00
 *
 * 15/08/2018
 * 
 * This file is part of Java Dersleri.
 *
 * Java Dersleri is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * Java Dersleri is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with Java Dersleri.  If not, see <https://www.gnu.org/licenses/>.
 *
 */

package com.bayckoh.javase.b1;

/**
 * 
 * Basit geomoetride daire sınıfının durumlarını ve bazı davranışlarını
 * tanımlar.
 * 
 * @author Muhammed K.
 * @version 1.00
 * @since 1.9
 */
public class Circle {

	/**
	 * Dairenin yarıcapını tanımlar
	 */
	private double radius;

	/**
	 * Kurucu metot(Default constructor)
	 */
	public Circle() {

	}

	public double getRadius() {
		return radius;
	}

	public void setRadius(double radius) {
		this.radius = radius;
	}

	/**
	 * Bu metot daireni alanı hesaplar
	 * 
	 * @return dairenin alanını
	 */
	public double calculateArea() {
		return Math.PI * radius * radius;
	}

	/**
	 * Bu metot daireni cevresini hesaplar
	 * 
	 * @return dairenin çevresi
	 */
	public double calculatecircumference() {
		return 2 * Math.PI * radius;
	}

}
```


### Classes & Interfaces

Sınıflar ve arayüzler UpperCamelCase kuralanına göre, ilk harf büyük ve kelimeler arası geçişte ilk harf büyük yazılır. Örnek: İşletimSistemi.

###  Methods

Metotlar lowerCamelCase kuralanına göre, ilk harf küçük  ve kelimeler arası geçişte ilk harf büyük yazılır. 

```java
public double calculateArea() {
		return Math.PI * radius * radius;
}
```

### Variables & Parameters

Veri tipleri ve parametreler “lowerCamelCase” kuralına göre yazılır.

1. Değişkenler küçük harfler ve geçişlerde herhangi bir alt-tire gibi özel karakter kullanma.
   > karadenizİklimi  //Hatalı
   > karadeniziklimi, karadeniz_iklimi vb.leri  //Doğru

2. Değişken isimlerinde kısaltma kullanımı önerilmez ama bloglar içinde veya tek kullanımlık geçici durumlarda kullanılabilir. Bu şekilde kullanımlarda, hep aynı biçimde kısatmaları  kullanımına dikkat et. Bazı yaygın kısatmalar: 
   - Döngülerde I,j
   - Steam için str
   - input için in
   - file için f
   - output için out

3. Kısaltılmış kelimelerin  harfleri tamamını büyük harfle yazma.

   > XMLHTTPRequest //Hatalı
   > 
   > XmlHttpRequest //Tavsiye

4. Değişken çoğul ifadeleri çağrıştırıyorsa  kelimeyi çogul yap.
   > systemProperties //Good 
   > 
   > systemProperty   //Bad

5. Boolean değişkenlerini sanki soru soruyormuş gibi yaz. Soru ekini yazmadan oluştur.
   > HatMeşgulmu  //:( 
   > HatMeşgul    //:)
   > 
   > iscarStopped //:( 
   > carStopped   //:) 

6. Statik değişkenler isimlendirme tamamı büyük ve kelimeler arası alt-tire kullanılır.
   > public static final int PI_NUMBER = 3.14;

7. Değişken tanımı yapılırken tek satırda yazma. Tip ve tanımlayıcılar arasında bir boşluk bırakabilir ya da aynı hızaya çekebilirsin.

   ```java
   int level;            //Tek satırda tımlama ve arasında 1 boşluk
   int size;       
   int level, size;      //Hatalı
    
   int     level;        // Aynı seviyede hızalama için boşluk kullanımı
   int     size;                    
   Object  currentEntry;
   ```

8. Global değişkenler ile yerel değişkenleri aynı isimde **tanımlamamaya** dikkat et.

9. Değişkenlerin ilk değerleri, bazı işlemlerden sonra atama yapılması gereken durumlar hariç, tanımlanan yerde ilk değer ataması yapmaya dikkat et.

10. **for** blokları hariç bir bloğun arayüzünde değişken tanımlaması yapma

### Indentation

İndentation Türkçede girinti çıkıntı gibi anlamlara gelmektedir.  Pratikte bir düzen veya tertip sağlamak için uygulanan kurallar bütünü diyebiliriz. Örneğin yeni bir paragrafa geçtiğimizi belirtmek için satır başı boşluk bırakmak gibi.

#### Satır Uzunlukarı (Line Length)

Okunabirliği zorlaştırdığı ve karışıklığa sebebiyet verdiği için  satırları çok uzun tutulması tavsiye edilmez. Bir satırın maksimumun uzunluğu 80 karakter olmalıdır.

#### Satır Sarmalama (Wrapping Lines)

İlk başta eğer satır 80 karakterdn fazla ise yeni satıra gecilecekse hangi kurallara uymalıyız onlara  bir göz atalım.

- Yeni satır virgulden sonra veya oparatörden önce yapılmalıdır.
- Metot çagrılarında birden fazla ifade içeriyor ve bu ifadeler arasında yüksel-düşük seviye ilişki var ise yüksek olanı tercih et.

```java
someMethod(longExpression1, longExpression2, longExpression3, // Virgunden sonra kesme
         longExpression4, longExpression5);   // 8 boşluk 
         
var = someMethod1(longExpression1,  // Yüksek seviyeden kesme yapıldı
              someMethod2(longExpression2,   // 8 boşluk bırakıldı
                     longExpression3));      // 8 boşluk bırakıldı

```

- Operatörden önce yapılan kesmelerde yeni satırı  orijinal satır  ile hizalanır.

```java
longName1 = longName2 * (longName3 + longName4 - longName5)
           + 4 * longname6; // Doğru

longName1 = longName2 * (longName3 + longName4
                       - longName5) + 4 * longname6; // Hatalı 
```
- Metot arayüzlerilerinde yeni satır geçildiğinde gelenksel girinti kullan

```java
someMethod(int anArg, Object anotherArg, String yetAnotherArg,
           Object andStillAnother) {        //Aynı satır hizası
      ...
}
```

- Metot imzası çok uzun ise 8 tane space kullan

```java
private static synchronized horkingLongMethodName(int anArg,
        Object anotherArg, String yetAnotherArg, //Satır başı 8 tane boşluk
        Object andStillAnother) {  //Satır başı 8 tane boşluk
       ...
}
```

- if ifadelerinde 4 tane boşluk yerin 8 tane boşluk kullanımını önerilir.

```java
//Hatalı
if ((condition1 && condition2)
    || (condition3 && condition4)
    ||!(condition5 && condition6)) {
    doSomethingAboutIt();            
} 

//Doğru 
if ((condition1 && condition2)
        || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
} 

//Bu şekilde de kullanılabilir.
if ((condition1 && condition2) || (condition3 && condition4)
        ||!(condition5 && condition6)) {
    doSomethingAboutIt();
} 
```

- Ternary ifadeleri için aşağıda belirtilen 3 durumda kullanılabilir.

```java
alpha = (aLongBooleanExpression) ? beta : gamma;  

alpha = (aLongBooleanExpression) ? beta
                                 : gamma;  

alpha = (aLongBooleanExpression)
        ? beta 
        : gamma;  
```

- Son olarak blok içi satır başı 4 tane boşluk yaparak başlanır.

```java
class MyClass{
    public static void main( String[] args ){  //4 tane boşluk
        ...
    }
}
```

- Satır 80 karakterden fazla ise:

```java
class MyClass{
    public static void aVeryLongMethod(new MyClassThatDoesSomething myClassThatDoesSomething, // 4 tane boşluk
            new MyOtherClassThatDoesSomething myOtherClassThatDoesSomething, // 8 tane boşluk
            int aVeryLongIdentifer) 
        ...
    }
}
```

