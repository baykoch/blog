---
title: "Markdown Nedir? Nasıl Kullanılır?"
last_modified_at:
categories:
  - Markdown
tags:
  - Kramdown
toc: true
toc_sticky: true
toc_label: "Markdown"
author_profile: True
mathjax: true
---

_Markdown_ bahsetmeden önce işaret dili _(markup language)_ nedir ondan biraz bahsedelim. İşaret dili metinleri nasıl biçimlendirileceğini belirlememize yarayan yapay dildir. Bilgisayar dünyasında en çok bilinen örneği HTML'dir.

_Markdown_ hızlı pratik ve HTML gibi kodlama gerektirmeyen herkese hitap eden basit veya diğer tabirle insancıl metin işleme dili diyebiliriz. *Markdown* günümüzde hemen hemen her yerde karşımıza çıkmaktadır. Bu ziyaret ettiğiniz bir forum sayfasında veya bir programın kullanım kılavuzu da olabilir. *Markdown* en güzel tarafı HTML bilmeden blog sayfaları yazabiliyoruz. Hemen hemen bütün online içerik yönetim sistemleri `Wordpress, Getgrav, Hugo, Jekyll` ve benzeri teknolojiler tarafından desteklenir. _Markdown_ formatında yazılan içerik [**CMS**](https://tr.wikipedia.org/wiki/%C4%B0%C3%A7erik_y%C3%B6netim_sistemi) tarafından HTML formatına çevirir.Bu derslerde github ve gitlab gibi **Git** tabanlı web servislerin  desteklediği **_Kramdown_** anlatılacak.

## Başlıklar

Başlık boyutu **h2** ile **h6** aralığında olabilir. Başlık her zaman **h2** ile başlamalı, kullanım sırası ardışık artan (h2 → h3 → h4) şekilde olmalıdır.

**Uyarılar:**
​    Web sayfalarında **h1** sayfa başlığı olarak kullanıldığından içerik kısmında kullanımı önerilmemektedir.
​    Hash Tag (**\#**) işaretinden sonra bir boşluk,
​    başlık ve paragraf arasında ise bir cümle bırakılmalıdır.
{: .notice--warning}

~~~~~~~~
###   Başlık h2
####  Başlık h3
##### Başlık h4
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>
>###   Başlık h2
>####  Başlık h3
>##### Başlık h4

## Paragraflar, Boşluklar ve Yatay Çizgi

Paragraflar sadece düz yazı stili sağlar. Paragraflar arası bir boşluk için bir satır, çoklu boşluk için **<\br>** etiketi
kullanılmalıdır.  

~~~~~~~~
Birinci paragrafın birinci cümlesi.
Birinci paragrafın ikinci cümlesi.
<!-- boş satır -->
İkinci paragrafın  cümlesidir.
<!-- boş satır -->
<br>
<!-- boş satır -->
Üçüncü paragrafın cümlesidir.
~~~~~~~~
<span style="color:#26A4C8"> **_SONUÇ_** </span>

>Birinci paragrafın birinci cümlesi.
Birinci paragrafın ikinci cümlesi.
>
> İkinci paragrafın  cümlesidir.
>
> <br>
>
> Üçüncü paragrafın cümlesidir.


## Vurgu: Eğri ve İtalik Yazı

Kalın vurgu için yıldız (\*\*), italik yazı gösterimi için alt tire (\_) kullanılır.
~~~~~~~~
**kalın** _italik_
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

> **kalın** _italik_

## Bağlantılar (Links)

Bağlantı paylaşımında köşeli parantez ve onu takip eden normal parantez **_\[Site bağlantısını içeren metin\]\(Site bağlantısı\)_** kullanılır.

~~~~~~~~
[Blog Sitem](https://baykoch.github.io/blog/)
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

>[Blog Sitem](https://baykoch.github.io/blog/)

### Tanımlayıcı Kullanımı

Aynı sayfada linklerin tekrar kullanımı söz konusu olduğunda tanımlayıcı kullanabiliriz.

~~~~~~~~
[Markdown Dersleri][Markdown Tanımlayıcı]

[Örnek Link][Örnek Tanımlayıcı]

<!-- Tanımlayıcılar -->
[Markdown Tanımlayıcı]: https://baykoch.github.io/blog/
[Örnek Tanımlayıcı]: https://example.com

~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

>[Markdown Dersleri][Markdown Tanımlayıcı]
>
>[Örnek Link][Örnek Tanımlayıcı]

[Markdown Tanımlayıcı]: https://baykoch.github.io/blog/
[Örnek Tanımlayıcı]: https://example.com

## Listeler

**Markdwon** sıralı ,sırasız ve ayrık liste kullanmaya imkan veriyor.Dikkat etmemiz gereken  birkaç nokta var; listelerden önce ve sonra bir satır atlamalı, iç içe liste için üç boşluk karakter ve ayrık listesi için `^` özel karakteri kullanılmalıdır.
~~~~~~~~
Sıralı Liste
<!-- boş satır -->
1. Madde Bir
   1. İç Madde Bir
   2. İç Madde İki
2. Madde İki
<!-- boş satır -->
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

>**Sıralı Liste**
>
>1. Madde Bir
>    1. İç Madde Bir
>    2. İç Madde İki
>2. Madde İki

### Sırasız Liste

Tire(\-) kullanarak sırasız liste kolayca oluşturulabilir.
~~~~~~~~
Sırasız Liste
<!-- boş satır -->
- Madde 1
- Madde 2
- Madde 3
   - İç Madde  1
   - İç Madde 2
- Madde 4
<!-- boş satır -->
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>
>**Sırasız Liste**
>
>- Madde 1
>- Madde 2
>- Madde 3
>   - İç Madde  1
>   - İç Madde 2
>- Madde 4

### Ayrık Liste

Ardışık iki listeyi ayırmak için şapkalı parantez (^) kullanılır.

~~~~~~~~
Ayrık Liste
<!-- boş satır -->
- Liste Bir - Madde 1
- Liste Bir - Madde 2
^ --> İki listeyi birbirinden ayırmak
- Liste İki - Madde _i_
- Liste İki - Madde _ii_
<!-- boş satır -->
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

>**Ayrık Liste**
>
>- Liste Bir - Madde 1
>- Liste Bir - Madde 2
>^
>- Liste İki - Madde _i_
>- Liste İki - Madde _ii_

## Tablolar

Markdown formatında tablo kullanmak biraz zahmetli.

~~~~~~~~
| Başlık1 | Başlık2 | Başlık3 |
|:--------|:-------:|--------:|
| Hücre1   | Hücre2   | Hücre3   |
| Hücre4   | Hücre5   | Hücre6   |
|----
| Hücre1   | Hücre2   | Hücre3   |
| Hücre4   | Hücre5   | Hücre6   |
|=====
| AltHücre1   | AltHücre2  | AltHücre3
~~~~~~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

| Başlık1 | Başlık2 | Başlık3 |
|:--------|:-------:|--------:|
| Hücre1   | Hücre2   | Hücre3   |
| Hücre4   | Hücre5   | Hücre6   |
|----
| Hücre1   | Hücre2   | Hücre3   |
| Hücre4   | Hücre5   | Hücre6   |
|=====
| AltHücre1   | AltHücre2  | AltHücre3


**Uyarılar:**
​    Markdown formatı yerine HTML kullanılarak tablo oluşturulması  daha kolaydır.[HTML tablo oluşturucu](http://www.tablesgenerator.com/html_tables) kullanarak kolayca tablo oluşturabiliriz.
{: .notice--info}

## Kod Blokları

Kod blok gösteriminin birkaç yolu var.En yaygın kullanım biçimi tek tırnak ve tek tırnağı takiben hangi programlama dili olduğunun yazılmasıdır.

~~~
```ruby
def hello
   puts "Hello world!"
end
```
~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

~~~ ruby
def hello
   puts "Hello world!"
end
~~~
#### Özel Karakterlerden Kaçma

Markdown birçok özel karakterden bahsettik. Bu  karakterlerin özelliklerini devre dışı bırakmak için önlerine `\` getirilir.

### GitHub Gist

Github Gist kod paylaşım platformudur. GitHub hesabınızla giriş yaptıktan sonra oluşturduğunuz kod bloklarını sağ üst köşedeki **emded** kısımdan kopyalayarak paylaşabilirsiniz.

```
<script src="https://gist.github.com/baykoch/757b2c4c7d1c69ffe13a46a737658b0f.js"></script>
```

<span style="color:#26A4C8"> **_SONUÇ_** </span>

<script src="https://gist.github.com/baykoch/757b2c4c7d1c69ffe13a46a737658b0f.js"></script>

### Liste İçinde Kod Blokları

Liste içinde kod blok paylaşmak için yapılması gereken ek olarak satır başlarını 4 tane boşluk bırakmaktır.

1. Kod bloğunun başında ve sonunda  3 tane tire (\`) bırak.
2. İlk 3 tireden sonra  kod bloğunun tanımını belirt.
   
   ```css
    p {
    font-family: "Times New Roman", Times, serif;
    font-size: 30px;
    color: blue;
   }
   ```
   
3. Liste içinde gösterim için 4 tane boşluk bırak.

## Markdown + HTML

**Markdown** sade ve bir o kadar da kısıtlı.Kısmen özelleştirme yapmamıza izin vermiyor. Sayfa içeriğine  güzellik ve estetik katmak istersek HTML ile CSS kullanmamız kaçınılmaz oluyor. Fazla ayrıntıya girmeden kısa anekdotlardan bahsedelim.

### Classes, IDs, and Attributes

Markdwon `class id and attribute` destekler. CSS dosyanın içeriğini aşağıdaki gibi tanımlamış olalım.

```
#kırmızımetin{
    color: red;
}
```

Şimdi herhangi bir metne **#kırmızımetin** etiketi tanımlayarak kırmızı renkli yapabiliriz.

```
Kırmızı metin.{:#kırmızımetin}
```
<span style="color:#26A4C8"> **_SONUÇ_** </span>

> <span style="color: red"> Kırmızı metin.</span>


### Metin Renklendirme

Metni iki farklı yordam  ile renklendirebiliriz.HTML **span** etiketi içinde belirterek veya bir önceki başlıkta mevzu bahis edilen CSS yöntemi uygulanabilir.

~~~
<span style="color:blue"> Mavi renkli metin. </span>

Kırmızı renkli metin.{: #kırmızımetin}.
~~~

<span style="color:#26A4C8"> **_SONUÇ_** </span>

> <span style="color:blue"> Mavi renkli metin. </span>
>
> Kırmızı renkli metin
> {: style="color: red"}


### Matematiksel İfadeler Ekleme

MArkdown matematiksel ifadeler gosterme kabiliyeti var. Ama bunun için [MathJax](https://www.mathjax.org/) kütüphanesine ihtiyaç duyuyor. Aşağıdaki betik parçasını sayfamıza ekleyerek işe koyulalım.


```
<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>

```
Daha sonra başlangıç ve bitişte çift dolar arasına istenilen matematiksel ifadeler yazılabilir.

#### Örnek İntegral Formülü

```
$$
\begin{align*}
  \int_a^b f(x)\,dx.
\end{align*}
$$
```
<span style="color:#26A4C8"> **_SONUÇ_** </span>
>$$
>\begin{align*}
>  \int_a^b f(x)\,dx.
>\end{align*}
>$$
>

**Notlar:** Matematik ifadeleri LaTex kullanılarak yazıldı. LaTex ilgi daha bilgi için [wiki](https://tr.wikibooks.org/wiki/LaTeX/Yeni_Ba%C5%9Flayanlar) sayfasını ziyaret edebilirsiniz. Vakit ayırabilirsen  LaTeX hakkında detaylı bir Türkçe kaynak hazırlamak isterim.
{: .notice--info}

### Resim ve Video Ekleme

HTML [figure](https://www.w3schools.com/tags/tag_figure.asp) etiketi kullanarak video veya resim eklenebilir.

{% include figure image_path="/assets/images/markdown-img.jpg" alt="Markdown" caption="Blog yazmak bu kadar kolay olmamıştı."%}

Yazımı burada noktalıyorum. Yararlı olması dileğiyle hoşçakalın.

**_ Faydalı Kaynaklar _**:

- [Gitlab Markdown Guide](https://about.gitlab.com/handbook/product/technical-writing/markdown-guide/)
- [Kramdown Syntax](https://kramdown.gettalong.org/syntax.html)
- [Google Markdown Guide  By Pete LePage](https://developers.google.com/web/resources/markdown-syntax)
- [Github Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
