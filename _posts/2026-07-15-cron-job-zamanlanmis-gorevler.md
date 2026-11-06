---
layout: post
title: "Linux'ta Cron Job ile Zamanlanmış Görevler (Cron Expression) Nasıl Oluşturulur?"
date: 2026-07-15 10:00:00 +0300
categories: [sistem]
tags: [cron, linux, otomasyon, zamanlanmis-gorevler, devops]
excerpt: "Sunucu üzerinde veritabanı yedekleme, e-posta gönderimi ve bakım betiklerini otomatik çalıştırmak için Cron Job kullanımı ve cron sözdizimi rehberi."
---

Yazılım geliştirme ve sistem yönetimi süreçlerinde bazı görevlerin insan müdahalesine gerek kalmadan, belirli periyotlarla otomatik olarak çalışması gerekir. Örneğin; her gece yarısı veritabanı yedeği almak, her pazartesi müşterilere haftalık bülten e-postası göndermek veya geçici dosyaları temizlemek gibi rutin işler otomasyona bağlanmalıdır.

Unix ve Linux tabanlı işletim sistemlerinde bu tür zamanlanmış görevleri yönetmek için **Cron** servisi kullanılır. Bu yazımızda, cron job mantığını, karmaşık gibi görünen cron sözdizimini (cron expression) ve pratik örnekleri detaylıca inceleyeceğiz.

---

## 1. Cron ve Crontab Nedir?

* **Cron:** Linux çekirdeğinde arka planda sürekli çalışan ve zamanı gelen görevleri tetikleyen sistem servisidir (`cron daemon`).
* **Crontab (Cron Table):** Her kullanıcının kendi zamanlanmış görev listesini tanımladığı ve sakladığı konfigürasyon dosyasıdır.

Sisteminizdeki mevcut cron görevlerini listelemek için terminale şu komutu yazabilirsiniz:

```bash
crontab -l
```
Yeni bir görev eklemek veya mevcut görevleri düzenlemek için ise düzenleme modunu açabilirsiniz:

```Bash
crontab -e
```
## 2. Cron Sözdizimi (Cron Expression) Çözümlemesi
Bir crontab satırı, zamanlamayı belirten 5 ana alan ve çalıştırılacak komuttan oluşur. Toplamda 6 parçalı bir yapıya sahiptir:

```Plaintext
* * * * * /yol/to/script.sh
│ │ │ │ │
│ │ │ │ └─── Haftanın Günü (0 - 6) (0 = Pazar veya 7 = Pazar)
│ │ │ └───── Ay (1 - 12)
│ │ └─────── Ayın Günü (1 - 31)
│ └───────── Saat (0 - 23)
└─────────── Dakika (0 - 59)
```
Özel Karakterlerin Anlamları:
* (Yıldız): Her anlamına gelir (Örn: Dakika kısmındaki * her dakika demektir).

, (Virgül): Birden fazla spesifik değer belirtmek için kullanılır (Örn: 0,15,30,45).

- (Tire): Aralık belirtmek için kullanılır (Örn: 9-17 vardiya saatleri arası).

/ (Bölü): Periyot (adım) belirtmek için kullanılır (Örn: */10 her 10 dakikada bir).

## 3. Pratik Senaryolar ve Örnek Cron Tanımları
Gerçek hayatta en sık kullanılan bazı zamanlama senaryoları ve karşılık gelen cron ifadeleri şunlardır:

Örnek 1: Her Gün Gece Yarısı Veritabanı Yedeği
Her gün saat 00:00'da (gece yarısı) çalışan bir yedekleme betiği:

```Bash
0 0 * * * /usr/local/bin/db_backup.sh > /var/log/backup.log 2>&1
```
Örnek 2: Her 15 Dakikada Bir API Kontrolü
Sunucunun ayakta olup olmadığını kontrol eden bir betiği her 15 dakikada bir çalıştırmak için:

```Bash
*/15 * * * * /usr/bin/python3 /var/www/scripts/health_check.py
```
Örnek 3: Her Pazartesi Sabahı Saat 08:30'da Rapor Gönderimi
Haftalık raporlama betiğini sadece pazartesi günleri sabah 08:30'da tetiklemek için:

```Bash
30 8 * * 1 /usr/bin/node /var/www/app/jobs/weekly_report.js
```
## 4. Cron Loglama ve Hata Ayıklama (Debugging)
Cron görevleri arka planda çalıştığı için ekranda doğrudan hata mesajı görmezsiniz. Eğer betiğiniz çalışmıyorsa sorun gidermek zor olabilir.

Çıktıları Dosyaya Yönlendirin: Komutlarınızın standart çıktılarını (stdout) ve hata çıktılarını (stderr) bir log dosyasına yönlendirmek her zaman en iyi pratiktir (> /path/to/logfile.log 2>&1).

Sistem Loglarını İnceleyin: Cron servisinin çalışıp çalışmadığını ve tetiklenme anlarını sistem loglarından takip edebilirsiniz:

```Bash
grep CRON /var/log/syslog
```
## 5. En İyi Pratikler (Best Practices)
Mutlak Yollar (Absolute Paths) Kullanın: Cron ortamındaki çevresel değişkenler (PATH) normal terminalinizden farklı olabilir. Bu nedenle komutlarda ve dosya yollarında kısaltma (~/script.sh) yerine tam yolları (/home/kullanici/script.sh) kullanın.

Çalıştırma İzinlerini Kontrol Edin: Cron tarafından çalıştırılacak .sh veya .py dosyalarının yürütme (chmod +x) yetkisine sahip olduğundan emin olun.

Zaman Dilimine (Timezone) Dikkat Edin: Sunucunuzun yerel saat dilimi (UTC veya Europe/Istanbul) cron tetiklenme saatlerini doğrudan etkiler. Sunucu saatini her zaman kontrol edin.

Sonuç
Cron job, sunucu otomasyonunun kalbidir. Zamanlama mantığını doğru kurarak ve loglamayı unutmayarak kritik operasyonlarınızı güvenle otomatikleştirebilirsiniz.

Bir sonraki yazımızda görüşmek üzere!
