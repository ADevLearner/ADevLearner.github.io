---
layout: post
title: "Web Güvenliğinde OWASP Top 10 Nedir? En Kritik 5 Güvenlik Açığı"
date: 2026-08-22 10:00:00 +0300
categories: [guvenlik]
tags: [owasp, web-guvenligi, siber-guvenlik, xss, sql-injection]
excerpt: "Web uygulamalarında en sık karşılaşılan ve en tehlikeli güvenlik açıklarını listeleyen OWASP Top 10 rehberini ve korunma yollarını keşfedin."
---

Yazılım geliştirme sürecinde bir uygulamanın hızlı çalışması ve güzel arayüze sahip olması ne kadar önemliyse, siber saldırılara karşı güvenli olması da bir o kadar (hatta daha fazla) hayati önem taşır. Geliştirdiğiniz bir web uygulamasında yaşanan tek bir güvenlik açığı; kullanıcı verilerinin çalınmasına, şirket itibarının zedelenmesine ve ağır yasal yaptırımlara yol açabilir.

Web güvenliği dünyasının standart başvuru kaynağı olan **OWASP (Open Worldwide Application Security Project)**, geliştiriciler için en kritik güvenlik açıklarını sınıflandıran **OWASP Top 10** listesini yayınlar. Bu yazımızda, bu listenin ne anlama geldiğini ve en sık karşılaşılan kritik güvenlik açıklarını nasıl önleyebileceğinizi inceleyeceğiz.

---

## 1. OWASP Top 10 Nedir?

OWASP, web uygulaması güvenliğini artırmak için küresel çapta çalışan kâr amacı gütmeyen bir topluluktur. **OWASP Top 10**, dünya genelinde web uygulamalarında en sık görülen ve en yüksek risk taşıyan 10 güvenlik açığını kategorize eden düzenli olarak güncellenen bir farkındalık belgesidir.

---

## 2. En Sık Karşılaşılan Kritik Güvenlik Açıkları

### 1. Broken Access Control (Yetersiz Erişim Kontrolü)
Kullanıcıların yalnızca kendi yetkileri dahilindeki alanlara erişebilmesi gerekir. Ancak erişim kontrol mekanizmalarındaki açıklar yüzünden sıradan bir kullanıcı, URL değiştirerek (`IDOR` açıkları vb.) başka bir kullanıcının paneline veya yönetici yetkilerine erişebilir.
* **Çözüm:** Her istekte sunucu tarafında rol ve yetki kontrolleri (`authorization middleware`) mutlaka eksiksiz yapılmalıdır.

### 2. Cryptographic Failures (Kriptografik Hatalar)
Hassas verilerin (kullanıcı şifreleri, kredi kartları, kişisel veriler) şifrelenmeden düz metin (`plaintext`) olarak veritabanında saklanması veya zayıf algoritmalarla korunması durumudur.
* **Çözüm:** Şifreler asla düz metin saklanmamalıdır; güçlü hash algoritmaları (`Argon2`, `bcrypt`) ve iletim sırasında `HTTPS` (TLS) kullanılmalıdır.

### 3. Injection (Enjeksiyon - Örn: SQL Injection)
İstemciden (kullanıcıdan) gelen zararlı girdilerin, sunucu tarafından doğrulanmadan doğrudan veritabanı sorgularına veya sistem komutlarına dahil edilmesiyle oluşur. Saldırgan bu sayede tüm veritabanını ele geçirebilir.
* **Çözüm:** Asla kullanıcı girdileri doğrudan SQL sorgularıyla birleştirilmemelidir. Hazırlıklı ifadeler (`Prepared Statements` / `Parameterized Queries`) ve ORM araçları kullanılmalıdır.

### 4. Cross-Site Scripting - XSS (Siteler Arası Kod Çalıştırma)
Saldırganın, uygulamanın kullanıcıya gösterdiği sayfalara kötü niyetli JavaScript kodları enjekte etmesidir. Kullanıcı sayfayı açtığında bu kod tarayıcısında çalışır ve çerezleri (`cookies`) çalabilir.
* **Çözüm:** Kullanıcıdan gelen tüm girdiler sunucu tarafında filtrelenmeli (`sanitize`) ve HTML çıktısı verilirken uygun şekilde kodlanmalıdır (`escaping`).

### 5. Security Misconfiguration (Güvenlik Yapılandırma Hataları)
Varsayılan şifrelerin değiştirilmemesi, gereksiz servislerin açık bırakılması, hata ayıklama (`debug`) modunun canlıda açık unutulması ve ayrıntılı hata mesajlarının kullanıcıya gösterilmesi bu kategoriye girer.
* **Çözüm:** Sunucu ve framework yapılandırmaları sıkılaştırılmalı (`hardening`), canlı ortamda detaylı hata logları kullanıcıya gösterilmemelidir.

---

## Sonuç

Web güvenliği bir özellik (feature) değil, sürekli dikkat edilmesi gereken bir süreçtir. OWASP Top 10 prensiplerini bilmek ve kod yazarken bu kuralları göz önünde bulundurmak, uygulamalarınızı siber saldırılara karşı güvenli bir kaleye dönüştürür.

Bir sonraki yazımızda görüşmek üzere!
