  API Mantığı (REST & JSON Temelleri)

1️ API Nedir? Neden Vardır?
 API (Application Programming Interface) Nedir?

API, iki yazılımın birbiriyle konuşmasını sağlayan arayüzdür.

Basit Tanım:

API = Programların birbirine veri göndermesini sağlayan sistem

Örnek:

Mobil uygulama → Sunucuya istek atar

Sunucu → Veritabanından veri alır

Sunucu → Mobil uygulamaya JSON formatında cevap döner

 API Neden Vardır?

Çünkü:

Frontend (kullanıcı arayüzü) ile Backend (sunucu) ayrı çalışır

Mobil, web, masaüstü aynı backend’i kullanabilir

Sistemler modüler olur

Güvenlik ve ölçeklenebilirlik sağlanır


REST Nedir?
REST (Representational State Transfer)

REST, API tasarlama mimarisidir.

RESTful API’ler:

HTTP protokolünü kullanır

URL yapısı düzenlidir

HTTP metodlarını kullanır (GET, POST vs.)

Örnek URL:

https://siteadi.com/api/users
3️ HTTP Metodları
1️ GET

Veri almak için kullanılır.

Örnek:

GET /users

Anlamı:

Kullanıcı listesini getir.

2️ POST

Yeni veri oluşturmak için kullanılır.

Örnek:

POST /users

Body:

{
  "name": "Mehmet",
  "age": 20
}

Anlamı:

Yeni kullanıcı oluştur.

3️ PUT

Var olan veriyi güncellemek için kullanılır.

Örnek:

PUT /users/1

Body:

{
  "name": "Mehmet Turan",
  "age": 21
}

Anlamı:

ID’si 1 olan kullanıcıyı güncelle.

4️ DELETE

Veri silmek için kullanılır.

Örnek:

DELETE /users/1

Anlamı:

ID’si 1 olan kullanıcıyı sil.

4️ JSON Nedir?
JSON (JavaScript Object Notation)

API’lerin veri gönderirken kullandığı formattır.

Ana Özellikleri:

Anahtar – Değer yapısı vardır

Stringler çift tırnak içindedir

Hafif ve okunabilir

JSON Örnekleri

Basit JSON:

{
  "name": "Mehmet",
  "age": 20,
  "isStudent": true
}

Liste içeren JSON:

{
  "users": [
    {
      "id": 1,
      "name": "Ali"
    },
    {
      "id": 2,
      "name": "Veli"
    }
  ]
}
5️ Basit Bir Endpoint Nasıl Tasarlanır?
Senaryo:

Bir "Kitap API" tasarlayalım.

1. Kaynak Belirlenir (Resource)

Kaynak: books

2. URL Tasarlanır
GET     /books          → Tüm kitaplar
GET     /books/1        → ID’si 1 olan kitap
POST    /books          → Yeni kitap ekle
PUT     /books/1        → Kitabı güncelle
DELETE  /books/1        → Kitabı sil
3. Örnek Response
GET /books/1

Response:

{
  "id": 1,
  "title": "Clean Code",
  "author": "Robert C. Martin",
  "year": 2008
}
6️ REST API Tasarlarken Dikkat Edilecekler

✔ URL’ler isim (noun) olmalı, fiil olmamalı
❌ /getUsers
✔ /users

✔ Çoğul kullanılmalı
✔ /books

✔ HTTP metodları doğru kullanılmalı

✔ Status Code dönülmeli

200 → Başarılı

201 → Oluşturuldu

400 → Hatalı istek

404 → Bulunamadı

500 → Sunucu hatası

Özet:

API:
→ Sistemlerin konuşmasını sağlar

REST:
→ API tasarım standardıdır

HTTP Metodları:
GET – POST – PUT – DELETE

JSON:
→ Veri taşıma formatıdır

Endpoint:
→ Belirli bir kaynağa erişim adresidir

Backend Yolculuğu İçin Önemi

API mantığını anlamak:

Backend öğrenmenin temelidir

Web geliştirme için zorunludur

Mobil + Web projelerin temelidir

Mikroservis mimarisinin başlangıcıdır