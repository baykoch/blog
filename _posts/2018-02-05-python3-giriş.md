---
title: "Python Derslerine Giriş"
last_modified_at:
categories: 
  - Python
tags:
  - Python Pep8 
toc: true
toc_label: "Python Giriş"
author_profile: True
mathjax: true
---

Yapa zeka ilgili çalışmalar yaparken Python'u sıkça kullanmak zorunda kaldım. Hem takıldığım unuttuğum noktaları anımsamak hem de yurdumun insanlarına istifadesine sunmak için eğitim serisi olarak yazmaya karar verdim. Bazı önemli hususları yazarak başlayalım:
 - Geniş çaplı ve detaylı olmayacak.
 - Amacım pratik, etkili ve hızlı bir şekilde öğrenmeyi sağlamak.
 - Yazıların merkez odak noktası Python 3. versiyonu olacak. 

## Python3 Genel Bakış

**Python is Interpreted** − Python satır satır yorumlanır. Programın tamamını çalıştırmak için bütün programı derlemeye ihtiyaç duymaz.

**Python is Interactive** − Bilgisayar uç birimde(Terminal) kod yazılabilir ve çaşıltırabilir.

**Python is Object-Oriented** − Nesneye yönelik programlama yöntemini destekler.

**Python is Easy** − Python söz dizilimi diğer dillere göre daha kolaydır.

## Python3 Kurulum

### Linux 

```
sudo apt-get install python3
```
### Windows 

Python3 [indirme](https://www.python.org/downloads/windows/) sayfasından kolayca indirilip kurulabilir.

### Geliştirme Ortamı
Aşağıda bazı ücretsiz geliştirme ortamlarını sıraladım.Beğendiğiniz  herhangi bir tanesini kullanabilirsiniz.

1. [VSCode](https://code.visualstudio.com/).
2. [Atom](https://atom.io/)
3. [Sublime Text](https://www.sublimetext.com/).Ücretli olmasına rağmen kayıt yapmadan kullanılabiliyor.
4. [Anaconda](https://www.anaconda.com/download/#linux).Herhangi bir ekstra kuruluma ihtiyaç duymuyor.


## Python3 PEP Yazım Kuralları

Python kodunda kullanılacak isimlendirme ve şekil (format) standartları aşağıda sıralanmıştır.

### Boşluk(Whitespace)  
Python3 Java dillerini aksine süslü parantezle(\{\}) blokları ayırma söz dizimini kullanmaz.Süslü parantez yerine boşluk kuralları ile bloklar tanımlanır.Bu nedenle boşluk (space) Python'da çok önemlidir.Yazılan kodun temizliği için boşluk kullanımda hassas davranmalıdır.
 - `Tab` tuşu yerine `Space` tuşu kallan
 - Blok ve seviyeler için 4 boşluk kullanılmalı
 - Python maksimum satır uzunluğu 79 karakteri geçmemeli 
 - Uzun ifadeler  eğer bölünecekse ikinci satır 4 boşluk ile başlamalı
 - Bir python dosyasında fonksiyon ve sınıflar 2 boş satır ile ayrılmalı
 - Sınıflar içindeki metotlar boş bir satır ile ayrılmalı
 - Değer atamalarında exp ifadeden önce ve sonra boşluk bırakılmalı
 
### İsimlendirme

 - Fonksiyonlar, değişkenler ve nitelikler(attribute) küçük harflerle yazılmalı kelime geçişlerinde altı çizgi kullanılmalı `lowercase_underscore`
 - `Protected` erişim belirleyici altı çizgili ile başlanmalı`_leading_underscore`
 - `Privete` erişim belirleyici iki tane altı çizgili ile başlanmalı `__leading_underscore__`
 - Sınıflar ve istisnalar büyük harf ile kullanılmalı `CapitalizedWord`
 - Sabitler büyük harflerle yazılmalı `ALL_CAPS`
 - Sınıf içindeki nesne örnekleri `self` kelimesi ile belirtilmeli
 - Sınıfların metotları `cls` kelimesiyle belirtilmeli

### İfadeler ve Durumlar (Expression and Statements)

 - Mantık ifadelerinde ilk varsayımı her zaman negatif olarak kabul et! 
    
    ```
    if a is not b <-- Hatalı
    if not a is b <-- Doğru
    ```

 - Boş değerleri kontrol etme `[] veya ''`. Değerlerin uzunluklarını kontrol et! `if len(somelist) ==  0`
 - Boş değerler "if not somelist" False, boş olmayan değerler "if somelist" True değeri verir.
 - `if`, `for`, `while` ve `try-except` ifadelerini tek satırda yazma!
 - `import` ifadelerini dosyanın en üst kısmında yaz!
 - Bütün kütüphaneyi değil sadece gerekli modülü `import` et! `from math import integral`
 - `Import` kelimesi kullanırken şu sıra takip edilmeli: 
    1. Standart kütüphane modülleri
    2. Üçüncü-parti modüller
    3. Kendi modüllerimiz. 
    - Her `import` iç bölgesinde alfabetik sıraya riayet edilmelidir.
 - [], {} veya () içinde yazılan ifadeler satırlara sığmayıp yeni satıra geçilecekse  ifade bütünlüğünü korumak için `\` karakterini kullan.
 - Python tek tırnak `''`, çift tırnak `""` ve `"""` üçlü tırnağı destekler.Üçlü tırnak ifadenin yeni satırlara taşmasına izin verir.
   ```python
    deyim = """ Yer demir 
              gök bakır"""
   ```



