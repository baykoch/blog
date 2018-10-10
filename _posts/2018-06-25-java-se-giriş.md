---
title: "Java Giriş"
last_modified_at:
categories:
  - java
tags:
  - java se
  - java 9
toc: true
toc_sticky: true
toc_label: "Java SE"
author_profile: True
mathjax: true
---

### Programlama Nedir?

Programlama her şeyden önce bir soyutlamadır. Peki, soyutlama nedir? Soyutlama doğal (kâinat kanunları), yapay (insanların ürettiklerini) bin bir müşkülat ile anlama çabasının bir sonucudur.  Hayatta her şey sonsuz bir derinliğe ve genişliğe sahiptir.  Bu gerçekliğin parçalarını anlayabilmek ve buna mukabil uygulayabilmek için var olan bilginin kısıtlanması ve sadeleştirilmesi gerekir.  Tam bu noktada soyutlama başvuruyoruz. Örnekle devam edelim. Günümüze hemen hemen herkeste var olan telefonları tasavvur edelim. Biz kullanabilmek için telefonun hangi materyallerden oluştuğunu, bu materyallerin arasında ilişkiyi, nasıl çalıştığını, en temel elektronik devrelerini bilmemiz gerekmez. Aksine üreticiler telefon oluşturan donanımından yazılımına kadar binlerce bilgiyi tüketicilerden gizleyerek kişilerin telefonu kullanılabilecek seviyede bilgi sahip olması sağlamayı amaçlar. İşte bu soyutlamadır. Diğer bir örnek ise bilgisayarın aslında elektronik devrelerden oluştuğunu biliyoruz. Elektrik var yoktan dili makine diline (0 = yok, 1 = var), makine dilinden yüksek seviyeli dillere -C gibi- yüksek seviyeli dillerden daha yüksek seviyeli dillere –Java gibi-  soyutlamadır. Şimdi **Assembly** programlama ile döngü yazmayı düşünün. Sonra **Java** ile *for/while* döngü yazmayı tasavvur edin bunun ne kadar daha kolay olduğu fark edeceksiniz.

 **Model** ise birçok karmaşık soyutlanmış sistemleri bir araya getirerek daha karmaşık sistemi anlamaya çalışmaktır. İnsanı anlayabilmek için onun duygularını, dolaşım sistemi sinir sistemi gibi sistemlerini bir araya getirmek gerekir.

 **Sınıflandırma** soyutladığımız bilgileri kategorize etmektir.

Programlama dilleri bu **soyutlamadan** başka bir şey değildir. Bir problemi ne ihtiyaçtan fazla ne de az bilişim dünyasına soyutlanarak aktarılması ve problemin çözülmesi amaçlar. Örnek olarak akaryakıt istasyonunda bazı akaryakıt türlerinde yakıt ikmali yaptığımız düşünelim. Adım adım soyutlayarak problemi kabaca çözmeye ve anlamlandırmaya çalışalım:

1. Akaryakıt türlerini kimyasal yapılarını, taşıtların ile akaryakıtlar arasındaki ilişkiyi -Benzinli Motorların Çalışma Sistemi Nedir? Nasıl Çalışır? - bilmeden türlerini **sınıflandırarak** program diline aktarıyoruz.

2. Asla ihtiyaçtan ne az ne de fazla bir türü tanımlamıyoruz.(Mesela ileride motorin satışı da yapılabilir diye düşünerek motorin eklemesi yapmıyoruz.)
3. Son olarak fatura tahsilat gibi işlemler için muhasebe bölümü oluşuyoruz.
4. Akaryakıt Bölümü ve Muhasebe Bölümü **modelleyerek** akaryakıt istasyonu daha karmaşık sistemi Akaryakıt İstasyonu oluşturduk.

### Java Nedir?

- **Basitir.**

 Pek çok programlama dilden basittir. Pointer, bellek yönetimi yöntemler kullanıcıların ellerine bırakılmamış kendi iç mekanizmalarla çözülme yoluna gidilmiştir. Buna mukabil sürükle bırak programlama kültürünü benimsemiş yazılımcılar ve tasarımdan uzak kaba kuvvet vari programlama yapan yazılımcılar için zor olabilir.

Platformdan bağımsızdır. Kaynak kod incelmesi ve `debugging` kolaydır.

- **Nesne merkezlidir.**

Nesne merkezli programlama 4 ana ilkelerine sahiptir. Daha sonra detaylı incelenecek. Nesne merkezli olması problemi daha düzgün modellemesini ve çözülmesini sağlar.

- **Java hem yorumlanabilen hem de derlenebilen dildir.**

Derleme ve yorumlayıcının tablo ile neler ifade ettiğine ve karşılaştırmasına göz atalım.

| Derleme (Compiled)                                           | Yorumlama (Interpreted)                                      |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| Program, bütün olarak makine dili çevrilir ve hedef sistemde çalıştırılır. | Satır satır makine koduna çevrilir ve makine kodu çalıştırılır. |
| Derlendiği platform bağlıdır.                                | Hedef sitemde yorumlayıcı kurulu olduğu sürece platformdan bağımsızdır. |
| Genellikle hızlıdır.                                          | Genellikle yavaştır.                                          |
| Kod incelemesi (debug) yapmak zordur. Örnek: C dili            | Satır satır işlendiği için kolay debug yapılır. Örnek: Python |
| Bellek tüketimi fazladır.                                    | Bellek tüketimi azdır.                                       |
| Kaynak kodu hususidir.                                       | Kaynak kodu umumidir.                                        |

{% include figure image_path="/assets/images/jvm.png" alt="jvm" caption=""%}


**1.Bölüm:** Java sınıf dosyaları Java Derleyici tarafından Java byte koda çevrilir. Bu işlemlerin amacı sitemden bağımsız, JVM kurulu her bilgisayarda çalışabilmesini sağlamaktır.

**2.Bölüm:** Transfer aşamasıdır. Derlenen yerel sisteme; ağ üzerinden veya farlı yollar ile hedef sistemlere (Örnek:  Android OS)  taşınmasını ifade eder.

**3.Bölüm:** Java sınıf yükleyici JVM ye programın çalışması için gerekli olan kütüphaneleri yükler ve byte kodu doğrular. JVM işletim sistemi ile program arasında köprüdür. Java yorumlayıcı ve JIT derleyici iki bölüm ayrılır.

**JIT:** Byte kodu okur ve önemli noktaları derler. Derleme işlemimi yaparken hız optimizasyonu yaparak kodun hedef sistemde hızlı çalışmasını sağlar.[Daha ayrıntılı bilgi için tıklayınız.](http://www.wiki-zero.co/index.php?q=aHR0cHM6Ly90ci53aWtpcGVkaWEub3JnL3dpa2kvSklU)

JVM uygun birçok programlama dili geliştirilmiştir. Bir grup yazılımcı Java’nın yetersiz olduğun yönleri düşünerek Scala geliştirmiştir. Vikipedia’dan bir kısmını kopyaladım.[Buradan](https://en.wikipedia.org/wiki/List_of_JVM_languages) inceleyebilirsiniz. Bununla birlikte direkt Java kullanmadan **JVM** üzerinde kod yazabilirsiniz. Öyle bir niyetiniz varsa sizi [buraya](https://dzone.com/articles/introduction-to-java-bytecode) yönlendirebilirim.

•    Clojure, a functional Lisp dialect
•    Groovy, a dynamic programming and scripting language
•    JRuby, an implementation of Ruby
•    Jython, an implementation of Python
•    Kotlin, a statically-typed language from JetBrains, the developers of IntelliJ IDEA
•    Scala, a statically-typed object-oriented and functional programming language

**JVM** kendi içinde öbek (*heap*) ,yığın (*stack*) , metot bölümü ve program sayaçları(*register*) olan belleğe sahiptir. Byte kodlar birtakım işlemlerden-JIT ve Interpreted- sonra belleğe alınır ve makine(*Execute Engine*) tarafından çalıştırılır.

Hemen hemen her sisteme uygun bir JVM vardır. **Google Android** için üretilmişti.  **Oracle** davası açması sonucu tazminat ödemeye mahkûm edildi. Microsoft **J#** bir dil çıkarmış karşı dava sonucunda **J#** teknolojisini sonlandırmış ve **JVM** ile benzer mantıkta işleyen **.Net** geliştirmiştir.

- **Java güvenlidir.**

Bellek yönetimi programcıya bırakılmamıştır. Güçlü tip sistemine sahiptir. Hem derleme hem de çalışma zamanında tip uyumu kontrol edilir. Güvenlik kod açığı (*exploit*) çok az bulunmuş ve hemen kapatılmıştır.

-          **Java yüksek performanslıdır.**

Java programcısı eğitimli ise Java kodu hızlıdır. Bununla birlikte Java çalışma zamanında performansı attırmak için derlenme zamanında kod optimizasyonu yapar. **Akın Hoca**'nın güzel ve bir o kadar yaralı makale serini [burdan]( <http://www.javaturk.org/java-yavas-mi-javanin-performansi-uzerine-i/>) okuyabilirsiniz.

- **Java çok kanallı yapıyı (thread) ve Ağ programlamayı destekler.**
- **Java 3 tane sürümü vardır.**
  - Standart Java (Standard  Edition, SE), çekirdek dildir. En son 9. sürümü çıkmıştır.
  - Mikro Java (Micro Edi5on, ME),  gömülü ve mobil ortamlar içindir. En son 8. sürümü çıkmıştır.
  - Kurumsal Java (Enterprise Edition, EE), kurumsal uygulamalar içindir. En son 8. sürümü çıkmıştır.
-  **Java şartname temellidir.**

Aynı şartname kullanarak birden çok ürün vardır.(**openjdk** vb.leri ) Aynı işlemi farklı yollarla yapan – örnek ağ programlama- kütüphaneye sahiptir.

- **Java yazılım mimarisine ve tasarım şablonları önem verir. Onları kullanmaya zorlar.**

İyi bir modelleme ile yazılmış 100 satır kod derme çatma **PHP** yazılmış 1000 koda aynı işi yapabilir.

-          **Popülerlik**

**Amazon**’daki kitap sayısı, **Stackoverflow**’daki girdi işlemlerine bakılarak en popüler dil olduğu anlaşılabilir. **Dünya** çapında kurumsal olarak genellikle Java tercih edilir.

**Türkiye** ise **.Net** sonra ikinci sıradadır. Çünkü bir daha çok tasarım yapmaktan ziyade hazır teknolojiler olan sürükle bırak yöntemini tercih ediyoruz. Bu noktada **.Net**’ten üstündür demiyorum. Sadece Microsoft’un hazır mekanizmalar sunması sebebiyle yazılımcıları belirli bir alana ile sınırlamıştır. Tatbikîde tasarım yapılarak yazılmış bir kod değil **.Net** hangi dil ile yazılmış olursa olsun, Java'da özentiden ve tasarımdan yoksun yazılmış bir yazılımdan kat ve kat üstündür.

