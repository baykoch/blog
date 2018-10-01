---
title: "Java Sınıf ,Nesne ve Kod Yapısı "
last_modified_at:
categories:
  - java
tags:
  - java se
  - java 9
toc: true
toc_label: "Java SE"
author_profile: True
mathjax: true
---

### Sınıflandırma (classification)

Sınıflandırmanın gerçek hayatta soyutladığımız nesneleri kategorize etmek olduğunda bahsetmiştik. Bu noktada nesne ile sınıfı ayıt etmemiz çok önemli.

 Doğal Nesneler > Bitkiler > Meşe Ağacı

- Bir sınıftan bahsediyoruz. Türkiye'de her iklimde türünde **meşe** ağaçları yetişir.
- Bir nesneden bahsediyoruz. Kütahya’daki asırlık **meşe** ağacı ilgi odağı oldu.

Aynı yaklaşımla insanların bir sınıf Ali, Veli vb.lerinin bir nesne olduğunu söyleyebiliriz. Programlama aslında tamamen bu yaklaşım üzerine bina edilmiştir.

Artık yavaş yavaş yazılım dünyasına doğru yelken açalım. Bilmemiz gereken ilk bilgi yazılım bir ihtiyacın sonucudur olduğudur. Mesela taşıtlar neden icat edildi?  Elbette uzun yolculukları kısaltmak için diyebilir veya yük taşımak için diyebiliriz, bunlar gibi birçok neden sayılabilir. Dikkat ediniz hepsi bir ihtiyacın sonucu değil mi? Diğer birçok bilimsel, hukuksal ve sosyal gelişmeler hep bir ihtiyacın, hayatı daha yaşanabilir alana getirmemin sonucudur.

Şimdi orta ve büyük çaplı projelerde 3 temel bölümden oluşur.

**Analiz Bölümü**: İhtiyaç tanımı yapılır. Problem nasıl ne şekilde çözüleceği araştırılır, bilgi toplanır. Ne fazla ne de az; amaç ihtiyacı karşılayacak, problemi çözecek kadar ihtiyacın girdileri belirlenir. Bu doğrultuda ihtiyaç planları ortaya çıkar.

**Tasarım Bölümü**: Analiz planları incelenerek ihtiyacın nasıl bir yöntem ve yordam izleneceği belirlenir. Bu doğrultuda tasarım planı çizilir. Tasarım yaparken **modellemek**, müşterini ihtiyacını karşılar nitelikte ürün ortaya koymaktır.

**Gerçekleştirme Bölümü**: Tasarımın planına göre kodlaması, diğer bileşenlerinin hazırlanmasını; bunu takriben çalışan yazılımın ortaya çıkışını ifade eder.

### Nesne Kavramı (Object)

Nesne akıl yoluna edinilmiş kavramsal veya fiziksel şeydir.Bir telefon ele alırsak x markalı telefon çalıyor.

**X marka** = Durumunu ifade ederken

**Çalıyor** = Nesnenin davranışını ifade eder.

**Nesne** =  **Durum**(*state*) + **Davranışlardan**(*behavior*) oluşur.

Nesnelerde sınıflardan oluşturulur. Sınıflar nesneler için kategorize edilmiş -örneğimizde telefon- bir şablondur. Nesnenin özelliklerine **durum**(*state*) denir. Nesnenin durumlarının her birine **özellik**(*attribute*) denir.Nesnenin davranışları **fonksiyon veya metot veya prosedür** ile ifade edilir. Metotların bütününe **arayüz**(*interface*) denir.

Aynı sınıftan türetilen nesneler ayni türe sahiptirler. Sadece durumları farklıdır. Bazı davranışları gerçekleştirmeye bilirler. Bazı cep telefonlarının kamerası olmayabilir bu onun durumunu belirtir. Bu durumda fotoğraf çekemeyeceği için *fotoğrafÇek* diye bir davranışa sahip olmaz.

Davranışlardan dört farklı eylemi icara etmesini beklenir.

1. Durumunun hakkında bilgi ver. Hangi mobil işletim sistem kullanıyorsun? – Android Nougat
2. Durumunu değiştir.  Android Oreo sürümüne güncellendi.
3. Bir faaliyeti yerine getir.  Rehberden birini ara.
4. Son olarak istenileni bir başka nesneye havale eder. Havale edilen nesne yukarıdaki bahsedilen 3 özelliği yerine getirir. Telefon evin ışıklarını kapatamayacağı için Akıllı Aydınlatma Sistemine ışıkları kapat eylemini havale eder. AAS 3. maddeyi yerine getirir.

**Java’da her şey sınıf ve sınıflardan oluşmuş nesnelerden ibarettir.** Sınıflar erişim **belirleyici** (*Modifier*)  sınıf belirteci, adı ve bloktan oluşur. Bloğun sınırları **süslü** parantez ile belirlenir. Blokların içi ise **nesne değişkenleri** (*instance variable*) ve **nesne fonksiyonlarından** (*instance methods*) oluşur.

Basit olarak cep telefon ele alalım.

**Durumları**:

- Markası
- Lira miktarı
- Mesaj miktarı

**Davranışları**:

- Mesaj gönder.
- Arama yap.
- Lira Güncelleme

{% include figure image_path="/assets/images/java-class.png" alt="Java class" caption=""%}

Sınıflar durumlarına veya metodlarına erişim sağlamak, kısıtlamak için erişim belirleyiciler kullanılır. İlerleyen derslerde yeri geldiğince detaylı bir şekilde bahsedeceğiz. Şimdilik bir tablo ile özetleyelim.



| Erişim Belirleyici (Modifier)                             | private | Default | Protected | Public |
| --------------------------------------------------------- | ------- | ------- | --------- | ------ |
| İç sınıflar (inner class)                                 | Evet    | Evet    | Evet      | Evet   |
| Bulunduğu paketteki sınıflar (Same package class)         | Hayır   | Evet    | Evet      | Evet   |
| Bulunduğu paketteki alt-sınıflar (Same package sub-class) | Hayır   | Evet    | Evet      | Evet   |
| Diğer paketteki sınıflar (Other package class)            | Hayır   | Hayır   | Hayır     | Evet   |
| Diğer paketteki alt-sınıflar (Other package sub-class)    | Hayır   | Hayır   | Evet      | Evet   |

### İlk Kod "Merhaba Dünya"

Merhaba sınıfını şablonu oluşturduk. Sonra merhaba söyle metot yani davranışı tanımladık. Son olarak **MerhabaTest** sınıfı ile testimizi gerçekleştirdik. Main metodu programlarım tetikleyicisidir. Java main noktasından programı başlatır.

- MerhabaSınıfı bir şablondur.
- MerhabaMakine sınıfı duruma (state) sahip değildir.
- MerhabaMakine merhabaSoyle adlı bir arayüze sahiptir.
- MerhabaNesnesi  MerhabaMakinesi’den oluşturulmuş bir nesnedir. Yani sınıfın hayat bulmuş halini ifade eder. Artık yukarıda belirttiğimiz 4 davranışlardan birini yerine getirebilir.
- merhabaSoyle davranışını yerine getirdi. Bize "Merhaba Dünyalı" dedi.

<script src="https://gist.github.com/baykoch/e9990fd19555fbc76f4ade00857dd71d.js"></script>

1. Bir java sınıfında sadece bir tane `public` niteleyicisi olabilir.
2. Java sınıfların isimleri dosya ismi ile aynı olmak zorundadır.
