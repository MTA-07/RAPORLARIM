# Bellek ve Performans Derinliği

**Kazanım:** Bu konuyu kavradığında; kodunun neden yavaş çalıştığını, uygulamanın neden cihazı ısıttığını veya durduk yere çöktüğünü anlayabilir ve belleği şişirmeyen, yüksek performanslı uygulamalar geliştirebilirsin.

Bir program çalıştığında verilere ulaşmak ve onları saklamak için bilgisayarın RAM'ini (Rastgele Erişimli Bellek) kullanır. Bu bellek yönetimi temelde **Stack** ve **Heap** olmak üzere iki farklı alanda yapılır.

### 1. Stack vs Heap Farkı

Bu iki kavram, verilerin bellekte nasıl depolanacağını ve ne kadar hızlı erişileceğini belirler.

**Stack (Yığın) Bellek:**
*   **Nedir?** Üst üste dizilmiş kitaplar gibi çalışan, çok düzenli ve statik bir bellek alanıdır. "Son giren ilk çıkar" (LIFO - Last In First Out) mantığıyla çalışır.
*   **Ne Tutar?** Boyutu önceden belli olan basit veri tiplerini (int, boolean, float) ve kodun çalışma sırasını tutar. Ayrıca Heap'te tutulan büyük verilerin "adreslerini (referanslarını)" de burada saklar.
*   **Avantajı:** Okuma ve yazma hızı muazzam derecede yüksektir. İşlem bitince (örneğin bir fonksiyon görevini tamamladığında) o fonksiyona ait veriler Stack'ten otomatik olarak silinir. Ekstra bir temizlik işlemine gerek yoktur.
*   **Dezavantajı:** Kapasitesi çok sınırlıdır. Çok fazla iç içe fonksiyon çağrısı yaparsanız (sonsuz döngü gibi), kapasite dolar ve meşhur **"Stack Overflow"** (Yığın Taşması) hatasını alırsınız.

**Heap (Öbek) Bellek:**
*   **Nedir?** Geniş, düzensiz ama son derece esnek bir depo alanıdır. Veriler buraya rastgele yerleştirilir.
*   **Ne Tutar?** Boyutu kod yazılırken belli olmayan, dinamik olarak büyüyüp küçülebilen karmaşık verileri (Nesneler - Objects, Diziler - Arrays) tutar. 
*   **Avantajı:** Kapasitesi çok büyüktür (RAM'in fiziksel boyutuyla sınırlıdır). Büyük ve karmaşık verileri saklamak için tek yoldur.
*   **Dezavantajı:** Stack'e göre çok daha yavaştır. Çünkü veriyi bulmak için önce Stack'teki adrese bakmak, sonra o adres üzerinden Heap'teki depoya gitmek gerekir. Ayrıca buradaki veriler otomatik olarak silinmez; temizlenmesi için bir mekanizmaya ihtiyaç vardır.


### 2. Garbage Collection (GC - Çöp Toplayıcı) Nasıl Çalışır?

*   **Nedir?** C#, Java, JavaScript, Python gibi modern dillerde, Heap belleğinde artık kullanılmayan verileri (çöpleri) tespit edip silen ve belleği otomatik olarak sisteme geri kazandıran arka plan aracıdır.
*   **Nasıl Çalışır?** Bir restoranda boşalan masaları temizleyen bir garson gibi düşünebilirsiniz. En yaygın çalışma mantığı **"Mark and Sweep" (İşaretle ve Süpür)** algoritmasıdır:
    1.  **Mark (İşaretle):** GC, Stack'ten yola çıkarak Heap'teki hangi nesnelere hala ulaşılabildiğini (bağlantısı olduğunu) kontrol eder. Ulaşılabilenlere "kullanımda" işareti koyar.
    2.  **Sweep (Süpür):** Hiçbir yerden ulaşılamayan, referansı kopmuş (sahipsiz kalmış) nesneleri tespit eder ve onları bellekten silerek alanı boşaltır.
*   **Neden Önemlidir?** Eğer C veya C++ gibi diller kullanıyorsanız GC yoktur; belleği manuel olarak temizlemeniz (örneğin `free()` komutuyla) gerekir. GC olan diller geliştiriciyi bu yükten kurtarır, ancak işlemciyi meşgul ettiği için çalıştığı anlarda uygulamada anlık takılmalara (mikro saniyeler düzeyinde) sebep olabilir.


### 3. Memory Leak (Bellek Sızıntısı) Nedir, Nasıl Oluşur?

*   **Nedir?** Programın artık işine yaramayan ama bir nedenden ötürü Garbage Collector'ın (Çöp Toplayıcı) silemediği verilerin bellekte birikerek yeri işgal etmeye devam etmesidir. 
*   **Nasıl Oluşur?** GC sadece "hiçbir bağlantısı kalmayan" verileri siler. Eğer siz bir veriyi kullanmayı bıraksanız bile, kodun bir yerinde o veriye gizlice bir bağlantı (referans) bırakırsanız, GC o veriyi "hala kullanılıyor" sanır ve silmez. En yaygın sebepleri:
    1.  Gereksiz yere **Global (genel) değişkenler** kullanmak (program kapanana kadar silinmezler).
    2.  Açılan veritabanı, dosya okuma veya ağ (network) **bağlantılarını iş bitince kapatmamak**.
    3.  Arayüzde oluşturulan **Event Listener**'ları (olay dinleyicileri), ilgili sayfa veya bileşen ekrandan kaybolduğunda iptal etmemek.
*   **Sonuçları Nelerdir?** 
    *   Uygulama çalıştıkça RAM tüketimi sürekli artar (bellek şişer).
    *   Cihaz gereksiz yere efor sarf ettiği için pil hızlı tükenir ve ısınma başlar.
    *   Bellek tamamen dolduğunda uygulama **"Out of Memory" (Bellek Yetersiz)** hatası vererek aniden çöker.
