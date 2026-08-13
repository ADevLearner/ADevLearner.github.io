---
title: "Veritabanı İndeksleme Nasıl Çalışır ve Ne Zaman Kullanılmalı?"
date: 2026-07-18
categories:
  - veritabani
tags:
  - performans
  - index
excerpt: "Index'lerin sorgu hızını nasıl artırdığı ve gereksiz index'lerin neden zararlı olabileceği."
---

Büyüyen bir tabloda sorgular yavaşlamaya başladığında akla ilk gelen çözüm genelde
index eklemektir. Ama index'in nasıl çalıştığını anlamadan eklemek bazen sorunu
çözmek yerine büyütür.

## Index Ne İşe Yarar?

Index'siz bir tabloda arama yapmak, alfabetik olmayan bir kitabı sayfa sayfa
tarayarak bir kelime aramaya benzer. Index eklendiğinde veritabanı, aranan
sütuna göre önceden sıralanmış bir yapı (genelde B-Tree) tutar, arama süresi
büyük ölçüde kısalır.

```sql
CREATE INDEX idx_musteri_email ON musteriler(email);
```

Bu komuttan sonra `WHERE email = '...'` şeklindeki sorgular çok daha hızlı çalışır.

## Ne Zaman Index Eklemeli?

- `WHERE`, `JOIN` ve `ORDER BY` ifadelerinde sık kullanılan sütunlar
- Benzersizliği yüksek sütunlar (email, kullanıcı adı gibi) — düşük çeşitlilikteki
  sütunlarda (örn. `cinsiyet` gibi 2-3 değer alan sütunlar) index faydası azdır

## Index'in Bedeli

Her index, yazma (INSERT/UPDATE/DELETE) işlemlerini yavaşlatır çünkü veritabanı her
değişiklikte index yapısını da güncellemek zorundadır. Çok fazla index eklemek,
okuma performansını artırırken yazma performansını ciddi şekilde düşürebilir.

## Pratik Tavsiye

Her sütuna index eklemek yerine, uygulamanızın en sık çalıştırdığı sorguları
tespit edip (yavaş sorgu logları buna yardımcı olur) sadece o sorgularda
kullanılan sütunlara index eklemek daha dengeli bir yaklaşımdır.
