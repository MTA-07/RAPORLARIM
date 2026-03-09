1. Monolith vs Microservice


Bu iki kavram, bir uygulamanın genel hatlarıyla nasıl inşa edileceğini ve barındırılacağını belirler.


Monolith (Monolitik) Mimari: * Nedir? Uygulamanın tüm parçalarının (kullanıcı arayüzü, iş mantığı, veritabanı bağlantıları, arka plan işlemleri) tek bir proje ve tek bir kod tabanı içinde bütünleşik olarak bulunmasıdır.

Avantajları: Başlangıçta geliştirmesi, test etmesi ve sunucuya yüklemesi (deploy) çok kolaydır.

Dezavantajları: Proje büyüdükçe kodlar karmaşıklaşır. Ufacık bir değişiklik için bile tüm projeyi yeniden derleyip sunucuya yüklemek gerekir. Projeyi ölçeklendirmek zordur (sadece yoğun kullanılan kısmı değil, tüm projeyi kopyalamanız gerekir).

Microservice (Mikroservis) Mimarisi:

Nedir? Sistemin tek bir devasa proje yerine, her biri kendi işinden sorumlu, bağımsız çalışan ve birbiriyle ağ üzerinden (genelde API'ler aracılığıyla) haberleşen küçük servislere bölünmesidir (Örn: Ödeme servisi, kullanıcı servisi, kargo servisi ayrı ayrıdır).

Avantajları: Bir serviste hata çıkarsa tüm sistem çökmez. Hangi servis yoğunluk yaşıyorsa sadece o servisin kapasitesi artırılabilir (ölçeklenebilir). Farklı servisler farklı programlama dilleriyle yazılabilir.

Dezavantajları: Kurulumu, yönetimi ve servislerin birbirleriyle iletişimini koordine etmesi zordur ve ileri seviye altyapı bilgisi gerektirir.


2. Mimari Desenler: MVC ve MVVM


Mimari desenler, kodumuzu proje içinde nasıl organize edeceğimizi gösteren şablonlardır. Amaç, karmaşayı önlemek ve farklı işleri yapan kodları birbirinden ayırmaktır.

MVC (Model - View - Controller)
Web geliştirmede en sık kullanılan, en eski ve en sağlam desenlerden biridir.


Model: Uygulamanın beynidir. Veriyi ve iş kurallarını temsil eder. Veritabanından gelen veriler burada şekillenir.

View: Kullanıcının ekranda gördüğü her şeydir (HTML sayfaları, butonlar, listeler).

Controller: Trafik polisidir. Kullanıcıdan gelen istekleri (örneğin bir butona tıklama) alır, Model'e gidip veriyi işler/getirir ve çıkan sonucu View'a göndererek ekranda gösterilmesini sağlar.

MVVM (Model - View - ViewModel)
Genellikle modern mobil uygulamalarda ve modern frontend frameworklerinde (React, Vue, Angular) kullanılan, verinin ekrana anında yansımasını sağlayan bir desendir.

Model: Verinin kendisidir.

View: Kullanıcı arayüzüdür.

ViewModel: View ile Model arasındaki köprüdür. Ancak Controller'dan farklı olarak Data Binding (Veri Bağlama) kullanır. Yani ViewModel'deki bir veri değiştiği anda, View (ekran) otomatik olarak güncellenir. View, ViewModel'i dinler; ViewModel ise View'ın neye benzediğini bilmez.


3. State Management (Durum Yönetimi) Nedir?


State (Durum): Bir uygulamanın belirli bir andaki anlık hafızasıdır. "Kullanıcı sisteme giriş yaptı mı?", "Sepette hangi ürünler var?", "Uygulama karanlık modda mı yoksa aydınlık modda mı?" gibi bilgilerin tümü "State"tir.

State Management: Uygulama büyüdükçe bu anlık hafızanın (state) onlarca farklı sayfa veya bileşen arasında tutarlı bir şekilde paylaşılması, güncellenmesi ve senkronize tutulması gerekir. Sepete bir ürün eklediğinde sepet ikonundaki sayının anında değişmesi, iyi yönetilen bir State sayesinde olur. (Frontend dünyasında Redux, Context API, Vuex; mobil dünyada Provider, Riverpod, Bloc gibi araçlar bu işi yapar.)


4. Katmanlı Mimari (Service – Repository – Controller)


Backend projelerinin omurgasını oluşturan, kodların "Sorumlulukların Ayrılığı" (Separation of Concerns) prensibine göre klasörlere ve sınıflara bölünmesidir.

Controller Katmanı (Sunum): Sadece ve sadece dış dünyadan (kullanıcıdan veya başka bir servisten) gelen API isteklerini karşılar. İsteği alır, Service katmanına iletir ve Service'den gelen cevabı kullanıcıya döndürür. İçinde asla hesaplama veya iş kuralı (business logic) barındırmaz.

Service Katmanı (İş Mantığı): Uygulamanın kalbidir. İş kuralları burada işletilir. Örneğin; "Şifre 8 karakterden uzun mu?", "Kullanıcının bakiyesi yeterli mi?" gibi kontroller burada yapılır. Veriye ihtiyacı olursa Repository'den ister.

Repository Katmanı (Veri Erişimi): Sadece veritabanı (veya harici bir API) ile konuşan katmandır. Veriyi kaydetme, silme, güncelleme ve getirme (CRUD) işlemlerinden sorumludur. Hangi veritabanının kullanıldığını (SQL, MongoDB vs.) Service veya Controller bilmez, bu detay sadece Repository'de gizlidir.