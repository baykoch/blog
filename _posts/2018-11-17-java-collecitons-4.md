---
title: "Java Torba Yapıları 4.Properties Yapısı ve Özet Tablo"
last_modified_at:
categories:
  - java
tags:
  - java Properties Sınıf
  - java hard code kaçınma
  - java arayüz metinleri
toc: false
toc_sticky: true
toc_label: "Java Properties"
author_profile: True
---

**Properties** Türkce kelime anlamı özellikler olarak çevrilir.  Javada genellikle get/set metodları olan private değişkenlere properties denilir. Properties kullanıcı ayarlarını konfigüre edilmesine yardımcı olmak için oluşturulmuş veri yapısıdır.

- Hashtable sınıfını miras alır. String anahtar değer çiftlerinden oluşur.

**Yazılımda (hard code) kodun içine gömülmesi veya veri tabanında saklanması uygun olmayan sadece basit bir metin dosyasında tutulabilen; **

- *yazılımın arayüzü dil metinleri*

- *zamanla değişebilecek teknik sabitler(KDV,ÖTV ...)*

- *ayar konfigüre bilgileri(veri tabanı ...)*

**gibi verilerin yönetilmesinde kullanılır.**

- *Hard Code*: Verileri doğrudan programın içine gömme

**Properties** `HashTable` yapısına ek olarak verileri  dosyaya kaydetme ve dosyadan geri yükleme kabiliyetine sahiptir.

| Constructor                     | Description                                                 |
| ------------------------------- | ----------------------------------------------------------- |
| Properties()                    | Boş Properties oluşturma.                                  |
| Properties(int initialCapacity) | Başlangıç kapasitesi belirtilerek boş Properties oluşturma. |
| Properties(Properties defaults) | \***Varsayılan Properties** girilerek Properties oluşturma. |

- *\***Varsayılan Properties (Properties defaults):*** Eğer aranan değer properties’de bulunmuyorsa default değerler bakılır. Örnek vermek gerekirse ağ işlemleri yürüten bir yazılım eğer bağlantı yapılacak ip değeri eklemeyi unutulmuşsa default değerlerde arama yapacaktır.

  - Properties dosyası yazılırken defaults değerleri yazılmaz.

  ```java
  public class PropertiesDemo {
 
      public static void main(String args[]) {
          // Varsayılan properties nesnesi üret
          Properties defaultConfig = new Properties();
          defaultConfig.setProperty("ip", "192.168.1.1");
          
          // Varsayılan Properties nesnesi geçilerek yeni config nesnesi üret
          Properties config = new Properties(defaultConfig);
          
          // Yeni değerler ekle
          config.setProperty("user", "root");
          config.setProperty("password", "12345");   
          
          // Varsayılan değerler gösterilmez.
          config.list(System.out); // password=12345 user=root
         
          // ip con bulunamadığından varsayılan değerlerde arama yapacaktır.
          String connectionIP = config.getProperty("ip"); // 192.168.1.1
      }
  }    
  ```

Proterties metin veya Xml dosyaları hard code olarak statik olarak belitirlerek veya getClass() ile dosyanın yolu elde edilebilir.

Properties dosyaları diğer kod dosyaları(*class,interface*) ile karışmasın diye resources paketlerinin altına konur.

Properties dosyaları byte-byte(InputStream,OutputStream)  veya karakter-karakter(Reader,Writer) okuma yazma yapılabilir.

Properties iki farklı formatta dosya yazılır.

1. ***Normal Format:*** Key=Value Örnek: `user=root`
2. ***XML Format:*** Örnek: `<entry key="user">root</entry>`

| Modifier and Type | Method                                                       | Description                                                  |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| void              | store(OutputStream out,      String comments)                | OutputStream kullanarak normal formatta kaydetme.            |
| void              | store(Writer writer,      String comments)                   | Writes kullanarak  normal formatta kaydetme.                 |
| void              | storeToXML(OutputStream os,           String comment)        | OutputStream kullanarak XML formatta  kaydetme.              |
| void              | storeToXML(OutputStream os,           String comment,           String encoding) | OutputStream kullanarak XML formatta  kaydetme.***\*encoding*** |
| void              | storeToXML(OutputStream os, String comment,           Charset charset) | OutputStream kullanarak XML formatta  kaydetme. ***\*\*charset*** |

- ***\*\*charset***: Hangi karakterler dizisi kullanılır.
- ***\*encoding***: Karakterler bellekte nasıl ve hangi yöntemle tutulur. (UTF-8,unicode -16 ...)

```java
public class PropertiesDemo {

    public static void main(String args[]) {
        // Boş properties nesnesi oluştur.
        Properties config = new Properties();
    
        // Anahtar-değer çiftleri ekleme
        config.setProperty("user", "root");
        config.setProperty("password", "12345");
        
        // Byte-Byte dosyaya yazdırma
        try(OutputStream output = new FileOutputStream("config.properties");) {

            config.store(System.out, "Config Value"); // Konsola yazdır.
            config.storeToXML(output, "XML Format");  // XML formata dosyaya yazdır.
            //con.store(output, "Normal Format");  // Normal formata dosyaya yazdı
            
        } catch (IOException io) {
            io.printStackTrace();
        }
        
    }
}
```

Properties dosyasında veri okuma ilgilendiren metrolara göz atalım.


| Modifier and Type | Method                      | Description                                     |
| ----------------- | --------------------------- | ----------------------------------------------- |
| void              | load(InputStream inStream)  | InputStream ile normal formattaki dosyayı  oku. |
| void              | load(Reader reader)         | Reader ile normal formattaki dosyayı oku.       |
| void              | loadFromXML(InputStream in) | InputStream ile XML formattaki dosyayı  oku.    |

Yukarıda `stream` yapıları ile yazma gerçekleştirdik. Bu örneğimizde ise Reader ile dosya okuyalım. Dosya içeriği:

>password=12345 <br>
>user=root

```java
public class PropertiesReadDemo {

    public static void main(String[] args) {
        Properties config = new Properties();
        // Reader ile normal formattaki dosyayı okuma.
        try(Reader f= new FileReader("config.properties");) {
            config.load(f);
            
        } catch (IOException e) {
            e.printStackTrace();
        }
        // "user" anahtarı ile eşleşen değeri getir.
        System.out.println(config.getProperty("user")); // root
        
        // Alınan değerleri Iterator yardımı yazdırma.
        Set  keys= config.entrySet();
        Iterator i = keys.iterator();    
        while (i.hasNext()) {
            System.out.println(i.next());    
        }
        // list metodu kullanılarak konsola yazdırma.
        config.list(System.out);    
    }
}
```

- XML formattaki dosyadan Reader ile veri hatalı okunur. Yani loadFromXML sadece InputStream destekler.

### Summary Collection Table

|               | Accept null | Duplicate Support | Primitive  Support | Sorted | Ordered | add/put  | get/next    | contain/search |
| ------------- | ----------- | ----------------- | ------------------ | ------ | ------- | -------- | ----------- | -------------- |
| HashSet       | Yes         | No                | No                 | No     | No      | O(1)     | O(h/n)      | O(1)           |
| TreeSet       | Yes         | No                | No                 | Yes    | Sorted  | O(log n) | O(log n)    | O(log n)       |
| ArrayList     | Yes         | Yes               | No                 | No     | Yes     | O(1)     | O(1)/O(1)   | O(n)           |
| LinkedList    | Yes         | Yes               | No                 | No     | Yes     | O(1)     | O(n)/O(1)   | O(n)           |
| HashMap       | Yes         | No                | No                 | No     | No      | O(n)     | O(1)/O(h/n) | O(1)           |
| LinkedHashMap | Yes         | No                | No                 | No     | Yes     | O(n)     | O(1)        | O(1)           |
| TreeMap       | Only value  | No                | No                 | Yes    | Sorted  | O(log n) | O(log n)    | O(log n)       |



