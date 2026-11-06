---
layout: post
title: "Caching (Önbellekleme) Stratejileri: Web Uygulamalarında Hız ve Performans"
date: 2026-08-02 10:00:00 +0300
categories: [performans]
tags: [caching, web-performansi, redis, optimizasyon, mimari]
excerpt: "Web uygulamalarında sunucu yükünü azaltan ve sayfa yüklenme sürelerini milisaniyelere düşüren caching stratejileri rehberi."
---

Yazılım geliştirme dünyasında kullanıcıların en büyük tahammülsüzlüğü yavaş açılan sayfalardır. Bir web sitesi veya API yanıtı 2-3 saniyeden uzun sürdüğünde kullanıcıların büyük kısmı siteyi terk eder. Sunucu kaynaklarını optimize etmek ve yanıt sürelerini hızlandırmak için kullanılan en güçlü mimari yaklaşım **Caching (Önbellekleme)** mekanizmasıdır.

Bu yazımızda önbelleklemenin temel mantığını, farklı caching katmanlarını, stratejileri ve dikkat edilmesi gereken noktaları inceleyeceğiz.

---

## 1. Caching Nedir ve Neden Hayatidir?

Önbellekleme, maliyetli veya uzun süren işlemlerin (örneğin devasa bir veritabanı sorgusu veya uzak bir API isteği) sonuçlarını geçici olarak hızlı erişilebilir bir bellekte (RAM veya hızlı diskler) saklama işlemidir.

* **Performans Artışı:** Veriler doğrudan bellekten çekildiği için milisaniyeler içinde yanıt alınır.
* **Sunucu Yükünün Azalması:** Aynı veri için binlerce kez veritabanına sorgu atmak yerine önbellekten servis edilir, böylece CPU ve disk I/O yükü minimuma iner.

---

## 2. Temel Önbellekleme Katmanları

Modern web mimarilerinde caching genellikle birden fazla katmanda uygulanır:

### Tarayıcı Önbelleği (Browser Caching)
Statik dosyaların (görseller, CSS, JavaScript dosyaları) kullanıcının tarayıcısında belirli bir süre (`Cache-Control` başlıkları aracılığıyla) saklanmasını sağlar. Kullanıcı siteyi tekrar ziyaret ettiğinde bu dosyalar sunucudan yeniden indirilmez.

### CDN Önbelleği (Content Delivery Network)
Cloudflare, AWS CloudFront gibi dağıtık ağlar sayesinde statik içerikler kullanıcılara coğrafi olarak en yakın sunucudan servis edilir.

### Sunucu Tarafı Önbelleği (In-Memory Caching)
Veritabanı sorgularının sonuçlarını veya sık kullanılan verileri **Redis** veya **Memcached** gibi bellek içi (in-memory) veri depolarında saklama yöntemidir.

---

## 3. Popüler Önbellekleme Stratejileri

Uygulamanızın gereksinimlerine göre farklı caching stratejileri seçebilirsiniz:

### 1. Cache-Aside (Lazy Loading) Stratejisi
En yaygın kullanılan yöntemdir. Uygulama önce önbelleğe (`Redis`) bakar:
* Eğer veri önbellekte varsa (`Cache Hit`) doğrudan döndürülür.
* Veri yoksa (`Cache Miss`) veritabanından sorgulanır, bulunan sonuç önbelleğe kaydedilir ve kullanıcıya sunulur.

### 2. Write-Through Stratejisi
Veri güncellendiğinde veya sisteme yeni veri eklendiğinde, hem veritabanı hem de önbellek eş zamanlı olarak güncellenir. Bu sayede önbellekte asla bayat (stale) veri kalmaz.

---

## 4. Önbellekleme Yaparken Dikkat Edilmesi Gerekenler

* **Cache Invalidation (Önbellek Geçersiz Kılma):** "Bilgisayar bilimindeki en zor iki şey: Önbellek geçersiz kılma ve isimlendirme." Veri veritabanında güncellendiğinde, eski önbellek verisinin temizlenmesi (`evict` veya `invalidate`) veya yenilenmesi gerekir; aksi takdirde kullanıcılar güncel olmayan eski verileri görürler.
* **TTL (Time to Live) Belirleme:** Önbellekte tutulan verilerin ne kadar süreyle saklanacağını belirleyen bir yaşam süresi mutlaka tanımlanmalıdır.

---

## Sonuç

Doğru kurgulanmış bir caching stratejisi, web uygulamalarının ölçeklenebilirliğini ve kullanıcı deneyimini doğrudan yukarı taşıyan en kritik mimari yatırımdır.

Bir sonraki yazımızda görüşmek üzere!
