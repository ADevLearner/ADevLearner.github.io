---
layout: post
title: "Veritabanı İndeksleme (Indexing) Nedir? Performansı Artırma Rehberi"
date: 2026-07-18 10:00:00 +0300
categories: [veritabani]
tags: [sql, indeksleme, performans, optimizasyon, b-tree]
excerpt: "Milyonlarca satırlık tablolarda sorgu sürelerini milisaniyelere indiren veritabanı indeksleme mantığı, türleri ve dikkat edilmesi gerekenler."
---

Yazılım projelerinde veri hacmi arttıkça, veritabanı sorgularının çalışma süreleri de doğru orantılı olarak uzamaya başlar. Küçük projelerde fark edilmeyen yavaşlıklar, binlerce veya milyonlarca kullanıcıya hizmet veren sistemlerde ciddi performans darboğazlarına (bottleneck) yol açar. Bu tür yavaşlıkları çözmek için kullanılan en temel ve etkili mekanizma **Veritabanı İndekslemedir (Database Indexing)**.

Bu yazımızda, indekslerin çalışma mantığını, en yaygın indeks türlerini, performans avantajlarını ve yanlış indeks kullanımının getirdiği dezavantajları detaylıca inceleyeceğiz.

---

## 1. İndeks Nedir ve Nasıl Çalışır?

Bir veritabanı tablosunda indeks bulunmadığında, veritabanı motoru (`DBMS`) aradığınız veriyi bulabilmek için tablodaki **her bir satırı tek tek taramak** zorundadır. Buna **Full Table Scan (Tam Tablo Taraması)** denir. Tabloda 10 milyon satır varsa, aradığınız kayıt en sonda veya hiç yoksa bile veritabanı milyonlarca satırı okumak zorunda kalır.

**İndeks (Index):** Kitapların arkasındaki "Dizin" veya "Fihrist" sayfalarına benzer. Aradığınız kelimenin veya verinin hangi sayfada / satırda olduğunu tek tek sayfaları çevirerek değil, doğrudan fihristten bularak saniyeler içinde erişmenizi sağlar.

---

## 2. Yaygın İndeks Türleri

Veritabanı yönetim sistemleri (MySQL, PostgreSQL vb.) farklı senaryolar için çeşitli indeks yapıları sunar:

### B-Tree İndeks (En Yaygın Tür)
Varsayılan olarak oluşturulan indeks türüdür. Verileri dengeli bir ağaç yapısında (`Balanced Tree`) saklar. Eşitlik (`=`), büyüktür (`>`), küçüktür (`<`) ve `LIKE 'kelime%'` tarzı sorgularda olağanüstü performans gösterir.

### Unique Index (Benzersiz İndeks)
Bir sütundaki değerlerin tekrarlanamayacağını garantiler (Örn: `e-posta` veya `TC kimlik numarası`). Hem veri bütünlüğünü korur hem de arama hızını artırır.

### Composite Index (Çoklu Sütun İndeksi)
Birden fazla sütunun birlikte sorgulandığı senaryolar için birden fazla sütunu kapsayan indekslerdir (Örn: `WHERE sehir = 'İstanbul' AND yas > 25`).

---

## 3. Pratik Senaryo ve Örnek Kullanım

Milyonlarca kullanıcının bulunduğu bir `kullanicilar` tablomuz olduğunu ve e-posta adresine göre sık sık arama yaptığımızı varsayalım:

```sql
-- İndeks olmaksızın yapılan sorgu (Büyük tablolarda çok yavaştır)
SELECT * FROM kullanicilar WHERE email = 'ornek@domain.com';
```
Bu sorguyu milisaniyeler mertebesine indirmek için ilgili sütuna indeks ekleyebiliriz:

```SQL
-- Email sütunu üzerine B-Tree indeks tanımlama
CREATE INDEX idx_kullanici_email ON kullanicilar(email);
```
Bu işlemden sonra veritabanı motoru Full Table Scan yerine doğrudan indeks ağacını kullanarak aradığınız kayda nokta atışı erişir.

## 4. İndekslerin Karanlık Yüzü: Maliyetler ve Dezavantajlar
"Her sütuna indeks ekleyelim, her şey uçsun" yaklaşımı veritabanı yönetiminde yapılan en büyük hatalardan biridir. İndekslerin de bir maliyeti vardır:

Yazma Performansını Düşürür: Tabloya yeni bir kayıt eklediğinizde (INSERT), veriler güncellendiğinde (UPDATE) veya silindiğinde (DELETE), sadece ana tablo değil, o tablodaki tüm indeksler de yeniden güncellenmek zorundadır. Çok fazla indeks, yazma işlemlerini yavaşlatır.

Disk Alanı Tüketimi: İndeksler disk üzerinde ek veritabanı dosyaları olarak saklanır ve büyük tablolarda ciddi oranda ek depolama alanı kaplar.

## 5. En İyi Pratikler (Best Practices)
Sık Sorgulanan Sütunları Hedefleyin: Sadece WHERE, JOIN koşullarında ve ORDER BY sıralamalarında sıklıkla kullandığınız sütunlara indeks ekleyin.

Kullanılmayan İndeksleri Temizleyin: Zamanla güncelliğini yitirmiş veya hiçbir sorguda kullanılmayan indeksler (Unused Indexes) sistemi sadece yorar; periyodik olarak tespit edilip silinmelidir.

Küçük Tablolardan Kaçının: Yüz veya bin satırlık küçük tablolarda indeks oluşturmanın performansa neredeyse hiçbir katkısı yoktur; veritabanı motoru zaten o veriyi bellekte tek hamlede okuyabilir.

Sonuç
Veritabanı indeksleme, doğru tasarlandığında uygulamaların performansını adeta uçuran kritik bir optimizasyon aracıdır. Okuma yoğunluklu sistemlerde hayat kurtarırken, yazma maliyetleri göz önünde bulundurularak dengeli tasarlanmalıdır.

Bir sonraki yazımızda görüşmek üzere!
