Güvenlik Temelleri (Security Basics)

Kazanım: Bu konuyu kavradığında; sadece “çalışan ama güvensiz” yazılımlar yazmaktan kurtulur, kullanıcı verilerini koruyan, en yaygın siber saldırılara karşı dirençli ve endüstri standartlarına uygun güvenli sistemler inşa edebilirsin.

Bir uygulamanın çok hızlı çalışması veya harika bir arayüze sahip olması, güvenlik açıkları varsa hiçbir anlam ifade etmez. Güvenlik, sonradan eklenen bir özellik değil, yazılımın temel taşlarından biri olmalıdır.

1. Authentication (Kimlik Doğrulama) vs Authorization (Yetkilendirme)

İsimleri birbirine çok benzediği için sıkça karıştırılan bu iki kavram, güvenliğin kapı bekçileridir ve birbirini takip eden iki farklı aşamayı temsil eder.

Authentication (Kimlik Doğrulama - AuthN):

Nedir? Sistemin kullanıcıya "Sen kimsin?" sorusunu sorması ve kullanıcının iddia ettiği kişi olup olmadığını doğrulamasıdır.

Nasıl Çalışır? Kullanıcı adı ve şifre girmek, Telefona gelen SMS kodunu (2FA) onaylamak, yüz tanıma (FaceID) veya parmak izi okutmak birer Authentication işlemidir.

Benzetme: Bir şirket binasına girerken güvenlik görevlisine personel kimlik kartınızı gösterip turnikeden geçmenizdir. Güvenlik sizin o şirketin çalışanı olduğunuzu doğrular ve binaya girmenize izin verir.

Authorization (Yetkilendirme - AuthZ):

Nedir? Kimliği doğrulanmış (içeri girmiş) bir kullanıcının "Neleri yapmaya izni var?" sorusunun cevabıdır. Her içeri giren her yere erişemez.

Nasıl Çalışır? Sisteme giriş yaptıktan sonra sizin bir "Normal Kullanıcı" mı, "Moderatör" mü yoksa "Admin (Yönetici)" mi olduğunuza bakılır. Kendi profil fotoğrafınızı değiştirebilmeniz ama başka bir kullanıcının hesabını silememeniz Authorization kuralları ile belirlenir.

Benzetme: Turnikeden geçip şirket binasına girdiniz (Authentication başarılı). Ancak kartınız sadece kendi çalıştığınız 3. kattaki ofisin kapısını açar; 5. kattaki "Sistem Odası"na veya "CEO Odası"na girmeye çalıştığınızda kapı açılmaz. İşte bu sınırlandırma Authorization'dır.

2. JWT (JSON Web Token) ve OAuth Mantığı

Modern web ve mobil uygulamalarda kullanıcı oturumlarını yönetmek ve güvenli veri paylaşımı yapmak için kullanılan iki temel standarttır.

JWT (JSON Web Token):

Nedir? Kullanıcı sisteme giriş yaptığında, sunucunun o kullanıcıyı tekrar tekrar veritabanından sorgulamamak için ona verdiği dijital olarak imzalanmış şifreli bir kimlik kartıdır (Token).

Nasıl Çalışır? (Her Şey Dahil Otel Bilekliği):

Otele ilk girdiğinizde resepsiyona kimliğinizi verirsiniz, kayıtlarınız kontrol edilir (Giriş işlemi).

Resepsiyon size kolunuza takmanız için özel bir bileklik (JWT) verir.

Tatil boyunca havuza girerken veya restorandan yemek alırken her seferinde nüfus cüzdanınızı gösterip kayıt kontrolü yaptırmazsınız; sadece bilekliğinizi gösterirsiniz.

Uygulamalarda da giriş yaptıktan sonra sunucu size bir JWT verir. Sepete ürün eklerken veya profilinizi güncellerken tarayıcınız bu JWT'yi sunucuya gösterir. Sunucu üzerindeki dijital imzaya bakar, sahte olmadığını anlar ve işlemi anında yapar.

OAuth (Open Authorization):

Nedir? Şifrenizi üçüncü parti bir uygulamayla paylaşmadan, başka bir platformdaki (Google, GitHub, Apple, Facebook) hesap bilgilerinize sınırlı erişim izni vermenizi sağlayan protokoldür. Sitelerde gördüğümüz "Google ile Giriş Yap" butonlarının arkasındaki teknolojidir.

Nasıl Çalışır? (Vale Anahtarı Mantığı):
Lüks araçlarda normal anahtarın yanında bir de "Vale Anahtarı" (Valet Key) bulunur. Arabanızı otopark görevlisine (valeye) verirken bu özel anahtarı verirsiniz. Bu anahtar arabayı çalıştırır ve park etmeye yarar; ancak torpido gözünü ve bagajı açamaz, aracın belirli bir hızı geçmesine izin vermez.

Yeni üye olduğunuz bir oyun sitesine Google şifrenizi (asıl anahtarı) vermek çok tehlikelidir.

Bunun yerine OAuth kullanarak Google'a yönlendirilirsiniz. Google o siteye bir "Vale Anahtarı" (Access Token) verir. Böylece o site sizin e-postalarınızı okuyamaz, Drive dosyalarınızı silemez; sadece Google'ın izin verdiği kadarını (Adınız, Soyadınız ve E-posta adresiniz) görebilir.

3. SQL Injection (SQLi) ve XSS Nedir?

Yazılımlarda en sık karşılaşılan, "kullanıcıdan gelen veriye körü körüne güvenmekten" kaynaklanan iki büyük siber saldırı türüdür.

SQL Injection (SQL İğneleme / Sızma):

Nedir? Saldırganın, uygulamadaki veri giriş alanlarına (kullanıcı adı kutusu, arama çubuğu vb.) normal bir metin yerine gizli veritabanı komutları (SQL sorguları) yazarak veritabanını kandırması, verileri çalması veya silmesidir. Doğrudan sunucuyu ve veritabanını hedef alır.

Nasıl Oluşur? Eğer yazılımcı, kullanıcının kutucuğa yazdığı metni hiçbir kontrolden geçirmeden doğrudan veritabanı sorgusunun içine yapıştırırsa oluşur.

Örnek: Saldırgan şifre kısmına gerçek bir şifre yerine ' OR '1'='1 yazar. Veritabanı bunu "Şifresi doğruysa VEYA 1 sayısı 1'e eşitse içeri al" şeklinde bir komut olarak algılar. 1 her zaman 1'e eşit olduğu için, saldırgan şifreyi bilmeden Admin olarak sisteme girer.

Nasıl Önlenir? Kullanıcıdan gelen veriyi asla doğrudan komuta eklemeyerek! Prepared Statements (Parametreli Sorgular) veya modern ORM araçları (Entity Framework, Hibernate, Prisma vb.) kullanıldığında, sistem kullanıcının yazdığı ' OR '1'='1 ifadesini bir "komut" olarak değil, sadece normal bir "metin" olarak kabul eder ve saldırı boşa çıkar.

XSS (Cross-Site Scripting - Siteler Arası Betik Çalıştırma):

Nedir? Saldırganın bir web sitesine zararlı JavaScript kodları gizleyerek, o sayfayı ziyaret eden diğer masum kullanıcıların tarayıcılarında bu kodları çalıştırmasıdır. SQL Injection veritabanını hedef alırken, XSS doğrudan diğer kullanıcıları hedef alır.

Nasıl Oluşur? Örneğin bir e-ticaret sitesinin ürün yorumları kısmına saldırgan şu yorumu yazar: Harika ürün! <script>kullanicininCerezleriniCalVeBanaGonder()</script>.

Eğer yazılımcı bu yorumu temizlemeden veritabanına kaydedip ekranda gösterirse; o ürüne bakan yüzlerce masum kullanıcının ekranında sadece "Harika ürün!" yazar ama arka planda o gizli <script> kodu çalışır.

Sonuç olarak o sayfayı açan herkesin oturum bilgileri (JWT veya Cookie'leri) saldırganın eline geçer ve hesapları çalınır.

Nasıl Önlenir? Kullanıcıdan gelen tüm girdileri temizleyerek (Sanitization) ve ekrana basarken <, >, & gibi özel kod karakterlerini zararsız düz metinlere dönüştürerek (Encoding / Escaping). Günümüzde React, Angular, Vue gibi modern arayüz kütüphaneleri bu korumayı büyük ölçüde otomatik olarak yapmaktadır.