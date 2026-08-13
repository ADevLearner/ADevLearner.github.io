---
title: "REST API Tasarlarken Dikkat Edilmesi Gereken 5 Nokta"
date: 2026-08-05
categories:
  - backend
tags:
  - api
  - rest
excerpt: "Sürdürülebilir ve okunabilir bir REST API tasarlamanın pratik kuralları."
---

İyi tasarlanmış bir REST API, hem geliştirici deneyimini hem de bakım maliyetini doğrudan
etkiler. İşte proje büyüdükçe fark yaratan birkaç kural.

## 1. Kaynak İsimlendirmede Tutarlı Olun

Endpoint'leri her zaman çoğul isimlerle kurun: `/users`, `/orders/123/items` gibi. Fiil
kullanmaktan kaçının; işlem türünü HTTP metodu zaten belirtir.

## 2. HTTP Durum Kodlarını Doğru Kullanın

- `200` — başarılı GET/PUT
- `201` — başarılı POST (yeni kaynak oluşturuldu)
- `204` — başarılı ama gövde dönmeyen işlem (örn. DELETE)
- `400` — istemci hatası (geçersiz veri)
- `404` — kaynak bulunamadı

## 3. Versiyonlama Stratejinizi Baştan Belirleyin

`/v1/users` gibi URL tabanlı versiyonlama basit ve yaygın bir yaklaşımdır. Header tabanlı
versiyonlama daha "temiz" sayılsa da debug etmesi daha zordur.

## 4. Sayfalama (Pagination) Zorunlu Olmalı

Büyük veri setlerini tek seferde dönmek performans sorunlarına yol açar:

```
GET /orders?page=2&limit=50
```

## 5. Hata Mesajlarını Standartlaştırın

Tutarlı bir hata formatı istemci tarafındaki hata yönetimini kolaylaştırır:

```json
{
  "error": {
    "code": "INVALID_INPUT",
    "message": "email alanı zorunludur"
  }
}
```

Bu kurallar küçük görünse de, API büyüdükçe tutarsızlıklar teknik borç olarak birikir.
