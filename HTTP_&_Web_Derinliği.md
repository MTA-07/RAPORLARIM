HTTP & Web Derinliği

Kazanım: Bu konuyu kavradığında; frontend (arayüz) ve backend'in (sunucu) kendi aralarında tam olarak nasıl konuştuğunu anlayacak, aldığın hataların kimden kaynaklandığını (senden mi yoksa sunucudan mı) anında çözecek ve meşhur CORS hatalarıyla başa çıkabileceksin.

Web dünyasındaki her şey bir "İstek" (Request) ve "Cevap" (Response) döngüsü üzerine kuruludur. Bu iletişimi sağlayan kurallar bütününe HTTP (Hypertext Transfer Protocol) denir.

1. HTTP Request (İstek) ve Response (Cevap) Yapısı

Frontend ile Backend'in iletişimini lüks bir restoran gibi düşünebiliriz.

Müşteri (Client/Frontend): Yemeği isteyen kişi.

Aşçı (Server/Backend): Yemeği hazırlayan kişi.

Garson (HTTP): Siparişi mutfağa götüren ve yemeği masaya getiren aracı.

HTTP Request (İstek - Müşteriden Mutfağa):
Frontend'in sunucudan bir şey istediği pakettir. Temel olarak 4 parçadan oluşur:

Metot (Method/Verb): Ne yapmak istiyorsun?

GET: Sadece veri getir (Menüyü getir).

POST: Yeni veri gönder/kaydet (Yeni sipariş ver).

PUT/PATCH: Var olan veriyi güncelle (Siparişi değiştir).

DELETE: Veriyi sil (Siparişi iptal et).

URL (Adres): İstek nereye gidiyor? (Örn: https://api.site.com/users)

Headers (Başlıklar): İstekle ilgili meta bilgiler ve kimlik. (Örn: "Müşteri VIP mi? Hangi dilde hizmet istiyor? JWT token'ı ne?")

Body (Gövde): Sadece POST veya PUT isteklerinde bulunur. Gönderilen asıl veridir. (Örn: Yeni üye olurken gönderilen Ad, Soyad ve Şifre bilgileri).

HTTP Response (Cevap - Mutfaktan Müşteriye):
Sunucunun işi bitirdikten sonra frontend'e gönderdiği pakettir.

Status Code (Durum Kodu): İşlem başarılı mı, başarısız mı? (Bknz. Bölüm 2)

Headers (Başlıklar): Dönen veri ne tipte? (Örn: "Dönen veri bir JSON dosyasıdır ve 200kb boyutundadır.")

Body (Gövde): İstenilen asıl veri. (Örn: Kullanıcıların listesi veya hata mesajının detayı).

2. Status Code'lar (Durum Kodları)

Sunucunun frontend'e "İşlemin sonucunda ne oldu?" sorusuna verdiği 3 haneli kısa cevaplardır. Restoran örneğinden devam edersek, garsonun masaya döndüğünde size söylediği cümledir.

2xx (Başarı - "Hallettim"):

200 OK: Her şey yolunda, istediğin veriyi getirdim.

201 Created: Gönderdiğin veriyi başarıyla veritabanına kaydettim (Genelde POST sonrası döner).

4xx (İstemci Hatası - "Sen Yanlış Yaptın"): Hata frontend'de veya kullanıcıdadır.

400 Bad Request: Gönderdiğin verinin formatı yanlış veya eksik (Örn: E-posta adresi yerine telefon numarası yazmışsın).

401 Unauthorized: Kimliğin yok! Bu işlemi yapmak için önce sisteme giriş yapmalısın (Örn: Token eksik).

403 Forbidden: Kimliğini biliyorum ama bu işlemi yapmaya yetkin yok! (Örn: Normal kullanıcısın ama admin paneline girmeye çalışıyorsun).

404 Not Found: İstediğin sayfayı veya veriyi bulamadım (Örn: Olmayan bir ID ile ürün arıyorsun).

5xx (Sunucu Hatası - "Ben Çuvalladım"): Hata backend'de (sunucuda) dir.

500 Internal Server Error: Sunucuda bir şeyler patladı. Yazılımcı kodda hata yapmış (Örn: Veritabanı bağlantısı koptu veya kodda mantık hatası var).

503 Service Unavailable: Sunucu şu an çok yoğun veya bakımda, cevap veremiyor.

3. CORS (Cross-Origin Resource Sharing) Nedir?

CORS, yeni başlayan yazılımcıların en çok karşılaştığı ve en sinir bozucu bulduğu tarayıcı güvenlik önlemidir.

Nedir? Modern web tarayıcıları (Chrome, Safari vb.), güvenlik gereği bir web sitesinin (örn: localhost:3000) başka bir domaine (örn: api.baskasite.com) arka planda HTTP isteği atmasını varsayılan olarak engeller. Buna Same-Origin Policy denir. CORS, bu kuralı güvenli bir şekilde esnetip farklı sitelerin birbiriyle konuşmasını sağlayan mekanizmanın adıdır.

Neden Var? Eğer bu kural olmasaydı, siz zararlı bir siteye girdiğinizde, o site sizin tarayıcınız üzerinden arka planda bankanızın web sitesine sanki sizmişsiniz gibi istek atıp paranızı transfer edebilirdi.

Nasıl Çözülür? (CORS Hatası Neden Alınır?)
Eğer frontend localhost:3000'de çalışırken backend localhost:5000'de çalışıyorsa tarayıcı bunu tehdit olarak algılar ve engeller (Meşhur kırmızı CORS hatası).
Çözüm frontend'de değil, backend'dedir! Backend yazılımcısı, sunucu ayarlarına (Headers) şu kuralı eklemelidir: "Benim API'me localhost:3000 adresinden gelen isteklere izin veriyorum, onlar güvenlidir." Bu ayar yapıldığında tarayıcı engeli kaldırır.