---
layout: single
title: "Günlük Geliştirme Süreçlerinde Hayat Kurtaran Linux Terminal Komutları ve Pratikleri"
date: 2026-07-05 10:00:00 +0300
categories: [sistem]
tags: [linux, terminal, komutlar, devops, ipuclari]
excerpt: "Yazılım geliştiricilerin günlük iş akışlarında sıklıkla ihtiyaç duyduğu temel ve ileri düzey Linux terminal komutlarını keşfedin."
---

Yazılım geliştirme, bulut sunucu yönetimi veya DevOps süreçleriyle ilgilenen her geliştiricinin yolu bir noktada **Linux terminali** ile kesişir. Grafik arayüzler (GUI) ne kadar gelişmiş olursa olsun, terminalin sunduğu hız, otomasyon gücü ve esneklik hiçbir şeyle değiştirilemez. Özellikle uzak sunuculara (`SSH` üzerinden) bağlanıldığında, tüm işlemler komut satırı üzerinden yürütülmek zorundadır.

Bu yazımızda, günlük yazılım geliştirme süreçlerinde en çok ihtiyaç duyacağınız temel ve orta düzey Linux terminal komutlarını, gerçek hayat senaryolarını ve ipuçlarını detaylıca inceleyeceğiz.

---

## 1. Dosya ve Dizin Yönetimi: Hızlı Navigasyon

Terminalde kaybolmamak ve dosyalar arasında saniyeler içinde geçiş yapabilmek en temel beceridir.

* **`pwd` (Print Working Directory):** Şu an hangi dizinde olduğunuzu tam yol (path) olarak gösterir.
* **`ls -la`:** Bulunduğunuz dizindeki gizli dosyalar da dahil olmak üzere tüm dosyaları detaylı (boyut, izinler, tarih) listeler.
* **`cd ~` veya `cd`:** Sizi doğrudan kullanıcı ana dizininize (`home`) götürür.

### Örnek Senaryo: Derin Dizin Yapısı Oluşturma
Bir projede iç içe birden fazla klasör oluşturmanız gerekiyorsa, her biri için ayrı ayrı `mkdir` yazmak yerine `-p` parametresini kullanabilirsiniz:

```bash
# Tek komutla iç içe klasör yapısı oluşturma
mkdir -p projeler/backend/src/controllers
```
## 2. Metin Arama ve Log İnceleme (grep, find, cat)
Uygulama sunucularında hata ayıklarken (debugging) binlerce satırlık log dosyaları arasında kaybolmak muhtemeldir. Bu tür durumlarda filtreleme araçları hayat kurtarır.

grep ile Metin İçinde Arama
Bir log dosyasında belirli bir hata kodunu veya kelimeyi aramak için grep komutu kullanılır:

```Bash
# error kelimesini case-insensitive (büyük/küçük harf duyarsız) olarak arama
grep -i "error" server.log
```
tail -f ile Canlı Log Takibi
Bir web sunucusu çalışırken anlık gelen istekleri veya hataları izlemek için canlı takip yapabilirsiniz:

```Bash
# Log dosyasının son 50 satırını göster ve yeni gelenleri anlık ekrana bas
tail -n 50 -f /var/log/nginx/access.log
```
## 3. Süreç (Process) ve Kaynak Yönetimi (ps, top, kill)
Sunucunuzda donanım kaynaklarını tüketen veya yanıt vermeyen bir süreci sonlandırmak gerekebilir.

ps aux: O an sistemde çalışan tüm süreçleri detaylı listeler.

top veya htop: Sistemdeki CPU ve RAM kullanımını anlık olarak izlemenizi sağlayan interaktif arayüzler sunar.

Süreç Sonlandırma Örneği
Çalışmayan veya kilitlenen bir Node.js uygulamasını PID (Process ID) numarası üzerinden sonlandırmak için:

```Bash
# Önce süreci bulma
ps aux | grep node

# Bulunan PID (Örn: 4122) ile süreci sonlandırma
kill -9 4122
```
## 4. Ağ (Network) ve Bağlantı Testleri (curl, ping, netstat)
API geliştirirken veya sunucu ağ bağlantılarını test ederken kullanılan temel araçlardır.

```Bash
# Bir API endpoint'ine test isteği atma ve başlıkları görme
curl -I [https://api.ornek.com/v1/status](https://api.ornek.com/v1/status)

# Yerel makinede hangi portların açık olduğunu ve hangi servislerin çalıştığını görme
netstat -tuln
```
## 5. Güvenlik ve İzin Yönetimi (chmod, chown)
Linux'ta dosya erişim yetkileri güvenlik açısından kritik önem taşır. Özellikle çalıştırma (executable) yetkisi vermemiz gereken bash betiklerinde (.sh) bu komutları sıkça kullanırız.

```Bash
# Bir betik dosyasına çalıştırma (execute) yetkisi verme
chmod +x deploy.sh

# Bir dosyanın sahip (owner) kullanıcı ve grubunu değiştirme
chown www-data:www-data /var/www/html/index.php
```
En İyi Pratikler (Best Practices)
Tab Tamamlama (Tab Completion): Uzun dosya veya klasör isimlerini yazarken klavyedeki Tab tuşunu kullanarak otomatik tamamlama yapın; bu hem hız kazandırır hem de yazım hatalarını önler.

Geçmişi Kullanma (history / Ok Tuşları): Daha önce yazdığınız karmaşık komutları tekrar yazmak yerine klavyedeki yukarı ok tuşuyla geçmişe gidebilir veya history komutunu aratabilirsiniz.

rm -rf Komutuna Dikkat: rm -rf (recursive force delete) komutu dosyaları geri dönüşüm kutusuna atmadan kalıcı olarak sildiğinden, kök dizinde (/) veya yanlış klasörde çalıştırılmamasına son derece dikkat edilmelidir.

Sonuç
Linux terminal komutlarına hâkim olmak, bir yazılımcının problem çözme hızını ve sistemler üzerindeki kontrolünü doğrudan artırır. Günlük rutinlerinizde bu komutları sıkça kullanarak kas hafızası oluşturabilirsiniz.

Bir sonraki yazımızda görüşmek üzere!
