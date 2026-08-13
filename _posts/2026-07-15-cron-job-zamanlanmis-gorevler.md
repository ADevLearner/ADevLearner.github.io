---
title: "Cron Job ile Zamanlanmış Görevleri Otomatikleştirmek"
date: 2026-07-15
categories:
  - devops
tags:
  - cron
  - otomasyon
excerpt: "Linux sunucularda tekrarlayan görevleri otomatik çalıştırmak için cron sözdiziminin çözümlenmesi."
---

Her gece veritabanı yedeği almak, her saat bir raporu güncellemek gibi tekrarlayan
görevler için cron, Linux dünyasının en köklü çözümüdür.

## Crontab Söz Dizimi

```
* * * * * komut
│ │ │ │ │
│ │ │ │ └── haftanın günü (0-7)
│ │ │ └──── ay (1-12)
│ │ └────── ayın günü (1-31)
│ └──────── saat (0-23)
└────────── dakika (0-59)
```

## Örnekler

Her gece saat 03:00'te çalışacak bir yedekleme scripti:

```
0 3 * * * /home/kullanici/backup.sh
```

Her 15 dakikada bir çalışacak bir kontrol scripti:

```
*/15 * * * * /home/kullanici/check.sh
```

Sadece hafta içi (Pazartesi-Cuma) sabah 9'da çalışacak bir görev:

```
0 9 * * 1-5 /home/kullanici/rapor.sh
```

## Crontab Düzenleme

```bash
crontab -e
```

Bu komut, mevcut kullanıcının cron görevlerini düzenlemenizi sağlayan bir editör
açar. Değişiklikler kaydedildiğinde otomatik olarak aktif olur.

## Yaygın Hatalar

- Script içinde relative path kullanmak — cron farklı bir çalışma dizininden
  başlar, bu yüzden dosya yollarını mutlak (absolute) yazmak daha güvenlidir.
- Ortam değişkenlerinin cron'da farklı davranması — script'in başında gerekli
  ortam değişkenlerini elle export etmek sorunları önler.
- Log tutmamak — `>> /var/log/gorev.log 2>&1` ekleyerek hataları görünür kılmak
  debug sürecini kolaylaştırır.
