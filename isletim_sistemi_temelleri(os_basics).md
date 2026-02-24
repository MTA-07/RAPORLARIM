           Isletim Sistemi Temelleri (OS Basics)
Ogreneceeklerimiz:
Kernel nedir?
Süreç (process) – iş parçacığı (thread) farkı
Bellek yönetimi nasıl yapılır?
CPU zamanlayıcıları nedir?
Kazanç: Yazılımın “nerede çalıştığını” tam anlamak.




1. Kernel (Çekirdek) Nedir?
Kernel, işletim sisteminin kalbidir. Bilgisayarı açtığında belleğe (RAM) yüklenen ilk kısımdır ve bilgisayar kapanana kadar orada kalır.

Görevi: Donanım (CPU, RAM, Diskler) ile Yazılım (Uygulamalar) arasındaki köprüdür.

Nasıl Çalışır? Biz bir programı açtığımizda (örneğin Chrome), bu program donanıma doğrudan emir veremez. Kernel'e "Bana biraz bellek ver" ya da "Bu dosyayı diske yaz" der. Kernel bu istekleri yönetir.

Analoji: Bir restoran düşünün.

Donanım: Mutfak (Ocak, fırın, malzemeler).

Uygulamalar: Müşteriler (Sipariş verirler).

Kernel: Garsonlardır. Siparişi alır, mutfağa iletir, yemeği getirir ve kimsenin birbirinin yemeğini almamasını sağlar.




2. Süreç (Process) ve İş Parçacığı (Thread) Farkı
Bu ikisi genellikle karıştırılır ama farkları hayatidir.

Süreç (Process)
Çalışmakta olan bir programdır.

İzole: Her sürecin kendine ait bir bellek alanı vardır. Bir süreç çökerse, genellikle diğerlerini etkilemez.

Ağır: Yeni bir süreç başlatmak (process creation) işletim sistemi için maliyetli bir işlemdir.

İş Parçacığı (Thread)
Bir sürecin içinde çalışan "alt görevlerdir".

Paylaşımcı: Aynı sürecin içindeki thread'ler, o sürecin belleğini ve kaynaklarını ortaklaşa kullanır.

Hafif: Başlatılması ve yönetilmesi süreçlere göre çok daha hızlıdır.




3. Bellek Yönetimi (Memory Management)
Bilgisayardaki RAM (Ana Bellek) sınırlıdır, ancak programlar sürekli daha fazla yer ister. İşletim sistemi bu kaosu yönetmek zorundadır.

Takip: Hangi bellek bölgesinin hangi program tarafından kullanıldığını, hangisinin boş olduğunu takip eder.

Sanal Bellek (Virtual Memory): Bu çok kritik bir kavramdır. Fiziksel RAM yetmediğinde, OS diskin (hard disk/SSD) bir kısmını RAM gibi kullanır. Buna "Swap" denir. Bu sayede 8GB RAM'in varken 16GB'lık program çalıştırabilirsin (biraz yavaşlasa da).

İzolasyon: Bir programın (process), başka bir programın belleğine izinsiz girmesini engeller. Bu güvenlik için şarttır.




4. CPU Zamanlayıcıları (CPU Scheduling)
İşlemcin (CPU) çok hızlıdır ama genellikle sınırlı sayıda çekirdeğe sahiptir (örneğin 8 çekirdek). Ancak bilgisayarda aynı anda yüzlerce süreç çalışır. CPU Zamanlayıcısı, "Sırada kim var?" sorusuna karar veren mekanizmadır.

Amaç: CPU'yu hiç boş tutmamak ve kullanıcılara adil davranmak.

Context Switch (Bağlam Değiştirme): CPU bir işlemden diğerine o kadar hızlı geçer ki (milisaniyeler içinde), biz her şeyin "aynı anda" çalıştığını sanırız. Buna "Multitasking" denir.

Yaygın Algoritmalar:

FCFS (First-Come, First-Served): İlk gelen ilk hizmeti alır. (Banka kuyruğu gibi).

Round Robin: Her işleme eşit süre (örneğin 10ms) verilir. Süre bitince sıranın sonuna geçer.

Priority (Öncelik): Önemli işlemler (örneğin işletim sistemi arayüzü) öne geçer.