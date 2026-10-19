Concurrency & Parallel Programming (Eşzamanlılık ve Paralel Programlama)



Günümüzde uygulamaların aynı anda binlerce kullanıcıya hizmet vermesi veya ağır işlemleri ekranı dondurmadan arka planda yapması gerekir. İşte burada devreye Concurrency ve Parallelism kavramları girer.

1. Concurrency (Eşzamanlılık) vs Parallelism (Paralellik)

Bu iki kavram genellikle birbiriyle aynı sanılır ancak çalışma mantıkları tamamen farklıdır.

Concurrency (Eşzamanlılık):

Nedir? Birden fazla işin aynı zaman dilimi içinde sırayla ama çok hızlı geçişler yapılarak (idare edilerek) yürütülmesidir. Tek bir işlemci çekirdeği bile bunu yapabilir. İşler tam olarak aynı saniyede yapılmaz; ancak işlemci işler arasında o kadar hızlı geçiş yapar ki (Context Switching), dışarıdan bakan biri hepsinin aynı anda ilerlediğini sanır.

Benzetme: Mutfaktaki tek bir aşçının aynı anda hem çorbayı karıştırması, hem fırındaki yemeği kontrol etmesi hem de salata doğramasıdır. Aşçı tektir; salata doğrarken çorbayı karıştırmaz ama ikisi arasında sürekli gidip gelerek iki yemeği de aynı zaman diliminde çıkarır.

Amacı: İşlemciyi (CPU) boşta bekletmemektir. Örneğin; veritabanından bir veri gelmesini beklerken uygulamanın donup kalması yerine, o sırada başka bir kullanıcının isteğini işleme almaktır (Asenkron programlama).

Parallelism (Paralellik):

Nedir? Birden fazla işin fiziksel olarak tamamen aynı anda yürütülmesidir. Bunun gerçekleşebilmesi için donanımsal olarak birden fazla işlemci çekirdeğine (Multi-Core CPU) ihtiyaç vardır.

Benzetme: Mutfakta üç farklı aşçının olmasıdır. Bir aşçı sadece çorbayla, diğeri sadece salatayla, öteki ise fırındaki yemekle ilgilenir. İşler gerçekten aynı saniye içinde, birbirinden bağımsız olarak yürütülür.

Amacı: Çok ağır hesaplama gerektiren işleri (görüntü işleme, yapay zeka modelleri, büyük veri analizi, oyun grafikleri) küçük parçalara bölüp farklı çekirdeklere dağıtarak işi çok daha kısa sürede bitirmektir.

2. Race Condition (Yarış Durumu) Nedir?

Nedir? Birden fazla iş parçacığının (Thread), paylaşılan ortak bir veriye aynı anda erişmeye ve onu değiştirmeye çalışması sonucunda ortaya çıkan veri bozulması ve tutarsızlık durumudur. İşlemin sonucu, hangi iş parçacığının işlemi daha önce bitireceğine ("yarışı kimin kazanacağına") bağlı olduğu için tamamen öngörülemezdir.

Nasıl Oluşur? (Gerçek Hayat Örneği):
Ortak kullanılan bir banka hesabında 100 TL olduğunu düşünün. A ve B kişileri, ellerindeki kartlarla tam olarak aynı saniyede farklı ATM'lerden bu hesaptan 80 TL çekmek istiyor.

A'nın ATM'si bakiyeyi kontrol eder: "Hesapta 100 TL var, 80 TL çekilebilir."

Aynı milisaniyede B'nin ATM'si de henüz A işlemi bitirmediği için bakiyeyi kontrol eder ve o da "Hesapta 100 TL var, 80 TL çekilebilir" der.

İki ATM de kullanıcılara 80'er TL verir.

Sonuç: Hesapta 100 TL vardı ama toplamda 160 TL çekildi. Veriyi koruma altına almadığımız için sistemde büyük bir mantık ve güvenlik açığı (Race Condition) oluştu.

3. Mutex, Semaphore ve Lock Kavramları

Yukarıda bahsettiğimiz Race Condition gibi felaketleri önlemek, yani ortak kullanılan verileri güvenli hale getirmek (Thread-Safe yapmak) için kodumuzda bazı trafik işaretleri ve kilit mekanizmaları kullanırız.

Lock (Kilit):

Nedir? En temel koruma mekanizmasıdır. Ortak bir verinin değiştirildiği kritik kod bloğuna (Critical Section) aynı anda sadece tek bir iş parçacığının (Thread) girmesini sağlar.

Nasıl Çalışır? Bir mağazadaki soyunma kabini gibidir. İçeri ilk giren kişi kapıyı içeriden kilitler. O kişi kıyafetini deneyip dışarı çıkana (kilidi açana) kadar, dışarıdaki diğer tüm müşteriler sıraya girip beklemek zorundadır. (Banka örneğinde Lock kullansaydık; A kişisi işlemi bitirene kadar B kişisinin ATM'si "Lütfen bekleyiniz" diyerek sırasını beklerdi).

Mutex (Mutual Exclusion - Karşılıklı Dışlama):

Nedir? Mantık olarak Lock ile neredeyse aynıdır; aynı anda sadece tek bir işin kaynağa erişmesine izin verir. Ancak Lock genelde sadece tek bir uygulama (process) içindeki iş parçacıklarını hizaya sokarken; Mutex işletim sistemi seviyesinde çalışır ve farklı uygulamalar arasında da kilit görevi görebilir.

Nasıl Çalışır? Kilitli bir odanın tek bir fiziksel anahtarı olması gibidir. Anahtarı (Mutex'i) kim alırsa odaya o girer ve işi bitince anahtarı teslim eder. Örneğin; bilgisayarınızdaki kamerayı veya mikrofonu o an sadece tek bir uygulamanın (Zoom ya da Discord) kullanabilmesini sağlayan şey işletim sistemi seviyesindeki bir Mutex'tir.

Semaphore (Semafor):

Nedir? Lock ve Mutex içeriye sadece 1 kişinin girmesine izin verirken, Semaphore ortak bir kaynağa aynı anda belirli bir sayıda (N kadar) iş parçacığının girmesine izin veren sayaçlı bir mekanizmadır.

Nasıl Çalışır? Kapasitesi 50 araçlık olan bir otopark veya gece kulübü kapısı gibidir. Girişteki görevli (Semaphore) içerideki boş yer sayısını tutar. İçeride yer varsa gelenleri içeri alır ve sayacı düşürür. 50 araç dolduğunda bariyeri kapatır. İçeriden 1 araç çıkana kadar dışarıdakileri bekletir.

Nerede Kullanılır? Genellikle kaynak sınırlandırmalarında kullanılır. Örneğin; bir veritabanı sunucusunun çökmemesi için aynı anda en fazla 10 bağlantıya izin vermek, 11. isteği sıraya alıp bekletmek için Semaphore kullanılır.