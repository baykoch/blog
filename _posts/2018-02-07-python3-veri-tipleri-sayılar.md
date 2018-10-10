---
title: "Python Veri Yapıları 1. Sayılar"
last_modified_at:
categories:
  - Python
tags:
  - integer
  - boolean
  - complex numbers
  - floating point numbers
  - bitwise operators
toc: true
toc_sticky: true
toc_label: "Python Numbers"
author_profile: True
mathjax: true
---

Bilgisayarların yaptığı tek iş aslında verileri yönetmek, onlar üzerinde tanımlanan işlerleri gerçekleştirmektir. Bu veriler birçok biçimde olabilir: müzik, film, belge... Bu bölümde Python'un verilere nasıl yaklaştığını  ve hangi tür verilere sahip olduğunu incelemeye çalışacağınız.

İlk olarak bilmemiz gereken nüans Python'da her şey birer nesne`object`dir. Bu nesneden kasıt Java'daki gibi nesnenin öznitelik`attribute` ve metotlarında oluşması gerekmez. Bu noktada aktarılmak istenen nesne: Değer atanabilir olması veya fonksiyonlara argüman geçilebilmesidir.[Python'da Nesne Kavramı](http://www.diveintopython.net/getting_to_know_python/everything_is_an_object.html)

## Python Varsayılan Veri Tipleri

Her programlama dillerinin dışarıdan herhangi bir kütüphaneye ihtiyaç duymadan, yerleşik desteklediği veri tipleri vardır.Python veri tiplerine yaklaşımı biraz farklıdır, değişkenlerini tiplerini belirmek için isim etiketlerine (Integer,String vb.) ihtiyaç duymaz. Aklımıza Python'nun eğer biz belirtmezsek değişkenin `integer` veya `string` olduğunu nasıl anlıyor sorusu takılabilir. Bu soruyu  Python dinamik atama yapması ile  açıklarız. Python atanan değerin  içeriğine bakar sayi ise `integer` karakter dizi ise `string` vb. olarak işlemine devam eder.

```python

veri_tipi = 3         #veri_tipi 3'e bağlandı. Python bu değişkeni integer olarak kabul eder.

veri_tipi = "Merhaba" #Bu satırda ise aynı değişkene karakter dizisi atanmış ve string olarak kabul eder.
```

Tablo halinde Python'daki varsayılan veri tiplerini görelim.

| Nesne Tipi    |           Örnek             |
|-------------- | --------------------------- |
| Numbers       | 25 , 3.1415 , 5+7j , 0b1010 , Decimal() , Fraction() , True                   |
| Strings       | 'Merhaba', " Veli'nin ", """ Türkiye """                           |
| Lists         | [3, [5, 'five'], 4.5] , list(range(5))                          |
| Dictionaries  | {'food': 'imam bayıldı', 'drink': 'ayran'} , dict(hours=10)                          |
| Tuples        | (1, 'test', 4, 'U') , tuple('test'), namedtuple                          |
| Sets/Frozenset| set('abc') , {'a', 'b', 'c'}                          |
| Byte   | bytearray("Merhaba" 'utf-8')                        |



## Numbers

Python sayı tiplerine geçmeden önce dilin bazı karakterlere yükledikleri matematiksel anlamları bir tablo ile özetleyelim.

| Operatör         | Tanım | Örnek                  |
|:------------------:|-------------|--------------------------|
| +  | Operatörün sağ ve solundaki değerleri toplar.        | s = x + y              |
| -  | Operatörün sağ ve solundaki değerleri çıkarır.          | s = x - y               |
| *  | Operatörün sağ ve solundaki değerleri birbiri ile çarpar.     | s = x * y               |
| /  | X değerini y değerine böler. | s = x / y               |
| %  | X değerini x'ye bölümünden kalanı  verir.  | s = x % y                 |
| ** | X değerinin y kez çarpma işlemidir.      | s = x ** y  |
| // | Bölme işlemini sonucunu tam sayıya yuvarlar. |    s = x // y                       |



### Integer

 Python `integer` (tam sayı) büyüklük bakımından herhangi bir kıstasa sahip değildir.Python koşulduğu cihazın bellekte bölgesine sığabilecek büyüklükte `integer` değeri tanımlanabilir. Integer değeri pozitif negatif veya sıfır değeri alabilir. Python `integer` değişkeni ile yapabileceklerimize göz atalım.
```python
x = 7
y = 4
result = 0
result = x + y
print ("Toplama         : ", result)
result = x - y
print ("Çıkarma         : ", result)
result = x * y
print ("Çarpma          : ", result)
result = x / y
print ("Bölme           : ", result)
result = x % y
print ("Modül Alma      : ", result)
result = x**y
print ("Üst Alma        : ", result)
result = x//y
print ("Aşağı Yuvarlama : ", result)
```

{% include figure image_path="/assets/images/python3-data-integer.png" alt="Integer" caption=""%}




### Booleans

Mantıksal veri tipleridir.Önermelerin gerçekleşebilmesi bilmesi veya durumları kontrol ermek için kullanılır. `True` ve `False`  olmak üzere 2 değerine  sahiptir. Aslında burda `True` 1 değerine `False`  0 değerine  eşittir.



### Floating Point Numbers

Python kayan noktalı sayıları [IEEE 754](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) standartlarına göre 64-bit(32 bit desteklemez) uzunlukta ve 3 bölüm halinde ifade eder:sign, exponent, and mantissa.

- Sign (1 Bit)      : 0 ise sayı pozitif, 1 ise sayı negatifidir.
- Exponent (11 Bit) : Sayının  üstel kısmı kodlanır.
- Mantissa (52 Bit) : Sayının kesirli kısmı kodlanır.

```python
x = 225.455 ** 7    # x = 2.960868358019457e+16

print (3*0.1 - 03)  # Sonuç neden 0 değil ?
```

### Complex Numbers

Karmaşık sayılar elektrik başta olmak üzere birçok mühendislik alanında kullanılmaktadır. Python karmaşık sayıları destekler.

```python
#Karmaşık Sayılarda İşlemler

c = 6 + 2j
c2 =4.2 + 5.1j

print("Real Kısmı  :", c.real)  
print("Sanal Kısım :", c.imag)
print("Carpma      :", c * 2)
print("Toplama     :", c + c2)
print("Çıkarma     :", c - c2)
print("Üst alma    :", c ** 2)
```
{% include figure image_path="/assets/images/python3-complex-data.png" alt="Integer" caption=""%}

### Decimal and Fraction  

Bilgisayar biliminde sayılar IEEE 754 standartlarına göre ifade edildiğinden bahsetmiştik. İEEE 754 bazı sayı göstermede bazı kısıtlamalara sahiptir.Yani `0` ve `2^−126` arasındaki sayılar gösterilemez.İkinci önemli hususta sayıların ondalık kısmını sabitlemek isteyebiliriz.

1. Gösterilmeyen sayılara çözüm getirme;
   ```python
   from decimal import Decimal
   
   float_issue = 0.1 * 3 - 0.3
   float_issue_fix = Decimal('0.1') * Decimal('3') - Decimal('0.3')
   
   print(float_issue)
   print(float_issue_fix)
   ```
   > 5.551115123125783e-17
   >
   > 0.0

2. Örnek olarak telefon lira  kullanımı ile ilgili bir program hazırlayalım.Dakika başına 2.45 lira kesimi yapalım. Programı `decimal` modülüne kullanmadan ve kullanarak yazalım. Dikkat ederseniz sayının ondalık kısmı çok şişirilmiş iken `getcontext` kullanarak ondalık kısmı belirli bir uzunlukta sabit tutabiliriz.  
   
   ```python
   from decimal import Decimal, getcontext

   getcontext().prec = 3     # Sayı hassaslığını belirtiyoruz.
 
   rate = Decimal('2.45')
   seconds = Decimal('222') # 3*60 + 42
   pre_cost = rate * seconds / Decimal('60')

   rate = 2.45
   seconds = 3*60 + 42
   cost = rate * seconds / 60

   print(cost)
   print(pre_cost)
   ```

   > 9.065000000000001
   >
   > 9.07

3. Örneğimizde eğer dakika başına ücret `0.05` olsaydı. Lira ücret hesaplaması bize sıfır değerini verecekti. Böyle istemediğimiz sonuçlardan kurtulmak için sayıları aşağıya veya yukarı yuvarlama işlemine tabii tutabiliriz.(_quantize_)

   ```python
   rate = Decimal('0.05')
   seconds = Decimal('5')
   cost = rate * seconds / Decimal('60')
   print(cost)

   rounded = cost.quantize(Decimal('0.01'), rounding=ROUND_UP)
   print(rounded)
   ```
   > 0.00417
   >
   > 0.01

Kesirli sayılarda işlem yapmak için `Fraction` modülü kullanabilir.

 ```python
from fractions import Fraction

x = Fraction(2, 5)
y = Fraction(2, 3)
result = a + b # 2/5 + 2/3 = 16/15
print(result)
 ```

> 16/15

### Hex, Octal, Binary

Hex,octal ve binary sayıları göstermek için aşağıda belirtilen notasyonları kullanılır.
- Hex     : `0o`
- Octal   : `0X`
- Binary  : `0b`

Örnek olarak `64` sayısının farklı sayı sistemlerinde kullanımı yazılmıştır.

 ```python
print("Hex :",0x40,"Octal :",0o100,"Binary :",0b1000000)
 ```

> Hex : 64 Octal : 64 Binary : 64


### Bitwise Operators

[Byte](https://tr.wikipedia.org/wiki/Bayt) seviyesinde yapılan operasyonları tablo halinde görelim.

| Operator | Description                             | Example                                   |
|:----------:|-----------------------------------------|-------------------------------------------|
| &        | AND Bitlerin çapımı gibi davranır.      |  0&0 = 0, 0&1 = 0 ,1&0 = 0, 1&1 =1      |
| \|        | OR Sadece bitler 0 ise 0’dır.           |  0\|0 = 0, 0\|1 = 1 ,1\|0 = 1, 1\|1 =1  |
| ^        | XOR Bitler aynıysa 0 farklı ise 1’dir.  | 0^0 = 0, 0^1 = 1 ,1^0 = 1, 1^1 =0       |
| ~        | One’s Complement Bitlerin tersini alır. | ~0b0110 = 0b1001                        |
| «        | Left Shift Sola kaydırır.               | 0b0011 << 2  = 0b1100  |
| »        | Right Shift Sağa kaydırır.              | 0b0011 >> 1  = 0b0001  |


```python
x = 19            # 19 = 0001 0011
y = 7             # 7 = 0000 0111

print ('x decimal değeri      :',x,'Binary  :',bin(x))
print ('y decimal değeri      :',y,' Binary  :',bin(y))

result = x & y;        # AND
print ("AND Operation         :", result,'Binary:',bin(result))

result = x | y;        # OR
print ("OR Operation          :", result,'Binary:',bin(result))

result = x ^ y;        # XOR
print ("XOR Operation         :", result,'Binary:',bin(result))

result = ~x;           # Complement
print ("Complement Operation  :", result,'Binary:',bin(result))

result = x << 2;       # LEFT SHIFT
print ("LEFT SHIFT Operation  :", result,'Binary:',bin(result))

result = x >> 2;       # RIGHT SHIFT
print ("RIGHT SHIFT Operation :", result,'Binary:',bin(result))
```

{% include figure image_path="/assets/images/python3-data-bitwise.png" alt="Integer" caption=""%}








































