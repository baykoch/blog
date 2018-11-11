---
title: "Java Sıra Dışı Durum Yönetimi"
last_modified_at:
categories:
  - java
tags:
  - java exception nedir
  - java error sınıf
  - java AutoCloseable kullanımı
  - java finally bloğu
  - java suppressed nedir
  - java assert kullanım amacı
  - java unchecked exception nedir
toc: true
toc_sticky: true
toc_label: "Java Exception"
author_profile: True
---

Yazılımın normal çalışma halinden sapmasına sıra dışı durum(exception) denir.

Dosya okuma işleminde dosyaya erişim izninin olmaması, site `login` yaparken bilgilerin yanlış girilmesi veya arama yaparken bakiyenin yetersiz olması gibi birçok sıra dışı durumlara örnek verilebilir.

Sıra dışı durumların oluşması problem değildir. Problem oluşan sıra durumlar için seçenekler üretilememesinden kaynaklanır. Bu gibi durumlar bazen insanı sinir krizine sokabilir. Kamu veya özel kuruluşa üye olmak için onlarca soruya cevap verilir fakat sonunda küçük bir hatadan her şeyin boşa gittiğine şahit olursunuz. Günlük hayat buna benzer binlerce olayla karşılaşırız.

Sıra dışı durumların nedenleri bu durumun olabileceğinin farkına varılmaması veya zaman ve imkan yetersizliğinden dolayı sonraya bırakılmasıdır. Yani sonra yaparız:)

> Analistlerin en önemli görevi meydana gelmesi pek olası görülmeyen veya bilinmeyen durumları ortaya çıkarmasıdır.

Sıra dışı durumlar engellenemez. Amaç problem ile karşılaşıldığında devekuşu gibi kafamızı toprağa gömmek yerine yazılımın nasıl devam edeceğini belirlemek olmalıdır.  

Sıra dışı durumlara iki farklı açıdan yaklaşılabilir.

1. Kullanıcıya durumu bildirmek ve onun kararına göre devam etmek.
2. Kullanıcıyı bilgi vermeden veya başvurmadan inisiyatif alarak devam etmek.

Detaya girmeden önce konuyla ilgili terimlere değinelim.

- **Exception**: Sıra dışı durumun nedeni veya kendisi: Kullanıcı adının hatalı girilmesi.

- **Throw**: Çağrıldığı noktaya/metoda fırlatmak/bildirmek.

- **Catch**: Throw ile bildirilen durumu yönetmek için yazılan kod parçası

- **Call Chain/Stack Trace** : Sıra dışı durum oluşan metottan ele alınan noktaya kadar ki çağrı sırası.

Sıradışı durumlar hata(*error*) değildir. Hata sözdizimi, matematiksel veya donanımsal yetersizliği ile oluşan geriye dönüşü olmayan hatalardır. Dosya yazma işlemlerinde, hard diske yeterli alan bulunamaz ise bekleyin yeni harddisk takıyoruz diyemeyiz.

Mantık hataları `bug` kullanıcı hatası ile oluşan hatalardır. Yanlış hesaplanan işlemler, ulaşılmaya çalışılan değişkenin null olması  veya dizinin olmayan hücresine ulaşmaya çalışmak gibi örnekler verilebilir. Mantık hataları `bug` düzeltilmelidir.

Sıra dışı durum olabilecek kod parçasını `try` kısmına, sıra dışı durum sonucunda yapılacak işlemler ise  `catch` kısmına yazılır. An az bir tane `catch` bloğu olması zorunlu olmakla birlikte istenildiği kadar tanımlanabilir.

`throws` ile metot, hatayı çağrıldığı metota fırlatır. Fırlatılan yer hatayı `try-catch` ile ele alabildiği gibi kendisininde çağrıldığı noktaya fırlatabilir. Önemli olan nokta sıra dışı durumun bilgisine sahip olan metotların sıra durumu ele alınmasıdır. Fırlatmak `throws` sıra dışı durum nesnesini çağrıldı bir üst noktaya `rising` geçmektir.

### throws vs throw

Bir metot sıra dışı durumu  ele almaz( try-catch)  ise bir üst çağrılan yere fırlatması gerekir.

- ***throw*** : `Throwable` veya `Throwable` alt sınıflarından  üretilen nesneyi fırlatır.

-  ***throws***:   Metot arayüzüne yazılarak fırlatılan `Throwable` nesnesinin tipini belirtir. Amaç ben bu tip ve tiplerdeki nesneyi fırlatıyorum haberiniz olsun. Fırlatılan nesneyi alan metot ise ya ele alır yada  çağrıldığı bir üst noktaya bildirir.

  ```java
  public class ThrowableDemo {
 
      public static void main(String[] args) {
          ThrowableDemo p = new ThrowableDemo();
          // Sıra dışı durum main ele alındı.
          try {
              p.method1();
          } catch (Throwable e) {
              // Çağrı zinciri göster.
              e.printStackTrace();
          }
      }
      // Sıra dışı durum ele alınmadı.
      // throws ile main metoda Throwable tipi bildirildi.
      private void method1() throws Throwable {
          method2();
      }
      // Sıra dışı durum oluşturuldu, ele alınmadı ve fırlatıldı.
      // throws ile method1'ye Throwable tipi bildirildi.
      private void method2() throws Throwable {
          // Sıra dışı durumun üretildi.
          Throwable th = new Throwable();
          throw th; // Nesne method1'ye fırlatıldı.
          // Aynı satırda nesneyi üretip fırlatma
          // throw new Throwable();
      }
  }
  ```

- Hiçbir yerde fırlatılan nesne ele alınmazsa JVM çalışmayı durdurur. **Yani üretilen bir sıra dışı durum kesinlikle ele alınmalıdır**.

```java
public class ThrowsDemo {
 
    public static void main(String[] args) throws Throwable {
 
        ThrowsDemo p = new ThrowsDemo();
        // Çağrı zincirin son halkası yani main fırlatılan durum ele alınmadığı için JVM
        // çalışmayı dudurur.
        // Metot çağrısından sonra println satırı çalışmaz.
        p.method1();
        System.out.println("Bu satır çalışmaz.");
 
    }
    private void method1() throws Throwable {
        method2();
    }
    private void method2() throws Throwable {
        Throwable th = new Throwable("Şaka yaptım.");
        throw th; // Nesne method1 fırlttıldı
    }
}
```

### Sıra Durum Hiyerarşi (Java SE 11)

{% include figure image_path="/assets/images/java-exception.png" alt="Integer" caption="Javanın hata ve sıra dışı durumlarla ilgili sınıflar"%}

## Throwable Sınıfı

Java'da sıra dışı durum ve hatalar `Throwable` sınıfın ile temsil edilir. Dikkat arayüz değildir(-able ekleri genellikle arayüz isimlerinde kullanılır bu prograyıcıyı yanıltmasın!) Fırlatılan `throws` her şey `Throwable` veya `Throwable` alt sınıflarından biri olmak zorundadır.

**`Throwable` Sınıfının Kurucuları ve İşlevi:**

| Erişim B. | Kurucular                                                    | Tanım                                                        |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
|           | Throwable()                                                  | Sıra dışı durum hakkında bilgi vermeden throwable nesnesi üretme. |
|           | Throwable(String message)                                    | Sıra dışı durum hakkında bilgi vererek throwable nesnesi üretme. |
|           | Throwable(String message,          Throwable cause)          | Sıra dışı durum hakkında bilgi bilgi ve  throwable nesnesi geçerek(cause) nesne üretme. |
| protected | Throwable(String message,          Throwable cause, boolean                                         enableSuppression, boolean writableStackTrace) | Hakkında bilgi, nedeni, baskılamanış/es geçilmiş/göz ardı edilmiş sıra durum  yöntern metodu aktif etme ve sıra dışı durum oluştuğu sırayı gösteren metotları üzerinde değişiklik yetkisini bloklama |
|           | Throwable(Throwable cause)                                   | Throwable nesneini (Sıra dışı durum hakkında bilgiye sahip nesne) geçerek nesne üretme. |

Şimdi Throwable davranışlarının bazıları göz atalım.

**String getMessage() :** Fırlatılan sıra dışı durum hakkında bilgi verir.

**StackTraceElement[] getStackTrace():** Yığındaki buluna metotlar hakkında son çağrılandan başlayarak `try -catch` ile ele alınan metoda kadar bilgi verir.

- `StackTraceElement` yağında bulunan metotlar hakkında bilgilere sahiptir.
  -  *getFileName():* Sınıfın dosya ismi
  -  *getClassName()*: Sınıfın açık adresi (bulunduğu paket)
  -  *getMethodName():* Çağrı zincirinde yer aldığı metot
  -  *getLineNumber():* Çağrı zincirinde  yer aldığı satır.

 **void printStackTrace():** Sıra dışı dırım mesajı ve yığında oluşan metot çağrılarını kırmızı renkte sondan başa doğru  gösterir.

```java
package baykoch.exception;

public class ThrowableDemo {

    public static void main(String[] args) {
        ThrowableDemo p = new ThrowableDemo();

        try {
            p.method1(); // Çağrı zinicin ilk metot çağrısı
        } catch (Throwable e) {
            // Yığındaki fonksiyonları/metotları hakkında en sondan başlayarak bilgi verme.
            StackTraceElement[] methodList = e.getStackTrace();
            for (StackTraceElement s : methodList) {
                System.out.print("Sınıf İsmi : "+s.getFileName() ); // Sınıfın dosya ismi
                System.out.print(" Paket Adresi : "+s.getClassName()); // Sınıf açık adresi (bulunduğu paket)
                System.out.print(" Metot İsmi : "+s.getMethodName()); // Yer aldığı metot
                System.out.print(" Satır :"+s.getLineNumber()+ "\n"); // Yer aldığı satır.               
            }
            System.out.println(e.getMessage()+ "\n"); // Sadece sıra durum bilgi mesajını gösterme
            // Kırmızı renkte sıra dışı durumun fırlatıldığı çağrı zinciri gösterir.
            e.printStackTrace();
        }
    }
    private void method1() throws Throwable {
        // Çağrı zincirinde 2.metodun çağrısı    
        method2();
    }
    private void method2() throws Throwable {
        // Çağrı zincirinde 3.metodun çağrısı
        method3();
    }
    private void method3() throws Throwable {
        // Sıra dışı durumun üretildiği ve fırlatıldığı ilk yer.
        Throwable th = new Throwable("Method3'te bir şey oldu!"); // getMessage() bilgisi girldi.        
        throw th;// Nesne fırlatılıyor.
    }
}
```

- > Sınıf İsmi : ThrowableDemo.javaPaket Adresi : baykoch.exception.ThrowableDemoMetot İsmi : method3Satır :34 <br>
  > Sınıf İsmi : ThrowableDemo.javaPaket Adresi : baykoch.exception.ThrowableDemoMetot İsmi : method2Satır :30<br>
  > Sınıf İsmi : ThrowableDemo.javaPaket Adresi : baykoch.exception.ThrowableDemoMetot İsmi : method1Satır :26<br>
  > Sınıf İsmi : ThrowableDemo.javaPaket Adresi : baykoch.exception.ThrowableDemoMetot İsmi : mainSatır :9<br>
  > Method3'te bir şey oldu!
  >
  > java.lang.Throwable: Method3'te bir şey oldu!
  > ​    at baykoch.exception.ThrowableDemo.method3(ThrowableDemo.java:34)
  > ​    at baykoch.exception.ThrowableDemo.method2(ThrowableDemo.java:30)
  > ​    at baykoch.exception.ThrowableDemo.method1(ThrowableDemo.java:26)
  > ​    at baykoch.exception.ThrowableDemo.main(ThrowableDemo.java:9)

 **void addSuppressed(Throwable exception):** Javada 1.7 önceki sürümlerinde eğer metot birden fazla throwable nesnesi fırlatıyorsa (in try-with-resources) biri hariç diğerleri yakalanamıyordu. `addSuppressed` metoduna göz ardı edilen sıra dışı durumlar eklenerek yönetilebilir. Dersin ileri kısımlarında değinilecek.

**Throwable[]     getSuppressed():** Göz ardı edilen/baskılanan sıra dışı durumları isteme. Dersin ileri ksımlarında değinilecek.

### Error Sınıf

JVM tarafından yakalanan ve kullanıcı tarafından ele alınamayan(try-catch) hatalardır. Bu hatalar sistemsel veya JVM yapısıyla ilgili hatalardır. Java SE 11 süründe 13 tanedir. Mesela `VirtualMachineError` Java Virtual Machine kırılması veya yeterli alan olmaması sonucunda oluşur.

- **Kullanıcıyı pek alakadar etmediğin detaya girmenin bir anlamı yok.**

## Exception Sınıfı

Ele alınabilen her türlü sıra dışı durumu ifade eder. Java SE 11 sürümünde `Exception` sınıfın  tanımlı olan yaklaşık 160 tane alt sıradışı durum sınıfı vardır. Kullanıcı tarafından `Exception` sınıfı devralınarak yeni sıra dışı durumlar tanımlanabilir. `Throwable` sahip olduğu kurucu ve davranışlara sahiptir. Onun için tekrar yazmaya gerek görmüyorum. Javanın paketlerinde `Exception` sınıftan türetilen ilgili sınıflar ilgili birçok `exception` bulunur.

Dizinin olamayan hücresine ulaşmaya çalışalım.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
            
        int a[] = { 12, 14, 21 };
        // Dizinin olmayan hücresi ulaşmak
        System.out.println("Dizin 4 elemanı :" + a[3]); // Hata!
        System.out.println("Güle güle..."); // Hatadan sonraki satırlar çalışmayacaktır.
    }
}
```

> Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3 at baykoch.exception.ExceptionDemo.main(ExceptionDemo.java:9)

Şimdi sıra dışı durum tolere edelim.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        
        try {
            int a[] = { 12, 14, 21 };
            System.out.println("Dizin 4 elemanı :" + a[3]);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Dizinin olmayan hücresine ulaşmaya çalıştırınız.");
        }
        System.out.println("Güle güle...");
    }
}
```

> Dizinin olmayan hücresine ulaşmaya çalıştığınız.<br>
> Güle güle...

### try-catch

- Sıra dışı durum fırlatılan kod kısmı `try` kısmına sıra dışı durumu ele alan kod kısmı `catch` kısmına yazılır.
- `try` bloğunda sonra sadece bir `catch` bloğu çalışır.

- Birden fazla sıra dışı durumu ele alınması durumunda birden fazla `catch` bloğu peşpeşe -araya kod bloğu girmeksizin-  kullanılır.

- Birden fazla sıra dışı durum fırlatılıyorsa **ölü kod** oluşmaması için **alt sınıflardan üst sınıflara doğru** sıralama yapılmalıdır. [Sebebi mirasa konu olan sınıfların yerine geçme özeliğinin bulunmasıdır.](https://baykoch.github.io/blog/java/java-polymorphism/) Ayrıca aynı sıra dışı durum bir `try-catch` bloğunda iki kere yazılamaz.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        
        try {
            int a[] = { 12, 14, 21 };
            
            int r = a[3] / 0;
        // Catch blokları alt sınıflardan üst sınıflara doğru sıralanmalıdır.    
        } catch (RuntimeException e) {
            System.out.println("Dizinin olayan hücresine ulaşmaya çalıştınız.");
        }
        //  Bir sıra dışı durum bir try-catch bloğunda iki kere yazılamaz.
        catch (RuntimeException e) {
            System.out.println("Dizinin olmayan hücresine ulaşmaya çalıştırınız.");
        }
        // Ulaşılamayan kod parçası
        catch (ArithmeticException e) {
            System.out.println("Bir sayıyı 0 bolmeye çalıştınız.");
        }    
        System.out.println("Güle güle...");
    }
}
```

- Metotlar `exception` ele almayıp bir üst noktaya fırlatabilir. Birden fazla `exception` fırlatılabilir. Bu durumda metot arayüzünde belirtilmelidir.

```java
public class ExceptionDemo {
    
    static int a[] = { 12, 14, 0 };
    
    public static void main(String args[]) {
        
        double r;
        try {
            r = divide();
        } catch (ArithmeticException e) {
            System.out.println("Bir sayıyı 0 bolmeye çalıştınız.");
        }
        catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("Dizinin olmayan hücresine ulaşmaya çalıştırınız.");
        }
    }
    // Birden fazla sıra dışı durumun fırlatılması
    private static double divide() throws ArrayIndexOutOfBoundsException, ArithmeticException {
        
        return a[0] / a[2];
    }

}
```

- **Fırlatılan exception daha spesifik (alt-sınıf) olması anlamlıdır**. Çünkü eğer bir metot hem  `NullPointerException` hemde `ArithmeticException` fırlatabilir duruma sahipse ve bu sıra dışı durumların ebeveyn sınıfı olan `Exception` yakanılyorsa olası bir hata durumunda hangisini oluştuğunu anlamak meşakkatli olacaktır.
- Üst sınıflardan alt sınıflara doğru yerine geçebilme özelliğine olmamasından dolayı fırlatılamaz.

- Metot arayüzünde belirtilen throws exception nesneleri metot imzasına dahil değildir. Yani aynı imzaya sahip fakat farklı exception sahip iki metot tanımlanamaz.

```java
public class ExceptionDemo {
    
    public static void main(String args[]) {
            // ....
    }

    private static double divide() throws ArrayIndexOutOfBoundsException, ArithmeticException {
       // ...
    }
    // Hata! throws belirtilen exception metot arayüzüne dahil değildir.
    // Bu yüzden farklı sıradışı durumlara sahip aynı imazlı iki metot tanımlanamaz.
    private static double divide() throws NullPointerException, ArithmeticException {
       // ...
    }
}
```

- Tek catch bloğunda birden fazla sıra dışı durum kullanılabilir. Bunun için sıra dışı durumlar arasına `|`  karakteri koyulur. Eğer aynı catch bloğuna konulan miras ilişkisi (üst-alt sınıf) varsa yerine geçebilme özelliğine bulunmasından dolayı hata verecektır. Hangi sıra dışı durumun oluştuğunu anlamak güç olacağından **tavsiye edilmez**.

  ```java
  public class ExceptionDemo {
 
      public static void main(String args[]) {
          double r;
          int a[] = { 12, 14, 0 };
 
          try {
              r = ExceptionDemo.divide(a[1], a[2]);
              // Tek catch bloğunda birden fazla exception kullanılabilir.
          } catch (NullPointerException | ArithmeticException e) {
              System.out.println(e.getMessage());
 
              // Hata! Araların üst-alt sınıf ilişkisi olmamalıdır.
          } catch (RuntimeException | Exception e) {
              System.out.println(e.getMessage());
          }
      }
      private static double divide(int x, int y) {
          return x / y;
      }
  }
  ```



## try-with-resources

Streams, connection gibi kaynaklar kullanıldığında bağlantıların kapatılması gereklidir. Örneğin açılan bir text dosyası işlemler bittikten sonra kapatılarak yeniden kullanılabilir hale getirilir. Fakat try bloğunda içinde kaynak kullanılıyorsa  karşılaşılan bir hata sonucu asla kapanmayabilir. Java bu gibi durumları ele almak iki farklı yol sunar.

1. **Finally**
2. **AutoCloseable**

### Finally

​    Kullanımı zorunlu olmamakla birlikte, kullanıldığında bir kere çalıştırılacağı garanti edilen bloktur.

- **Catch**’den sonra gelmek zorundadır.
- Sıra dışı durum meydana gelip gelmesin bir kere kesin çalışır.
- Sadece bir tane **Finally** bloğu tanımlanabilir.
- **Catch** bloğu ile **Finally** bloğu arasında başka kod bloğu giremez.
- **AutoCloseable** arayüzünü yerine getirmeyen(**not** *implements*) kaynaklar için tercih edilir.
- **Finally** yapılan her türlü işlerin temizlik yeridir.
- **Finally** temizlik yeri olduğu için  içinde `return` `throw` gibi geri dönüş değeri döndören ifadeler bulunmamalıdır.
- Sıra dışı durum olmasa bile [dallanma ifadeleri](https://baykoch.github.io/blog/java/java-control-flow-statements/) yüzünden çalışmayan kod parçaları **finally** bloğu da çalışması sağlanır.
- **Finally** bloğunda sıra dışı durum olabileceğinden `try-catch-finally` kullanılabilir.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        BufferedReader rd = null;
        // Text dosyadan veri okuma
        try {
            rd = new BufferedReader(new FileReader("file"));
            String inputLine = null;
            while ((inputLine = rd.readLine()) != null)
                System.out.println(inputLine);
            
        } catch (IOException ex) {
            ex.printStackTrace();
        } finally {
            // finally  içinde duruma göre tekrar try-catch kullanılabilir.
            // Dosya eğer null değilse kapatılacaktır.
            if (rd != null) {
                try {
                    rd.close();
                } catch (IOException ex) {
                    ex.printStackTrace();
                }
            }
        }
    }

}
```

### AutoCloseable

Bir kaynak eğer `AutoCloseable` arayüzünü yerine getiriyorsa veya miras alıyorsa `AutoCloseable` üzerindeki close() metodu ezilerek kaynaklar kapatılabilir.  try anahtar kelimesinden sonra () parantez içinde kaynak belirtilir. `AutoCloseable` yöntemi `finally` bloğuna göre daha derli toplu yapı sağlar.

> FileReader sınıf AutoCloseable arayüzünü yerine getirdiği(implements) etiği için close() metodu sahiptir. Örnekle gösterelim.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        // Try dan sonra parantez içinde kaynak belirtilir.
        try (BufferedReader rd = new BufferedReader(new FileReader("/home/baykoch/file"));) {

            String inputLine = null;

            while ((inputLine = rd.readLine()) != null)
                System.out.println(inputLine);

        } catch (IOException ex) {
            ex.printStackTrace();

        }
    }

}
```

- `AutoCloseable` yerine getiren veya miras alan sınıf çağrıldığından bir kez `AutoCloseable` üzerindeki **close()** bir kez kesinlikle çalışır.

- Yazılımcılar kaynak sınıflarını `AutoCloseable` yerine getirerek(*implements*) kendisi oluşturabilir.
```java
public class ExceptionDemo {

    public static void main(String args[]) {

        try (AutoClose rd = new AutoClose()) {
            // r = 2/0 hatası meydana gelse bile close() metodu çalışacaktır.    
            int r = 2 / 0;
        } catch (ArithmeticException ex) {
            ex.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}

class AutoClose implements AutoCloseable {
    // close() her halükarda çalışacaktır.
    @Override
    public void close() throws Exception {
        System.out.println("Kaynak kapatıldı.");
    }
}        
```

- Eğer `Try` içinde birden fazla  kaynaklar kullanılmış ise son yazılandan başa doğru çalışır. Eğer kaynaklar birbirine bağlı ise yazım sırasına dikkat etmek gerekebilir.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        // Try içine birden fazla kaynak yazılabilir.
        // Kaynaklar yazım sırasına göre sondan başa doğru çalıştırılır.
        try (AutoClose p = new AutoClose(); AutoClose2 k2 = new AutoClose2()) {
            int r = 2 / 0;
        } catch (ArithmeticException ex) {
            ex.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class AutoClose implements AutoCloseable {
    // try içinde ilk yazıldığından son çalışacaktır.
    @Override
    public void close() throws Exception {
        System.out.println("1.kaynak kapatıldı.");
    }

}
class AutoClose2 implements AutoCloseable {
    // try içinde sona yazıldığından ilk çalışacaktır.
    @Override
    public void close() throws Exception {
        System.out.println("2.kaynak kapatıldı.");
    }
}
```

### AutoCloseable vs Finally

Bir kaynak  **AutoCloseable** arayüzünü yerine getiriyor(*implements*) veya devralıyorsa(*extends*) kesinlikle **AutoCloseable** yöntemi tercih edilmelidir. Diğer kaynaklar için **Finally** tercih edilebilir.

### Suppressed

Javada 1.7 önceki sürümlerinde eğer metot birden fazla throwable nesnesi fırlatıyorsa (**in try-with-resources**) biri hariç diğerleri yakalanamıyordu. Peki bir metot birden fazla exception fırlatabilir mi? Evet `try-with-resources` içinde birden fazla `exception` fırlatılabilir.

```java
public class SuppressedDemo {
    public static void main(String[] args) throws Exception {
        try {
            call();
        } catch (Exception e) {
            e.printStackTrace(); // Sadece ikinci exception yakanaldı.
        }
    }
    private static void call() throws Exception {
        try {
            // Kaybolan exception
            throw new FirstException("Birinci fırlatılan sıra dışı durum.");    
        } finally {
            throw new SecondException("İkinci fırlatılan sıra dışı durum.");
        }
    }
}
class FirstException extends Exception {
    public FirstException(String message) {
        super(message);
    }
}
class SecondException extends Exception {
    public SecondException(String message) {
        super(message);
    }
}
```

**Normalde finally blokların içinde `return` `throw` gibi geri dönüş değeri döndören değerler olması doğru değildir.**

Yukarı kodda görüldüğü üzere `FirstException` kaybolmuştur. Şimdi `addsuppressed` metot kullanarak fırlatılan her `exception` yakalayalım.

```java
public class SuppressedDemo {
    public static void main(String[] args) throws Exception {
        try {
            call();
        } catch (Exception e) {
             e.printStackTrace(); // İkinci exception.
            // Birinci exception
            for(Throwable t: e.getSuppressed()) {
                t.printStackTrace();
            }
        }
    }
    private static void call() throws Exception {
        Throwable t = null;
        try {
            // Kaybolan exception
            throw new FirstException("Birinci fırlatılan sıra dışı durum.");    
        } catch (Exception e) {
            t = e; //Kaybolan  Exception yakalanıyor.
        }finally {
            SecondException secondEx = new SecondException("İkinci fırlatılan sıra dışı durum.");    
            if (t!=null) {
                // Kaybolan exception sonra kurtarmak için addSuppressed geçiyoruz.
                secondEx.addSuppressed(t);
            }
            throw secondEx;
        }
    }
}
class FirstException extends Exception {
    public FistException(String message) {
        super(message);
    }
}
class SecondException extends Exception {
    public SecondException(String message) {
        super(message);
    }
}
```

### Rethrow Exception

Bazı durumlarda yakalanan sıra dışı durum yeniden fırlatılabilir.

1. Yakalanan yer ele alınacağı (*handle*) yer olmamakla birlikte sadece bilgi amaçlı `log` yapmak yakalanmıştır.

```java
// login() metodu sadece loglama yapmak için sıra dışı durumu yakalıyor.
private void login() throws UserNotFoundException {
        
        try  {
            // To-do smt
        } catch (UserNotFoundException ex) {
            //Logging
            Logger.log(ex);
            // Sıra dışı durumun yeniden fırlatılması
            throw ex;
        }
}
```

2.  Yakalanan sıra dışı durumun daha öznel/spesifik hali yeniden fırlatılabilir. Fırlatılırken bir önceki/genel genel sıra dışı durum içine konulabilir.

   Şimdi bir örnekler açıklayalım. Veritaban aranan bir ürün bulanmadığında `SQLExcetion` firlatılır. Daha spesifik sıra dışı durum `NoProductFound` fırlatılıyor.

   Genel sıra dışı durum `SQLExcetion` gibi içinde birçok hata kod bilgisi barındırabilir. Bu bilgileri ele alınacak yere aktarmak istenebilir. Fazla bilgiyi aktarmak istiyorsak `initCause` metodu eski/genel sıra dışı durum geçilir. Daha sonra [getCause()](file:///home/baykoch/Documents/docs/api/java.base/java/lang/Throwable.html#getCause()) metodu ile genel sıra dışı durum geri alınır.

   ```java
   private void search() throws SQLException {
           
           try  {
               // To-do smt
           } catch (SQLException ex) {
               Logger.log(ex);
               Exception newEx = new NoProductFound(); // Spesifik sıra dışı durum.
               newEx.initCouse(ex); // Eski sıra dışı durumun aktarılması
               throw newEx;
           }
   }
   ```

### Unchecked vs Checked

   Yukarıdaki **Throwable** sınıf hiyerarşisini gösteren resme bakılırsa **Error** ve **RuntimeException** sınıflarını kırmızı ile işaretlendiği görülebilir. Bu sınıflar Unchecked yanı kontrol edilemeyen dışı durumlardır. Çünkü error sınıf JVM den veya sistemsel hatalardan olduğunu kontrol edilemeyeceğinden bahsetmiştik. Benzer şekilde **RuntimeException** sınıfı ise programcı tarafından yapılan hatalar olup kontrol edilmesine yani throws fırlatılmasına gerek yoktur.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        double r;
        r = ExceptionDemo.divide(1, 0);
    }
    // RuntimeException fırlatılmasına gerek  yoktur.
    private static double divide(int x, int y) {
        return x / y;
    }
}
```

   Zaten fırlatma gibi durum olsaydı -örnek olarak `NullPointerException`- hatayı her yere yazmak zorunda kalırdık ki buda pek uygulanabilir değildir. Ama biz dersin anlaşılması yardımcı olması için `ArithmeticException`, `NullPointerException` gibi sıra dışı durumları fıllattık.

- Programcı hiçbir zaman bir sayının sıfıra bölünmesine veya bir metodun asla `null` döndürmesine izin vermelidir.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        double r;
        r = ExceptionDemo.divide(1, 0);

    }
    private static double divide(int x, int y) {
        double r = 0;
        // Kullanıcı sıfıra bölmek gibi hataları kendisi tolere etmelidir.
        if (y == 0) {
            System.out.println("Sayı 0'ra bölünemez.");
        } else {
            r = x / y;
        }
        return r;
    }
}
```

   Bazen hatta çoğu zaman tasarımsal problemler olur veya şartlar değişir yada öyle gerekiyordur metot null döndürmek zorundadır. Bu durumda bilgilendirme amaçlı **Api dokümantasyonu** metodun `null` dönderebilkeçeği belitrilmedlir. Metot kullanan yazılımcı metottan gelen değerin null olup olmadığı kontrol eder. Aksi halde [Polymorphism](https://baykoch.github.io/blog/java/java-polymorphism/) prensibine göre metot içinde ne olduğunu bilinmediğinden `null`  dönderebileçeğinden kimsenin haberi olmaz. Buda  ölümcül hatalara neden olur.

`Checked` düzeltilebilecek durumları ifade eder. Dosya bulunamadı, kullanıcı şifreyi hatalı girdi, bakiyesi yetersiz ne yapalım? `Checked` sıra dışı durumlar tasarıma göre aksiyon alınmalı ve düzeltilmelidir.

### Sıra Dışı Sınıf Oluşturmak

Java’nın sunduğu sıra dışı durumlar yetersiz kaldığı durumda Exception sınıfını devralarak kendi sıra dışı durumu oluşturabilirz.

Bilgi taşıyan sınıflar için ihtiyaca göre `get/set` metotları yazılır. Tipik olarak kurucusu `String` bilgilendirme mesajı alır.

```java
public class ExceptionDemo {

    public static void main(String args[]) {
        ExceptionDemo bs = new ExceptionDemo();
        try {
            bs.findBook("");
            // To-do smt...
        } catch (İsimBulunamadıException e) {
            e.printStackTrace();
        }
    }
    private void findBook(String name) throws İsimBulunamadıException {

        if (name.equals("")) {
            throw new İsimBulunamadıException("İsim boş geçilemez.");
        }
        // To-do smt...
    }
}
// Özel sıra dışı durum oluşturma
class İsimBulunamadıException extends Exception {

    public NameNotFoundException(String message) {
        super(message);
    }
}
```

### Ezilmiş Metotlarda Sıra Dışı Durum

Ezilen metot eğer sıra dışı durum fırlatıyorsa bu durumda **aynısını** bir daha **spesifik alt sınıf**  fırlata bildiği gibi **hiçbir** sıra dışı durum fırlatmaya bilir. Fakat **üst sıra dışı durumu (ebeveyn) asla fırlatamaz**.

```java
public class ExceptionDemo extends DivideOps {
    /*
    // Hata! Ezdiği metottan daha genel üst sıra dışı durumu (ebeveyn) asla fırlatamaz.
    @Override
    protected double divide(int x, int y) throws Exception {
        return super.divide(x, y);
    }
       // Ezdiği metottan daha spesifik alt sınıf  fırlata  bilir.
    @Override
    protected double divide(int x, int y) throws ArithmeticException {
        return super.divide(x, y);
    }
    */
    // Ezdiği metottan sıra dışı ele alıp hiçbir durum(exception) fırlatmaya bilir.
    @Override
    protected double divide(int x, int y) {
        double r;
        if (y == 0) {
            r = x;
        } else {
            r = super.divide(x, y);
        }
        return r;
    }
}
class DivideOps {
    protected double divide(int x, int y) throws RuntimeException {
        return x / y;
    }
}
```

### Assertion

- `Assert` ile test edilen ifadenin her zaman doğru olması umulan aski halde çalışmayı durduran yapıdır.

- Bu yapı daha çok uygulama geliştirirken vaad edilen şartların doğruluğunu test etmek için kullanılır.

- Maliyeti fazladır. Yazılım dağıtım sürümününde(son halinde) kullanılmaz.

- `assert` yapısın iki hali vardır.
  1. Sadece ifadeyi kontrol eden yapı.
  2. İfadeyi kontrol ederken bilgi mesajı gecen yapı.

```java
public class AssertDemo {

    public static void main(String args[]) {
        int i = 2;
        // ilk şekli sadece ifadeyi kontrol eden yapı
        assert i > 1;
        // ikinci şekli ifadeyi kontrol ederken bilgi mesajı gecen yapı.
        assert i > 4 : "i 2'den kesinlikle büyük olmalı.";

    }
}
```

Basit senaryo assert neden ve nasıl kullanıldığını açıklamaya çalışalım.

> Şirketimizin X bir bölümünden gönderilen verileri için alan hesaplayan bölüm kodlanacak. X bölümü eksi sayılardan oluşan hatalı veri gönderebilir. Eksi sayıların kontrol etme sorumluluğu X bölüme aittir. Karşı taraf kontrol etmesi gereken durumları kontrol etmemiş yani hatalı proglama yapmıştır. Bunun sonucunda hatalı veri gönderilmiştir. Bize vaad edilen durumun(verilerin eksi sayı olması) hatalı olabileceğini düşünerek alan hesabı yapmadan önce assert ile kontrol etmeliyiz. Bununla birlikte X bölümünü hatayı düzeltmesi için bilgilendirmeliyiz. X bölümü hatayı düzelttikten sonra artık yazılımın son sürümünde asset silebiliriz.

- Kısace `assert` kodun doğru çalıştığını emin olmak amacıyla kullanılır. Emin olduktan sonra `assert` koddan kaldırılmalıdır. Bu prensibe `defensive programming` denir.

- ***Başkasının hatalı olabileceğini düşünerek hareket et.***

### Son Olarak

- Kendi sıra dışı durumlar oluşturarak yazılımınıza entegre edin.

- Sıra dışı durumları tasarlarken sınırı aşmayın. Yani yazılında seçenek olabilecek yapıları sıra dışı durum diye kurgulamayın. Mesela mağaza uygulamasında ödeme seçenekleri (kredi havale vb.) durumlar sıra dışı durum değil, seçenektir. Eğer kredi kartında yeterli bakiye bulunmuyor ise sıra dışı durumdur.

- Sıra dışı durumlar özel olun, genel `Exception,Throwable` fırlatmayın.

- Sıra dışı durumlara **gerekli bilgileri içerecek şekilde kurgulayın** ve fırlatılırken de bilgileri **boş geçmeyin**. Ayrıca bu bilgileri **loglayın**.

- Api dokümantasyonu sıra dışı durum bilgisini girin(`Örnek içeren ders linki eklenecek`).

- Kaynakaları **her zaman** kapatın. `Autocloseable` yapısını `finally` yapısına tercih edin.

