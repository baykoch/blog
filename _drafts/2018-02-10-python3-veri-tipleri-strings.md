---
title: "Python Veri Yapıları 2. Karakteri Dizileri"
last_modified_at:
categories: 
  - Python
tags:
  - strings
toc: true
toc_sticky: true
toc_label: "Python Strings"
author_profile: True
mathjax: true
---

 Python `strings` hakkında bazı noktalara değinelim.

- Tek, çift veya 3'lü tırnaklar içinde gösterilebilirler.
    - Tek tırnak `'metin'` sembolik kısa ifadelerde kullanılması önerilir(dict keys, regular expressions, SQL vb).
    - Çift tırnak `"metin"` daha uzun kelime gruplarının ifadesinde kullanılır.
    - 3'lü tırnak ise `"""metin"""` daha çok  [`docstrings`](https://www.python.org/dev/peps/pep-0257/)  oluşturmak için yazılan yorum satırlarında tercih edilir.
      
       ```python
       # Tek tırnal sembolik kısa ifadelerde 
       list1 = ['Fizik', 'Kimya', A, C]

       # Çift tırnak uzun ve semblik olmayan kısa metinlerde 
       str = "Merhaba Dünya"

       # 3'lü tırnak docstring için yazılan yorum satırlarında
       def function(a, b):
       """Do X and return a list."""
       ```

- Python `char` tek bir karakteri ifade eden veri tipi bulunmaz, yani bütün metin ifadeler `string`'dir. 

- Python `string` ilgili bir çok yararlı modül ve kütüphaneler yazılmıştır. Bu yüzden metinlerle ilgili bir çok problemlerin çözümünde sık tercih edilen programlama dilidir.

- `string` dizilerin özelliklerine sahiptirler. İlk eleman 1 ile değil `0` başlar. Herhangi bir indisdeki karaktere veya bir kısmına ulaşılabilir.

- Sondan başa doğru indislere  -1 -2 ... girilerek ulaşılabilir. 

    ```python
    String     : p  y  t  h  o  n
    İndis      : 0  1  2  3  4  5
    Ters indis :-6 -5 -4 -3 -2 -1  
    ```

- İndisler tam sayı olmak zorundadır. Örnek hatalı kullanım: `str[1.5] ` 
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

- string değişkenler değişmez (immutable) nesnelerdir.  String üzerine yapılan birleştirme gibi işlemrin sonucunda yeni nense üretilir.

```python
str = "Hello" 
tr[2] = 2  # Hata!
str = str + " World"  # string değştirimedi yeni nensene oluşturuldu.
```

- `str` kurucusu kullanılarak diğer tiplerden string nesneleri üretilebilir. List,Tuple, Dictionary ve Set string cevirirklen herşeyi ile birlikte çevirir.

```python
from builtins import str
from fractions import Fraction
from _decimal import Decimal

if __name__ == '__main__':
   
    i = 2						#  int
    f = Fraction(2,3) 			#  Fraction (kesirli sayı)
    c = 2 + 3j					#  complex (karmaşık sayı)	
    dec = Decimal("0.7")    	#  Decimal (Ondalik sayı)
    l = [2,3,"3"]				#  list
    t = (2,3,5,6,"232")			#  tuple	
    d = {1:"Adana",25:"Erzurum"}#  dictionary
    s = {1,3,"Hi",5}			#  set
   
    f_int = str(i)  # from int : 2				
    f_dict = str(d) # from dict
    # Parantezler,virgüler vb. herşeyi olduğu gibi str cevirlir.
    print(test)   #  {1: 'Adana', 25: 'Erzurum'}
    # ...
	pass
```

### Escape Characters

Yorum satırları veya `print` gibi madulü içinde çift tırnak ile verilen bilgi amaçlı metinleri yorumlayıcı düz metin olarak kabul eder. Tam bu noktada işlevselliği artırmak için bazı karakterlere özel anlamlar yüklenir. Bu karakter kaçış yani `escape` karakter denir. Bu karakter bir çoğu aşağıdaki tabloda verilmiş, bir örnekle konu taçlandırılmıştır.

| Anlamı                         | Escape Dizge | Notlar                                  |
| ------------------------------ | :----------: | --------------------------------------- |
| Backslash                      |   \newline   | Yeni satır yok sayılır.                 |
| Backslash (\)                  |      \\      | Slash gösterir.                         |
| Single quote (')               |      \'      | Tek tırnak gösterir.                    |
| Double quote (")               |      \"      | Çift tırnak gösterir.                   |
| ASCII Bell (BEL)               |      \a      | Bip sesi verir.                         |
| ASCII Backspace (BS)           |      \b      | İmleçi bir karakter geri alır.          |
| ASCII Formfeed (FF)            |      \f      | Yeni satırda kaldığı yerden devam eder. |
| ASCII Linefeed (LF)            |      \n      | Yeni satırda en baştan devam eder.      |
| ASCII Carriage Return (CR)     |      \r      | Satır başı yapar ve üzerine yazar.      |
| ASCII Horizontal Tab (TAB)     |      \t      | Dikey Tab.                              |
| ASCII Vertical Tab (VT)        |      \v      | Yatay Tab.                              |
| Character with octal value ooo |     \ooo     | Octal karakterler                       |
| Character with hex value hh    |     \xhh     | Hex karakterler                         |

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

### Unicode

Konun iyi anlaşılması için lutfen [burdan](https://baykoch.github.io/blog/genel/unicode/) unicode,utf, ascii gibi kavramlar ne anlama geliyor bir göz atın.

Unicode kunusunda Python 2 ve 3 arasında fark olduğunu belirteyim. Python 2 bahseilmeyecek.

- byte olduğunu belirtmek için tırnaklardan önce `b` harfi kullanılır.

```python
byt = b'\xe2\x82\xba' # utf8 göre kodlanmış bayt gösterimi
print(byt.decode("utf8")) # bayt kodun çözümü: ₺
```

- Kodlama işlemeleri için `encode` ve `decode` foksiyonları kullanılır. 

```python
 print("₺".encode("utf8"))  # b'\xe2\x82\xba'
 print(b'\xe2\x82\xba'.decode("utf8")) # ₺
```

- Kodlama biçimi temsil edilmiyorsa hata verecektir. Ascii olmayan bir karakter kodlamaya çalışalım. `ü` karakteri ascii bulunmaz.

```python
byt = "ü".encode("ascii") #  'ascii' codec can't encode character
```

- Temsil edilmeyen durumları ele almak için `error` parametresi kullanılır. 

| Parametre           | Anlamı                                                       |
| ------------------- | ------------------------------------------------------------ |
| ‘strict’            | Karakter temsil edilemiyorsa hata verilir.                   |
| ‘ignore’            | Temsil edilemeyen karakter görmezden gelinir.                |
| ‘replace’           | Temsil edilemeyen karakterin yerine bir ‘?’ işareti koyulur. |
| ‘xmlcharrefreplace’ | Temsil edilemeyen karakter yerine XML karşılığı koyulur.     |

```python
ignore = "aü".encode("ascii", errors="ignore") # b'a'
replace = "aü".encode("ascii", errors="replace") # b'a?'
xml = "aü".encode("ascii", errors="xmlcharrefreplace") # b'a&#252;'
```

`strict` modu ile varsayılan boş mod aynı anlama gelir.

```mathematica
"aü".encode("ascii", errors="strict") = "aü".encode("ascii")
```

- Dosya okuma yazma işmelerinde unicode yeniden değinilecetir.

UTF-16 ve UTF-32 çevirme.

```python
lira_Utf16 = "₺".encode("utf16") # b'\xff\xfe\xba '
lira_Utf32 = "₺".encode("utf32") # b'\xff\xfe\x00\x00\xba \x00\x00'
    
dec_utf16 = lira_Utf16.decode("utf16") # ₺
dec_utf32 = lira_Utf32.decode("utf16") # ₺
```

Hard kod biçimden UTF-16 için `\u` ve UTF-32 için`\U` kullanılabilir.

```python
lira_Utf16 = "\u20BA"
lira_Utf32 = "\U000020BA"
print(lira_Utf16) # ₺
print(lira_Utf32) # ₺
```

### String Formatting

format str nesneleri için çok yünlü biçilendirme foksioynudur. Biçimlendirme süslü parntezler`{}` arasınada belirtilitr. Süslü parnteler arasında biçimlernirme 3 faklı şeklide varsayılan, sırayı belitme veya anahtar  kelime kullnılarak yapılabilir. 

```python
if __name__ == '__main__':
   
    # varsayılan boş 
    default_order = "{}, {} and {}".format('İncir','Kivi','Muz')
    print(default_order) # İncir, Kivi and Muz

    # Sırayı bildirme
    positional_order = "{1}, {0} and {2}".format('İncir,','Kivi','Muz')
    print(positional_order) # Kivi, İncir, and Muz

    # Anahtar kelime kullanark
    keyword_order = "{s}, {b} and {j}".format(j='İncir',b='Kivi',s='Muz')
    print(keyword_order) # Muz, Kivi and İncir
   
    pass
```



### String Fonksiyon

## Lists

## Dictionaries

## Tuples

## Sets 

### Frozenset




































