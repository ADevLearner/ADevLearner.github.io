---
title: "Her Geliştiricinin Bilmesi Gereken Linux Terminal Komutları"
date: 2026-07-05
categories:
  - araçlar
tags:
  - linux
  - terminal
excerpt: "Günlük geliştirme iş akışında en çok işe yarayan temel Linux komutlarının özeti."
---

Terminal, ilk bakışta ürkütücü görünse de birkaç komutu öğrendikten sonra grafik
arayüzden çok daha hızlı çalışmanızı sağlar.

## Dosya Sistemi Gezinme

- `pwd` — bulunduğunuz dizini gösterir
- `ls -la` — gizli dosyalar dahil tüm içeriği detaylı listeler
- `cd ..` — bir üst dizine çıkar

## Dosya İşlemleri

```bash
cp kaynak.txt hedef.txt      # kopyala
mv eski.txt yeni.txt          # taşı / yeniden adlandır
rm dosya.txt                  # sil
```

`rm -rf` komutunu özellikle root yetkisiyle kullanırken çok dikkatli olun; geri
alma seçeneği yoktur.

## Metin Arama ve Filtreleme

```bash
grep "hata" log.txt
```

Bu komut, `log.txt` içinde "hata" geçen satırları bulur. `-r` bayrağıyla tüm alt
dizinlerde arama yapabilirsiniz.

## Süreç Yönetimi

```bash
ps aux | grep node
kill -9 <PID>
```

Çalışan bir süreci bulup sonlandırmak için sıkça kullanılan kombinasyon budur.

## Yetki Yönetimi

```bash
chmod +x script.sh
```

Bu komut bir dosyaya çalıştırılabilir izni verir; script dosyalarını çalıştırmadan
önce sık karşılaşacağınız bir adımdır.

Bu komutları ezberlemek yerine sık kullandıkça doğal olarak akılda kalır — önemli
olan `man <komut>` ile her komutun tüm seçeneklerini keşfetmeyi bilmek.
