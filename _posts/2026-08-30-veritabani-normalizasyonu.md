---
layout: single
title: "Veritabanı Normalizasyonu Nedir? 1NF, 2NF ve 3NF Kuralları"
date: 2026-08-30 10:00:00 +0300
categories: [veritabani]
tags: [sql, normalizasyon, veritabani-tasarimi, bdw, backend]
excerpt: "İlişkisel veritabanlarında veri tekrarını önlemek, veri bütünlüğünü sağlamak ve performansı artırmak için uygulanan normalizasyon kurallarını keşfedin."
---

Yazılım geliştirme süreçlerinde veritabanı tasarımı, sistemin uzun ömürlü ve hatasız çalışmasının temel taşıdır. Geliştirme aşamasında verileri tek bir büyük tablo içine doldurmak ilk başta pratik gelse de zamanla veri tekrarları (`data redundancy`), güncelleme anomalileri ve tutarsızlıklar kaçınılmaz hale gelir.

Veritabanı tasarımında veri tekrarını en aza indirmek ve veri bütünlüğünü (`data integrity`) maksimum seviyeye çıkarmak için uygulanan matematiksel temelli sürece **Veritabanı Normalizasyonu** denir. Bu yazımızda normalizasyonun aşamalarını ve temel kurallarını inceleyeceğiz.

---

## 1. Normalizasyon Nedir ve Neden Gereklidir?

Normalizasyon, ilişkisel veritabanı tablolarının belirli kurallara (`normal forms`) göre daha küçük, mantıksal ve ilişkili alt tablolara bölünmesi işlemidir.

* **Veri Tekrarını Önlemek:** Aynı bilginin farklı satırlarda tekrar saklanarak disk alanı harcamasını ve tutarsızlık yaratmasını engeller.
* **Anomalileri Önlemek:** Veri ekleme (`insert`), güncelleme (`update`) ve silme (`delete`) işlemlerinde yaşanabilecek mantıksal hataları ortadan kaldırır.

---

## 2. Temel Normalizasyon Aşamaları (Normal Forms)

Normalizasyon süreci aşamalı kurallardan oluşur. En yaygın kullanılan ilk üç aşama şunlardır:

### 1. Birinci Normal Form (1NF)
* **Kural:** Tablodaki her bir hücrede sadece **tek bir değer** (atomik değer) yer almalıdır. Bir hücrede virgülle ayrılmış birden fazla değer veya dizi (`array`) bulunamaz.
* **Amaç:** Verilerin sorgulanmasını ve filtrelenmesini standart hale getirmek.

### 2. İkinci Normal Form (2NF)
* **Kural:** Tablo öncelikle 1NF şartını sağlamalıdır. Ek olarak, tablonun birincil anahtarı (`Primary Key`) bileşik anahtarlardan oluşuyorsa, anahtarın tamamına bağlı olmayan kısmi bağımlı sütunlar (`partial dependency`) başka bir tabloya taşınmalıdır.
* **Amaç:** Anahtarın sadece bir kısmına bağlı olan sütunların gereksiz tekrarını önlemek.

### 3. Üçüncü Normal Form (3NF)
* **Kural:** Tablo 2NF şartını sağlamalıdır. Ek olarak, birincil anahtara doğrudan bağlı olmayan, ancak başka bir sütun üzerinden dolaylı olarak bağlı olan sütunlar (`transitive dependency - geçişli bağımlılık`) bulunmamalıdır. Yani ana anahtar haricindeki sütunlar kendi aralarında ilişki barındırmamalıdır.
* **Amaç:** Veritabanındaki tüm sütunların "sadece anahtara, doğrudan anahtara ve başka hiçbir şeye" bağlı olmasını sağlamak.

---

## Sonuç

Veritabanı normalizasyonu, doğru tasarlandığında sistemin güvenilirliğini ve ölçeklenebilirliğini artıran kritik bir mühendislik disiplinidir. Ancak aşırı normalizasyon (`over-normalization`) çok fazla tablo birleşimine (`JOIN`) yol açarak okuma performansını düşürebileceği için projeye göre dengeli tasarlanmalıdır.

Bir sonraki yazımızda görüşmek üzere!
