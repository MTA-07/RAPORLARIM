1.     Temel Kavramlar: Adresler ve Rehberler

İnterneti devasa bir kargo dağıtım ağı gibi düşünebilirsin.

IP Adresi (Internet Protocol Address)
Nedir? İnternete bağlı her cihazın (bilgisayar, telefon, sunucu) sahip olduğu benzersiz dijital kimlik numarasıdır.

Benzetme: Evinin açık adresi. Kargonun hangi binaya gideceğini belirler.

Örnek: 192.168.1.1 veya 172.217.17.46 (Google).

Port (Kapı)
Nedir? IP adresi cihazı bulur, peki o cihazın içindeki hangi uygulamaya gidecek? Port, sunucu içindeki sanal kapı numarasıdır.

Benzetme: Kargo binaya geldi (IP), ama kime teslim edilecek? Daire numarası (Port).

Örnekler:

Web siteleri (HTTP) genellikle 80. kapıdan girer.

Güvenli web siteleri (HTTPS) 443. kapıyı kullanır.

DNS (Domain Name System)
Nedir? İnsanlar sayıları (IP adreslerini) akılda tutamaz, kelimeleri tutar. DNS, yazdığın site ismini IP adresine çeviren sistemdir.

Benzetme: Telefon rehberi. Sen "Ahmet" (domain adı) ismine basarsın, telefon arkada "0555..." (IP adresi) numarasını çevirir.

Süreç: Tarayıcıya google.com yazarsın -> DNS sunucusu "Bunun adresi 172.217.17.46" der -> Bilgisayarın o adrese gider.

2.     İletişim Protokolleri: TCP ve UDP

Verinin A noktasından B noktasına nasıl taşınacağını belirleyen kurallar bütünüdür.

TCP (Transmission Control Protocol) – "Garantici"
Özelliği: Güvenilirdir. Verinin eksiksiz ve sırasıyla gittiğinden emin olur. Karşı taraftan "Aldım" onayı bekler.

Kullanım Alanı: Web siteleri, E-postalar, Dosya transferi. (Bir harfin bile eksik olması web sitesini bozar).

Mantığı: "Paket 1 ulaştı mı? Evet. Paket 2 ulaştı mı? Evet..."

UDP (User Datagram Protocol) – "Hızlıcı"
Özelliği: Çok hızlıdır ama garantisi yoktur. Veriyi fırlatır atar, ulaşıp ulaşmadığına bakmaz.

Kullanım Alanı: Online oyunlar, Canlı yayınlar, Görüntülü konuşmalar. (Görüntülü konuşmada anlık bir kare kaybolsa da akış devam etmelidir, donup o kareyi beklemek istemeyiz).

3.       Paket Yapısı: Veri Nasıl Paketlenir?
İnternette "Selam" yazdığında bu veri tek parça halinde gitmez. Küçük parçalara (paketlere) bölünür. Her paketin bir yapısı vardır:

Header (Başlık) - Zarfın Üzeri:

Gönderen IP: Mektup geri dönerse kime gelecek?

Alıcı IP: Nereye gidiyor?

Protokol: İçinde ne var? (TCP mi UDP mi?)

Sıra No: Bu kaçıncı parça? (Örneğin: 10 paketin 3.sü)

Payload (Yük) - Zarfın İçi:

Asıl taşınan veri (Mesajın kendisi, resmin bir parçası vb.).

Trailer (Kuyruk):

Paketin sonunu belirtir ve hata kontrolü yapar (Yolda bozuldu mu?).

4.      Alet Çantası (Komut Satırı Araçları)
Bu araçlar, bir ağ mühendisinin veya yazılımcının "stetoskop"udur. Sorunları dinlemek için kullanılır.

Ping (Packet Internet Groper):

Ne yapar? Karşıdaki bilgisayara "Orada mısın?" diye küçük bir paket atar. O da "Buradayım" der.

Amaç: Bağlantı var mı? Cevap ne kadar sürede (ms cinsinden) geliyor? (Lag var mı?)

Örnek: ping google.com

Traceroute (veya Windows'ta tracert):

Ne yapar? Verinin senin bilgisayarından hedefe gidene kadar hangi duraklardan (router/yönlendirici) geçtiğini listeler.

Amaç: Bağlantı yavaşsa veya kopuksa, sorunun nerede olduğunu (senin modemin mi, servis sağlayıcın mı, yoksa hedef sunucu mu?) anlamanı sağlar.

Nslookup:

Ne yapar? DNS sorgusu yapar. Bir alan adının hangi IP adresine karşılık geldiğini söyler.

Amaç: "Siteye giremiyorum, acaba DNS sunucum mu bozuk?" sorusuna cevap arar.

Örnek: nslookup google.com

Özet: Bir Web Sitesine Girdiğinde Ne Olur?
Tarayıcıya example.com yazarsın.

DNS devreye girer, bu ismin IP adresini bulur.

Bilgisayarın o IP adresindeki sunucunun 80 veya 443 Portuna bir istek gönderir.

Bu istek TCP protokolü ile güvenli bir şekilde paketlenir.

Veri, küçük Paketlere bölünür; her paketin üzerine adres yazılır.

Paketler kablolar/wi-fi üzerinden sunucuya ulaşır, sunucu paketleri birleştirir, senin isteğini anlar ve sana web sitesinin verilerini geri yollar.