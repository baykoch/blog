---
title: "Java Generics"
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

Generics iki türlü kullanımı sahiptir.

1. Torba gibi veri yapılarda sadece spesifik nesne tipleri kullanımı sağlama.

```java
public class GenericsDemo {

	public static void main(String[] args) {
		
		Set meyvelerB = new HashSet();
		meyvelerB.add("Kivi");
		meyvelerB.add("Muz");
		meyvelerB.add("İncir");
		// add metodu object kabul ettiği için hertürlü tip eklenebilir. 
		meyvelerB.add(23);
		System.out.println(meyvelerB); // [İncir, Kivi, Muz, 23]
		
		Set<String> meyveler = new HashSet<>();
		meyveler.add("Kivi");
		meyveler.add("Muz");
		meyveler.add("İncir");
		// Generics ile Set tipi String belirledik.	
		// meyveler.add(23);  // Hata! String'den faklı tipde değşken eklenemez		
    }
}
```

- Generics kullanmak tipleri birbirine çevrimden(cast) kurtarır.
- Spesifik tipden başka nesneler eklenemez.

Generics kullanılan tip parametre isim ve anlamları:

| Adlandırma | Açıklaması                                                   |
| :--------: | :----------------------------------------------------------- |
|     E      | Java Collections yapılarında elemanı(Element) temsil eder.   |
|     K      | Map gibi anahtar-değer çifti içeren yapılarda anahtar(Key) tipini temsil eder. |
|     V      | Map gibi anahtar-değer çifti içeren yapılarda değer(Value)  tipini temsil eder. |
|     N      | Sayı tiplerini temsil eder. ***Number*** sınıfın miras alan tipler(Double,Integer...) |
|     T      | Tipi bilinmeyen değerleri için kullanılan ilk generics adlandırma |
|     S      | Tipi bilinmeyen değerleri için kullanılan ikinci generics adlandırma |
|     U      | Tipi bilinmeyen değerleri için kullanılan üçüncü generics adlandırma |
|     V      | Tipi bilinmeyen değerleri için kullanılan dörtüncü generics adlandırma |
|     ?      | Joker                                                        |

Örnekler:

- ***E example***:

````java
class ListGenerics<E> {
   private List<E> l = new ArrayList<E>();
   // ... 
}
````

- ***K-V example***:

```java
class MapGenerics<K,V>{
   private Map<K,V> map = new HashMap<K,V>();
	// ...
}
```

- ***N example***:

```java
class MapGenerics<N extends Number>{   
	// ...
}
```

- ***T S U V example***:

```java
public class GenericsClass<T, S> {
	private T t;
	private S s;
	
	public GenericsClass(T t, S s) {
		this.t = t;
		this.s = s;
	}
}	
```



1. Hangi tipde olduğu bilinmeyen sınıf tipi ve durumu; metot geri dönüş tipleri ve metot parametreleri generics yapıda olabilir.
   - Generics tipler ilkel tip(*int,double,boolean*...) olamaz.

   - Generics ihityaca göre yeni sınıf yapıları ile kullanılabilir.

   - Generics kullanıcı tarafından oluşturulan sınıflar kullanılabilir.

   - Miras ilişkisine sahip alt-sınıf üst sınıf yerine kullanılabilir. Fakat alt sınıf üst sınıfn yerine kullanılamaz.

```java
public class GenericsClass<T, E> {
	private T t;
	private E e;
	
	public GenericsClass(T t, E e) {
		this.t = t;
		this.e = e;
	}
	@Override
	public String toString() {

		return "GenericsClass [T=" + t + ", E=" + e + "]";
	}
	
	public static void main(String[] args) {
		
		GenericsClass<String, Integer> book= new GenericsClass<>("Otomatik Portakal",1962);
		System.out.println(book); // GenericsClass [T=Otomatik Portakal, E=1962]
		
		// Generics tipler ilkel tip(int,double,boolean) olamaz.
		//GenericsClass<String, int> book2= new GenericsClass<>("Otomatik Portakal",1962); // Hata!
				
		// Yeniden faklı tipde generics sınıf tanımlama
		GenericsClass<Double, Boolean> newGenerics= new GenericsClass<>(3.14,false);
		System.out.println(newGenerics); // GenericsClass [T=3.14, E=false]
		
		// Generics kullanıcı tarafından oluşturulan sınıflar kullanılabilir.
		// Aynı sırda oturan iki öğrenci çifti
		Öğrenci ö1= new Öğrenci("Ali K.", 22);
		Öğrenci ö2= new Öğrenci("Veli K.", 23);
		GenericsClass<Öğrenci, Öğrenci> sıra= new GenericsClass<>(ö1,ö2);
		
		// Miras ilişkisine sahip alt-sınıf üst sınıf yerine kullanılabilir.(Upcasting) 
		GenericsClass<Öğrenci, Kişi> sıra2= new GenericsClass<>(ö1,ö2);
		
		// Alt-sınıflar kullanılamaz.
		Kişi k = new Kişi();
		//GenericsClass<Öğrenci, Kişi> sıra3= new GenericsClass<>(k,ö2); // Hata!	
	}	
}
class Öğrenci extends Kişi{

	private String name;
	private int no;

	public Öğrenci(String name, int no) {
		this.name = name;
		this.no = no;
	}
	
	@Override
	public String toString() {
		return "Student [name=" + name + ", no=" + no + "]";
	}

}
class Kişi{}
```

- Generics tipler ilkel tip(*int,double,boolean*...) olamaz.
- Generics ihityaca göre yeni sınıf yapıları ile kullanılabilir.
- Generics kullanıcı tarafından oluşturulan sınıflar kullanılabilir.
- Miras ilişkisine sahip alt-sınıf üst sınıf yerine kullanılabilir. Fakat alt sınıf üst sınıfn yerine kullanılamaz.

















### Generics Problemli Kısımları ve Önlemler

Generics sadece derleme zamanında tip koruması sağlar. Çalışma zamında(runtime) tip koruması(type erasure) sağlamaz. Geriye dönük uyumluluk sağlamak amacıyla bu karar alınmıştır.

***Type Erasure:*** Generics yapılarının çalışma zamanında tip değerlerini silinmesinidir.

- ` List<String> meyveler` generics kısım(<String>) çalışma zamında silinerek `List meyveler` halini alır.

***Derleme Zamanı (Compile Time):*** Program dosyalarının  makine koduna çevrilmesini ifade eder.

***Çalışma Zamanı (Runtime):*** Üretilen makine kodlarının hedef sistemde çalıştırılmasıdır.



1. Generecs çalışma zamanında silinirler. Faklı tipe sahip olmalarına rağmen faklı imzaya sahip iki arayüz tanımlanamaz.

```java
public class GenericsProblem { 
 	// İmzaları faklı olmasına rağmen aynı isimli metot tanımlanamaz.
    public void call(List<String> meyveler) { } 
    public void call(List<Integer> digits) { } 
}
```

> Erasure of method call(List<String>) is the same as another method in type GenericsProblem



2. Generics tiplerin kullanılıdığı tipler arasında karşılaştırma yapılıyorsa **Comparable** `extends` edilmelidir.
