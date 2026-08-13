---
title: "Ortam Değişkenlerini (Environment Variables) Doğru Yönetmek"
date: 2026-07-12
categories:
  - devops
tags:
  - env
  - guvenlik
excerpt: "API anahtarları ve gizli bilgileri kod içine gömmeden yönetmenin standart yolları."
---

API anahtarı, veritabanı şifresi gibi hassas bilgileri doğrudan kod içine yazmak
en yaygın güvenlik hatalarından biridir. Ortam değişkenleri bu sorunu çözer.

## Neden Kod İçine Yazmamalı?

Kod bir GitHub reposuna push edildiğinde, içindeki her şey (özellikle geçmişteki
commit'ler) potansiyel olarak herkese açık hale gelebilir. Bir şifre bir kez
commit edilirse, sonradan silinse bile git geçmişinde kalır.

## .env Dosyası Kullanımı

```bash
# .env dosyası
DATABASE_URL=postgres://kullanici:sifre@localhost:5432/db
API_KEY=gizli_anahtar_buraya
```

Bu dosya proje koduyla birlikte push edilmemeli — `.gitignore` dosyasına
`.env` satırını eklemek ilk yapılması gereken şey.

```bash
# .gitignore
.env
```

## Kod İçinde Kullanım (Node.js örneği)

```javascript
require('dotenv').config();
const apiKey = process.env.API_KEY;
```

## Production Ortamında

Yerel geliştirmede `.env` dosyası kullanılsa da, production ortamında bu değerler
genelde hosting sağlayıcının (Vercel, Heroku, AWS vb.) panel üzerinden ayarlanan
ortam değişkenleri aracılığıyla enjekte edilir — dosya olarak sunucuya hiç
yüklenmez.

## Ekstra Güvenlik

Takım halinde çalışıyorsanız `.env.example` adında, gerçek değerler olmadan
sadece hangi değişkenlerin gerektiğini gösteren bir örnek dosya bırakmak yeni
katılan geliştiriciler için faydalıdır.
