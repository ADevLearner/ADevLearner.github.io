---
title: "Caching Stratejileri: Uygulamanızı Nasıl Hızlandırır?"
date: 2026-08-02
categories:
  - backend
tags:
  - cache
  - performans
excerpt: "Farklı önbellekleme katmanlarının ne zaman ve nasıl kullanılacağına dair pratik bir bakış."
---

Caching (önbellekleme), sık istenen ama nadiren değişen verileri tekrar tekrar
hesaplamak yerine hafızada tutmaktır. Doğru uygulandığında performansı ciddi
şekilde artırır, yanlış uygulandığında ise eski/hatalı veri gösterme riski
doğurur.

## Tarayıcı Önbelleği

```
Cache-Control: max-age=86400
```

Bu HTTP header'ı, tarayıcının bir kaynağı (görsel, CSS dosyası vb.) 24 saat
boyunca tekrar sunucudan istemeden yerelden kullanmasını söyler.

## Sunucu Tarafı Önbellek (Redis örneği)

Sık sorgulanan ama nadiren değişen veriler (örneğin bir ürün kataloğu) veritabanı
yerine Redis gibi bellek içi bir veri deposunda tutulabilir:

```javascript
const cached = await redis.get('urunler');
if (cached) return JSON.parse(cached);

const urunler = await db.query('SELECT * FROM urunler');
await redis.set('urunler', JSON.stringify(urunler), 'EX', 3600);
return urunler;
```

## Cache Invalidation Sorunu

Bilgisayar bilimlerinde şaka gibi anlatılan bir söz vardır: "En zor iki şey isim
koymak ve cache invalidation'dır." Veri değiştiğinde eski cache'in ne zaman ve
nasıl temizleneceğini planlamak, caching'in en kritik kısmıdır. Yaygın yaklaşımlar:

- **TTL (Time To Live):** Belirli bir süre sonra cache otomatik geçersiz olur
- **Manuel invalidation:** Veri güncellendiğinde ilgili cache anahtarı elle silinir

## Ne Zaman Cache'lememeli

Sık değişen, kullanıcıya özel (örneğin bakiye bilgisi gibi) veriler için
caching riskli olabilir — yanlış veya eski veri göstermek, performans
kazancından çok daha büyük bir sorun yaratır.
