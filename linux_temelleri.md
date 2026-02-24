1. Temel Terminal Komutları (Navigasyon ve Dosya Yönetimi)
Grafik arayüz (mouse ile tıklama) yerine, bilgisayarla "konuştuğun" yerdir.

ls (List): Bulunduğun klasördeki dosyaları listeler.

İpucu: ls -la kullanırsan hem gizli dosyaları (.) görürsün hem de dosya detaylarını (boyut, izinler).

cd (Change Directory): Klasörler arası geçiş yapar.

Örnek: cd /home/kullanici/belgeler (Belgelere git), cd .. (Bir üst klasöre çık).

mkdir (Make Directory): Yeni klasör oluşturur.

Örnek: mkdir Projelerim.

grep (Global Regular Expression Print): Dosyaların içinde metin arar. Bir yazılımcı için en hayati komutlardan biridir.

Örnek: grep "Hata" log.txt (log.txt dosyasındaki "Hata" geçen satırları bul).

top: Windows'taki "Görev Yöneticisi"nin terminal halidir.

Kullanım: CPU ve RAM'i en çok hangi programın yediğini canlı izlersin. Çıkmak için q tuşuna basman yeterli.

2. Dosya İzinleri ve chmod
Linux'ta güvenlik her şeydir. Her dosyanın bir sahibi ve o dosya üzerinde kimin ne yapabileceğini belirleyen kurallar vardır.

Mantık (rwx):

r (read - okuma): Dosyayı açıp bakabilir.

w (write - yazma): Dosyayı değiştirebilir veya silebilir.

x (execute - çalıştırma): Dosya bir programsa (script gibi) onu çalıştırabilir.

chmod (Change Mode): İzinleri değiştirir.

Rakamlarla Kullanım: 4 (oku), 2 (yaz), 1 (çalıştır).

Örnek: chmod 777 dosya (Herkes her şeyi yapabilir - Güvenlik riski!).

Örnek: chmod +x script.sh (Dosyaya çalıştırma izni ver, böylece ./script.sh diyerek çalıştırabilirsin).

3. Paket Yönetimi (App Store Mantığı)
Linux'ta program (paket) yüklemek için internete girip .exe indirmeyiz. Merkezi bir depodan komutla çekeriz. Kullandığın Linux dağıtımına (versiyonuna) göre komut değişir:

Not: sudo (SuperUser DO), komutu yönetici (admin) yetkisiyle çalıştırmak demektir. Program yüklerken sisteme müdahale ettiğin için sudo şarttır.

4. Servisler (systemctl)
Bilgisayar başladığında arka planda sessizce çalışan programlara "Servis" veya "Daemon" denir. (Örneğin: Web sunucusu, Veritabanı). Bunları yöneten araç systemctldir.

sudo systemctl start nginx: Servisi başlatır.

sudo systemctl stop nginx: Servisi durdurur.

sudo systemctl enable nginx: Bilgisayar her açıldığında bu servis otomatik başlasın.

sudo systemctl status nginx: Servis çalışıyor mu, çöktü mü? (Hata ayıklarken ilk bakacağın yer).