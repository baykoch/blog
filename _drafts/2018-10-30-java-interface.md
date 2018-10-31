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
toc_sticky: true
toc_label: "Java "
author_profile: True
---

 Arayüz(interface) tabiattaki nesnelerin birbirleri ile haberleştiği normlar bütünüdür. İnsanlar için dil, göz veya el birer arayüzdür.

Konumuza dönersek bütün metotları soyut olan sınıflara arayüz(**interface**) denir. Varsa erişim belirleyiciden sonra,  arayüz isminden önce `interface` anahtar kelimesi getirilerek oluşturulur.

Arayüzlerin metotları olağan(**default**) olarak soyut(**abstract**) ve `public` olur. Bu yüzden `abstract` ve `public` anahtar kelimesi yazılmayabilir. 

```java
public interface A {
  // Aşağıdaki iki metot eşitirler.  
  public abstract void start();
  void start(); // public ve abstract yazılmayabilir.
}
```

Arayüzler sınıflar tarafın sınıf isminde sonra ***`implements`*** anahtar kelimesini kullanarak devralır ve yerine getirir(*implementation*). Devralan sınıflar arayüzün metotları yerine getirmek zorundadırlar.

```java
public class A implements B {
	// Arayüzleri devralan sınıflar arayüzün metotlarını yerine getirmelidir.(implement)
	@Override
	public void start() {
		System.out.println("Lets go.");
	}

}
interface B {
	void start();
}
```

- Devirlan sınıflar metotları yerine getirmez ise kendi de arayüz olmak zorundadır.

- Arayüzler ile onu devralan sınıflar arasında miras ilişkisi vardır. Bir arayüz kendisini gerçekleştiren sınıfların ebeveyn sınıftır. Aralarında somutluk ve soyutluk farkı vardır. Yani sınıflar nesnesi üretilebildiğinden somut arayüzler nesnesi üretilemediğinden soyutur.

- Arayüzler yerine getirilen davranışları içerdiğinden genellikle sonu `-able` ilen biten isim kullanılır.

```java
// Arayüzlerin isimleri sonu genellikle -able biter
public interface Printable{
	
	void monochrome(String text); // Sıyah-beyez baskı
	void polychromechrome(String text);// Renkli baskı
	void printInfo();
	
}
```

Arayüzlerin code...

- Sınıflar birden fazla arayüzü devralabilir. Devraldığı her arayüzün metotlarını geçcekteştimek zorundadır.

```java
public class A implements B, C {
	// Birden fazla arayüzleri devralan sınıf arayüzlerin metotlarını yerine
	// getirmelidir.(implement)
	@Override
	public void start() {
		System.out.println("Lets go."); // From B interface
	}

	@Override
	public void stop() {
		System.out.println("Stoping..."); // From C interface
	}
}

interface B {
	void start();
}

interface C {
	void stop();
}
```

- Sınıflar sadece bir sınıfın miras alabilirken(**extends**) birden fazla arayüzü yerine getirebilir(**implements**). 

```java
//Sınıflar sadece bir sınıfı extends edebilirken bir den fazla arayüzü yerine gecçekleştırebilir.
public class A extends D implements B, C {//...}

interface B {//...}

interface C {//...}

class D {//...}
```

- Bazen arayüzler hiçbir metot içermeyebilir.-java serializable interface gibi- Bu gibi yapılara ***marker design pattern*** denir. Amaçı bir sınıf işaretlemektir. Örneğin `serializable` arayüzünde devalan sınıflar serialize ve deserialize edilebilir. Bir sınıfın serialize ve deserialize olup olmadığını ***instanceof*** operatörü yardımı kontrol edilebilir.
- Arayüzler durumları (*attributes*) yoktur. Sadece `public`,`static` ve `final` olan değişken tanımlanabilir. ***İlk değer verilmek zorundadır.*** Sadece bu tip değişkenlerden oluşan, davranış içermeyen arayüzler `enum` gibi davranır(eğer enum yapısı varsa neden  arayüzü bu şekilde kullanıyorsun) bu da istenmeyen durumdur **kaçınılmalıdır**.

```java
public interface C {
    // Aşağıdaki iki tanımlamada eşittir.
	int i = 2; // public, final ve static yazılmayabilir.
    public static final int i = 2;
}
```

