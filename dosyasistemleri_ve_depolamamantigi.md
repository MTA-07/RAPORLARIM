1.  Dosya Sistemleri: NTFS, ext4 ve APFS

Bir kütüphane düşünün. Kitapların raflara nasıl dizileceği, fihristin nasıl tutulacağı ve bir kitap kaybolursa ne yapılacağı kurallar bütününe Dosya Sistemi denir. İşletim sistemi, diskin üzerine veriyi rastgele yazmaz; bu kurallara göre yazar.

A. NTFS (New Technology File System)
Kimin: Microsoft (Windows).

Mantığı: Güvenlik ve izinler (ACL - Access Control Lists) üzerine kuruludur. Kimin hangi dosyayı okuyabileceğini çok detaylı denetler.

Özelliği: "Journaling" (Günlükleme) özelliği vardır. Elektrik kesilirse, diskteki veri bozulmasın diye yapılan işlemlerin kaydını tutar.

Dezavantajı: Zamanla fragmantasyon (parçalanma) sorunu yaşar. Dosyalar diskin farklı yerlerine dağılır, bu yüzden arada sırada "birleştirme" (defrag) yapmak gerekebilir (özellikle HDD'lerde).

B. ext4 (Fourth Extended Filesystem)
Kimin: Linux (Android, Ubuntu, sunucular).

Mantığı: Verimlilik ve performans. Windows'un aksine, dosyaları diske yazarken parçalanmayı (fragmantasyon) en aza indirecek şekilde dağıtır.

Özelliği: Çok büyük dosyaları ve disk boyutlarını destekler. Sunucularda çok tercih edilmesinin sebebi, bozulmalara karşı çok dayanıklı olmasıdır.

Dezavantajı: Windows veya macOS, ek yazılım olmadan ext4 formatlı bir diski okuyamaz.

C. APFS (Apple File System)
Kimin: Apple (macOS, iOS, iPadOS).

Mantığı: SSD ve Flash bellekler için özel olarak sıfırdan tasarlanmıştır. Mekanik diskler (HDD) için değil, modern hızlı diskler içindir.

En Havalı Özelliği (Copy-on-Write): Bir dosyayı kopyaladığınızda, APFS veriyi fiziksel olarak hemen çoğaltmaz; sadece "bu verinin aynısından bir tane daha var" diye işaretler. Bu yüzden 5 GB'lık bir dosyayı kopyalamak APFS'de anında gerçekleşir ve diskte yer kaplamaz (ta ki siz kopyanın üzerinde değişiklik yapana kadar).

Şifreleme: Güvenlik ve şifreleme, dosya sisteminin çekirdeğine gömülüdür.

2. Blok Yapısı Nedir?
Diskinizi kareli bir defter gibi düşünün. Her bir kareye Blok (veya Cluster) denir. İşletim sistemi veriyi bu kutucuklara doldurarak yazar.

En Küçük Birim: Dosya sistemlerinde (örneğin NTFS'de) genellikle bir blok 4 KB (4096 Bayt) büyüklüğündedir.

Mantık: Bir dosya 1 Bayt bile olsa, diske yazıldığında tam bir bloğu (4 KB) işgal eder.

Slack Space (Boşluk): Eğer 5 KB'lık bir dosya yazarsanız, 2 blok kullanırsınız (4 KB + 4 KB). İkinci bloğun sadece 1 KB'ı doludur, kalan 3 KB boştur ama başka dosya oraya yazılamaz. Buna "Slack Space" denir.

Neden Önemli? Blok boyutu çok büyük seçilirse, küçük dosyalar çok fazla yer israf eder. Çok küçük seçilirse, büyük dosyaları okumak için çok fazla adresleme yapmak gerekir ve sistem yavaşlar.

3. HDD vs SSD: Çalışma Prensipleri
Depolama dünyasındaki en büyük devrim, mekanikten elektriğe geçiştir.

A. HDD (Hard Disk Drive - Mekanik Disk)
Eski usül bir plakçalar (gramofon) gibi çalışır.

Yapısı: İçinde dakikada binlerce kez (5400 veya 7200 RPM) dönen manyetik diskler (plaka) ve bu disklerin üzerinde milimetrik hareket eden bir okuma/yazma kafası vardır.

Çalışma Prensibi: Veriye ulaşmak için diskin dönmesi ve kafanın doğru yere gitmesi gerekir. Buna "Erişim Süresi" (Seek Time) denir.

Dezavantajı: İçinde hareketli parça olduğu için sarsıntıya gelemez, düşerse bozulur. Ayrıca "rastgele okuma" hızı yavaştır çünkü kafa sürekli bir oraya bir buraya gitmek zorundadır.

B. SSD (Solid State Drive - Katı Hal Sürücüsü)
Büyük bir USB bellek veya RAM'in kalıcı hali gibidir.

Yapısı: İçinde hareket eden hiçbir parça yoktur. Veriler NAND Flash denilen yongalarda (chiplerde) elektrik yükü olarak saklanır.

Çalışma Prensibi: Bir Excel tablosundaki hücreye gitmek gibidir. İşlemci "Bana 5. bloktaki veriyi ver" der ve veri anında gelir. Dönme veya kafa hareketi bekleme süresi yoktur.

Avantajı: HDD'ye göre 10 ila 100 kat daha hızlıdır. Sessizdir ve darbeye dayanıklıdır.

TRIM Komutu: SSD'lerde silinen verinin "gerçekten" silinmesi ve hücrenin tekrar yazmaya hazır hale getirilmesi için işletim sistemi TRIM komutunu kullanır (HDD'lerde buna gerek yoktur).

Özetle Neyi Bilmelisin?
Formatlarken: Sadece Windows kullanacaksan NTFS, Mac kullanacaksan APFS, Linux kuracaksan ext4 seçmelisin. Hem Mac hem Windows arasında dosya taşıyacaksan ExFAT (burada değinmedik ama ara bir formattır) kullanılır.

Performans: Bilgisayarın yavaşsa, sorumlu genellikle HDD'dir. SSD'ye geçmek, işlemciyi değiştirmekten daha büyük hız farkı yaratır çünkü "Mekanik" hızdan "Elektronik" hıza geçersiniz.

Yer Kaybı: Diskinizde binlerce çok küçük (1KB) dosya varsa, blok yapısı yüzünden diskte sandığınızdan çok daha fazla yer kaplarlar.