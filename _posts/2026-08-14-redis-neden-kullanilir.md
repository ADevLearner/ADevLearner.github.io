---
layout: post
title: "Redis Nedir ve Neden Kullanılır? Bellek İçi Veri Depolama Rehberi"
date: 2026-08-14 10:00:00 +0300
categories: [backend]
tags: [redis, caching, veritabani, performans, backend]
excerpt: "Modern web mimarilerinin vazgeçilmezi olan Redis'in ne olduğunu, geleneksel veritabanlarından farkını ve hangi senaryolarda hayat kurtardığını keşfedin."
---

Yazılım projelerinde veri hacmi ve eş zamanlı kullanıcı sayısı arttıkça, geleneksel ilişkisel veritabanları (MySQL, PostgreSQL vb.) disk tabanlı yapıları nedeniyle yavaşlamaya başlar. Her istekte karmaşık SQL sorguları çalıştırmak ve diske gitmek ciddi bir performans darboğazı yaratır. Bu tür performans sorunlarını kökten çözmek için modern mimarilerde **Redis** gibi bellek içi (`in-memory`) veri yapıları devreye girer.

Bu yazımızda Redis'in çalışma mantığını, geleneksel veritabanlarından farkını ve projelerinizde hangi amaçlarla kullanabileceğinizi inceleyeceğiz.

---

## 1. Redis Nedir?

**Redis** (Remote Dictionary Server), açık kaynaklı, verileri disk üzerinde değil doğrudan **RAM (bellek)** üzerinde saklayan ve bu sayede milisaniyenin altında (`sub-millisecond`) yanıt süreleri sunan bir NoSQL anahtar-değer (`key-value`) veri tabanıdır.

* **Neden Bu Kadar Hızlıdır?** Veriler RAM'de tutulduğu için disk okuma/yazma gecikmeleri ortadan kalkar ve saniyede milyonlarca isteği kolayca karşılayabilir.

---

## 2. Redis Hangi Senaryolarda Kullanılır?

Redis sadece basit bir önbellek (`cache`) aracı değil, aynı zamanda çok yönlü bir veri yapısı sunucusudur:

### 1. Caching (Önbellekleme)
En yaygın kullanım alanıdır. Sık erişilen ancak nadir değişen veritabanı sorgu sonuçları (örneğin ana sayfadaki popüler ürünler listesi) Redis'te saklanır. İstek geldiğinde veritabanına hiç gidilmeden doğrudan Redis'ten anında servis edilir.

### 2. Session Yönetimi (Oturum Yönetimi)
Kullanıcıların web sitenizde oturum açtıklarında sisteme giriş yaptıklarını doğrulayan session bilgileri Redis'te tutulur. Bu sayede sunucular arası geçişlerde (load balancer arkasında) kullanıcı oturumu kaybolmaz.

### 3. Rate Limiting (İstek Sınırlandırma)
API'lerinize bir kullanıcının veya IP adresinin dakikada kaç istek atabileceğini sınırlamak (`rate limit`) için Redis'in sayaç (`counter`) ve süre sınırlama (`EXPIRE`) özellikleri mükemmel bir çözüm sunar.

### 4. Real-time Mesajlaşma (Pub/Sub)
Redis, yayıncı/abone (`Publish/Subscribe`) mekanizması sayesinde anlık bildirimler, sohbet uygulamaları ve canlı veri akışları için hızlı bir mesaj kuyruğu görevi görür.

---

## 3. Temel Redis Komutları

Redis ile terminal üzerinden çalışırken en sık kullanılan komutlar şunlardır:

```bash
# Bir anahtara değer atama
SET kullanici:1 "Ahmet Yılmaz"

# Belirli bir sürede (örneğin 60 saniye sonra) silinmesini sağlama
SETEX oturum:123 60 "aktif"

# Bir anahtarın değerini okuma
GET kullanici:1

# Bir anahtarı silme
DEL kullanici:1
```
Sonuç
Redis, doğru senaryolarda kullanıldığında web uygulamalarının yükünü büyük ölçüde hafifleten ve kullanıcı deneyimini zirveye taşıyan kritik bir araçtır.

Bir sonraki yazımızda görüşmek üzere!
