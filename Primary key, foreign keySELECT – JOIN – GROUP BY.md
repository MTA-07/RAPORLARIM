Veritabanı Mantığı (SQL Temelleri)
1. Relational Database (İlişkisel Veritabanı) Nedir?
Relational Database, verilerin satırlar ve sütunlardan oluşan tablolar halinde tutulduğu ve bu tabloların birbirleriyle belirli kurallar çerçevesinde ilişkilendirildiği veritabanı türüdür.

Bunu birbirine bağlı gelişmiş Excel sayfaları gibi düşünebilirsin. Her tablo belirli bir varlığı (örneğin Kullanicilar, Siparisler, Urunler) temsil eder. Bu yapı veri tekrarını (aynı veriyi defalarca yazmayı) önler ve veri bütünlüğünü sağlar.

Popüler ilişkisel veritabanlarına örnekler: PostgreSQL, MySQL, Microsoft SQL Server, Oracle.

2. Primary Key (PK) ve Foreign Key (FK) Nedir?
Bu iki kavram, ilişkisel veritabanlarındaki tabloları birbirine bağlayan yapıştırıcılardır.

Primary Key (Birincil Anahtar)
Bir tablodaki her bir kaydı (satırı) tekil (unique) olarak tanımlayan kolondur.

Asla boş bırakılamaz (NOT NULL).

Aynı değerden iki tane bulunamaz.

Gerçek Hayat Örneği: Senin T.C. Kimlik Numaran, vatandaşlık veritabanındaki Primary Key'indir.

Foreign Key (Yabancı Anahtar)
Farklı iki tabloyu birbirine bağlayan kolondur. Bir tablodaki Foreign Key, başka bir tablonun Primary Key'ini işaret eder.

Gerçek Hayat Örneği: Siparisler tablosunda siparişi kimin verdiğini tutmak için kullanıcının adını yazmak yerine, kullanıcının Kullanici_ID'sini (PK) yazarız. Bu ID, Siparişler tablosunda bir Foreign Key olur.

3. Temel SQL Komutları: SELECT – JOIN – GROUP BY
SELECT
Veritabanından verileri sorgulamak ve çekmek (okumak) için kullanılır. En temel SQL komutudur.

SQL
-- Tüm kullanıcıları getirir
SELECT * FROM Kullanicilar;

-- Sadece kullanıcıların adını ve e-posta adresini getirir
SELECT ad, email FROM Kullanicilar;
JOIN
Farklı tablolardaki verileri, aralarındaki ilişkilere (genellikle PK ve FK) dayanarak tek bir sonuç kümesinde birleştirmek için kullanılır. En sık kullanılanı INNER JOIN'dir (Sadece her iki tabloda da eşleşen kayıtları getirir).

SQL
-- Kullanıcıları ve onların verdikleri siparişleri bir arada getirir
SELECT Kullanicilar.ad, Siparisler.siparis_tarihi, Siparisler.tutar
FROM Kullanicilar
INNER JOIN Siparisler ON Kullanicilar.ID = Siparisler.Kullanici_ID;
GROUP BY
Verileri belirli bir kolona veya kolonlara göre gruplamak için kullanılır. Genellikle matematksel özetleme fonksiyonlarıyla (Aggregate Functions - COUNT, SUM, AVG, MAX, MIN) birlikte kullanılır.

SQL
-- Hangi kullanıcının toplam ne kadar tutarlık sipariş verdiğini bulur
SELECT Kullanici_ID, SUM(tutar) as ToplamHarcama
FROM Siparisler
GROUP BY Kullanici_ID;
4. Index (İndeks) Ne İşe Yarar?
İndeks, veritabanında arama işlemlerini (veriyi bulmayı) çok daha hızlı hale getiren yapısal bir özelliktir.

Nasıl Çalışır? Bir kitabın sonundaki "Dizin" veya başındaki "İçindekiler" kısmı gibi çalışır. Kitapta belirli bir kelimeyi bulmak için 500 sayfayı tek tek okumak yerine, dizine bakıp kelimenin bulunduğu sayfayı anında açarsın. Veritabanı da milyonlarca satırı tek tek taramak (Full Table Scan) yerine, indekse bakarak veriyi saniyeler içinde bulur.

Dezavantajı: Veri okumayı (SELECT) inanılmaz hızlandırırken, tabloya yeni veri ekleme veya güncelleme (INSERT, UPDATE, DELETE) işlemlerini bir miktar yavaşlatır. Çünkü her yeni kayıtta indeksin de güncellenmesi gerekir. Bu yüzden sadece sık arama yapılan kolonlara indeks eklenmelidir.