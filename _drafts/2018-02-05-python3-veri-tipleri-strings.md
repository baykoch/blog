---
title: "Python Veri Yapıları 2. Karakteri Dizileri"
last_modified_at:
categories: 
  - Python
tags:
  - strings
toc: true
toc_label: "Python Strings"
author_profile: True
mathjax: true
---

Programlama dillerinde kullanılması kaçınılmaz olan metinleri ifade etmek için kullanılırlar. Python `strings` hakkında bazı noktalara değinelim.

- Tek, çift veya 3'lü tırnaklar içinde gösterilebilirler.
    - Tek tırnak `'metin'` sembolik kısa ifadelerde kullanılması önerilir(dict keys, regular expressions, SQL vb).
    - Çift tırnak `"metin"` daha uzun kelime gruplarının ifadesinde kullanılır.
    - 3'lü tırnak ise `"""metin"""` daha çok  [`docstrings`](https://www.python.org/dev/peps/pep-0257/)  oluşturmak için yazılan yorum satırlarında tercih edilir.
       
       ```python
       # Tek tırnal sembolik kısa ifadelerde 
       list1 = ['Fizik', 'Kimya', A, C];

       # Çift tırnak uzun ve semblik olmayan kısa metinlerde 
       str = "Merhaba Dünya"

       # 3'lü tırnak docstring için yazılan yorum satırlarında
       def function(a, b):
       """Do X and return a list."""
       ```

- Python `char` tek bir karakteri ifade eden veri tipi bulunmaz, yani bütün metin ifadeler `string`'dir. 
- Python `string` ilgili bir çok yararlı modül ve kütüphaneler yazılmıştır. Bu yüzden metinlerle ilgili bir çok problemlerin çözümünde sık tercih edilen programlama dilidir.
- `string` dizilerin özelliklerine sahiptirler. İlk eleman 1 ile değil `0` başlar. Herhangi bir indisdeki karaktere veya bir kısmına ulaşılabilir.
   
```python
str = "Merhaba Dünya"
print("Örnek metin      :",str)         # str'ini değerinin 
print("Metinin Uzunluğu :",len(str))    # String'in uzunluğunu gösterir.
print("str[0]           :",str[0])      # İlk karakter verir. 
print("str[6]           :",str[6])      # 7. karakter verir.
print("str[:7]          :",str[:7])     # Baştan 0-7 arasındaki bölüm 
print("str[8:]          :",str[8:])     # 8-13 arasındaki bölüm
print("str[3:11]        :",str[3:11])   # 3-11 arasındaki bölüm
print("str[1:12:3]      :",str[1:12:3]) # Metinin harflerini 1. indisten 12. indise kadar 2şer 2şer alır.
print("str[:]           :",str[:])      # Metni kopyalamanın kısa yolu
```

{% include figure image_path="/assets/images/python3-data-string.png" alt="Integer" caption=""%}

### Escape Characters

Yorum satırları veya `print` gibi madulü içinde çift tırnak ile verilen bilgi amaçlı metinleri yorumlayıcı düz metin olarak kabul eder. Tam bu noktada işlevselliği artırmak için bazı karakterlere özel anlamlar yüklenir. Bu karakter kaçış yani `escape` karakter denir. Bu karakter bir çoğu aşağıdaki tabloda verilmiş, bir örnekle konu taçlandırılmıştır.


| Escape Dizge | Anlamı                        | Notlar |
|:-----------------:|--------------------------------|-------|
| \newline        | Backslash                      | Yeni satır yok sayılır.      |
| \\              | Backslash (\)                  | Slash gösterir.  |
| \'              | Single quote (')               | Tek tırnak gösterir. |
| \"              | Double quote (")               | Çift tırnak gösterir. |
| \a              | ASCII Bell (BEL)               | Bip sesi verir.      |
| \b              | ASCII Backspace (BS)           | İmleçi bir karakter geri alır. |
| \f              | ASCII Formfeed (FF)            | Yeni satırda kaldığı yerden devam eder.|   
| \n              | ASCII Linefeed (LF)            | Yeni satırda en baştan devam eder.|
| \r              | ASCII Carriage Return (CR)     | Satır başı yapar ve üzerine yazar. |
| \t              | ASCII Horizontal Tab (TAB)     | Dikey Tab.     |
| \v              | ASCII Vertical Tab (VT)        | Yatay Tab.      |
| \ooo            | Character with octal value ooo | Octal karakterler       |
| \xhh            | Character with hex value hh    | Hex karakterler      |

        
```python 
print("1.Merhaba\
Dünya")                         # Yeni satırı yok sayar.
print("2.Merhaba\\Dünya")       # Backslash gösterir. 
print("3.Merhaba\'Dünya")       # Tek tırnak gösterir.
print("4.Merhaba\"Dünya")       # Çift tırnak gösterir. 
print("5.Merhaba\aDünya")       # Bip sesi verir.  
print("6.Merhaba\bDünya")       # İmleçi bir karakter geri alır.
print("7.Merhaba\fDünya\fMars") # Yeni satırda kaldığı yerden devam eder. 
print("8.Merhaba\nDünya")       # Yeni satırda en baştan devam eder. 
print("9.Merhaba\rDünya")       # Satır başı yapar ve üzerine yazar.
print("10.Merhaba\tDünya")      # Dikey Tab. 
print("11.Merhaba\vDünya")      # Yatay Tab.
# MerhabaDünya octal sistemede yazılımı
print("12.\115\145\162\150\141\142\141\104\374\156\171\141") 
# MerhabaDünya hex sistemede yazılımı
print("13.\x4d\x65\x72\x68\x61\x62\x61\x44\xfc\x6e\x79\x61") 
```
{% include figure image_path="/assets/images/python3-data-escape.png" alt="Integer" caption=""%}

### Escape Karakteri Yok Sayma

`Escape` karakterleri `r` parametresi  kullanılarak yok sayılabilir.
Örnek vermek gerekirse geliştirilmekte olduğumuz bir programda dosya okuma işlemi yapmamız gerekiyor. Dosya yolu `C:\new\testdb.db'` olsun. Dosya yolundaki `\n` karakteri yeni satıra anlamına geldiğini için dosyaya ulaşamayacağız. `r` kullanmanızdaki amaç  bu gibi karakterlerin işlevlerini yetkisiz kılmaktır.

```python 
path_no_escape = 'C:\new\testdb.db' # Dosya yolu r parametresiz kullanım.
path_escape = r'C:\new\testdb.db'   # Dosya yolu r parametresiyle kullanım.

print("Hatalı Kullanım : ",path_no_escape)
print("Doğru Kullanım  : ",path_escape)
```
{% include figure image_path="/assets/images/python3-data-raw-escape.png" alt="Integer" caption=""%}

### String Conversion Tool

### String Formatting

### String Fonksiyon ve Methodlar

## Lists

## Dictionaries

## Tuples

## Sets 

### Frozenset




































