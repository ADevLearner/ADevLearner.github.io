---
title: "SQL JOIN Çeşitleri: INNER, LEFT, RIGHT ve FULL Farkları"
date: 2026-07-03
categories:
  - veritabani
tags:
  - sql
  - join
excerpt: "Dört temel JOIN türünün ne zaman hangi sonucu döndürdüğünü örneklerle açıklıyoruz."
---

JOIN, ilişkisel veritabanlarında iki veya daha fazla tabloyu birleştirmenin temel
yoludur. Hangi JOIN'in ne zaman kullanılacağını karıştırmak yaygın bir hata kaynağı.

## INNER JOIN

Sadece her iki tabloda da eşleşen kayıtları döndürür.

```sql
SELECT * FROM siparisler
INNER JOIN musteriler ON siparisler.musteri_id = musteriler.id;
```

## LEFT JOIN

Sol tablodaki tüm kayıtları, sağ tabloda eşleşme olmasa bile döndürür. Eşleşme
yoksa sağ tablodan gelen sütunlar NULL olur.

```sql
SELECT * FROM musteriler
LEFT JOIN siparisler ON musteriler.id = siparisler.musteri_id;
```

Bu sorgu, hiç sipariş vermemiş müşterileri de listede tutar.

## RIGHT JOIN

LEFT JOIN'in tam tersi — sağ tablodaki tüm kayıtlar korunur. Pratikte çoğu ekip
LEFT JOIN kullanmayı tercih eder çünkü sorgu okunurken tablo sırası daha sezgisel
kalır.

## FULL JOIN

Her iki taraftaki eşleşmeyen kayıtları da dahil eder. MySQL bunu doğrudan
desteklemez, LEFT JOIN ve RIGHT JOIN'i UNION ile birleştirmek gerekir.

## Pratik İpucu

JOIN yazarken önce hangi tarafın "tüm kayıtları korunmalı" olduğunu düşünün, JOIN
türünü ona göre seçin. Performans sorunu yaşıyorsanız JOIN edilen sütunların index'li
olduğundan emin olun.
