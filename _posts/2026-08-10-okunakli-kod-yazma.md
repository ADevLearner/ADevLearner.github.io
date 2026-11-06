---
layout: single
title: "Temiz Kod (Clean Code) İlkeleri: Okunabilir ve Sürdürülebilir Kod Nasıl Yazılır?"
date: 2026-08-10 10:00:00 +0300
categories: [gelistirme]
tags: [clean-code, yazilim-kalitesi, refaktoring, best-practices, kod-kalitesi]
excerpt: "Yazılım geliştirme sürecinde sadece çalışan değil, aynı zamanda başkaları tarafından kolayca okunabilen ve bakımı yapılabilen temiz kod yazma rehberi."
---

Yazılım dünyasında sıklıkla karşılaşılan popüler bir söz vardır: *"Kodunuzu sadece bilgisayarın anlaması için değil, aynı zamanda başka insanların (ve gelecekteki kendinizin) okuyabilmesi için yazın."* Çalışan bir kod her zaman iyi bir kod anlamına gelmez. Hatalarla dolu, karmaşık ve okunması imkansız bir kod tabanı kısa vadede işinizi görse de uzun vadede projeyi çıkmaza sokar.

Robert C. Martin (Uncle Bob) tarafından popülerleştirilen **Clean Code (Temiz Kod)** felsefesi, yazılımın sürdürülebilirliğini ve kalitesini belirleyen en temel kılavuzdur. Bu yazımızda, okunabilir ve temiz kod yazmanın altın kurallarını inceleyeceğiz.

---

## 1. Anlamlı ve Açıklayıcı İsimlendirme (Naming Conventions)

Kod yazarken en çok zorlanılan ve en çok hata yapılan konuların başında değişken, fonksiyon ve sınıf isimleri gelir. 

* **Tek Harfli İsimlerden Kaçının:** `a`, `x`, `d` gibi hiçbir şey ifade etmeyen değişken isimleri yerine `kullaniciYasi`, `toplamTutar` gibi açıklayıcı isimler kullanın.
* **Bool İsimlendirmeleri:** Mantıksal (`boolean`) değer tutan değişkenlerin başına `is`, `has`, `can` gibi önekler koyun (Örn: `aktifMi`, `yetkisiVarMi`).
* **Fonksiyon İsimleri Eylem Bildirmeli:** Fonksiyonlar ne iş yapıyorsa onu açıkça belirtmelidir. Örneğin `kullaniciVerisi()` yerine `kullaniciyiGetir()` veya `fiyatHesapla()` isimleri tercih edilmelidir.

---

## 2. Küçük ve Odaklı Fonksiyonlar (Single Responsibility)

Temiz kodun en temel kuralı, fonksiyonların **sadece tek bir iş yapması** ve bunu kusursuz şekilde yerine getirmesidir.

* **Uzun Fonksiyonlardan Kaçının:** Onlarca satır süren, içinde iç içe döngüler barındıran devasa fonksiyonların okunması ve testi çok zordur. Fonksiyonunuz ekrana sığacak kadar kısa olmalıdır (genellikle 10-20 satırı geçmemelidir).
* **DRY (Don't Repeat Yourself) Prensibi:** Aynı kod bloğunu projenin farklı yerlerinde tekrar tekrar yazmak yerine, o mantığı ortak bir yardımcı fonksiyona (`helper`) taşıyın.

---

## 3. Yorum Satırı Kullanımında Denge

Yazılımcılar arasında "Yorum satırı ne kadar çoksa kod o kadar kalitelidir" şeklinde yanlış bir algı vardır. Aslında tam tersi geçerlidir:

* **Kötü Kodu Yorumla Temizleyemezsiniz:** Kötü yazılmış, anlaşılması güç bir kodu yorum satırlarıyla açıklamaya çalışmak yerine, **kodu daha okunabilir hale getirin**.
* Kodunuz zaten kendisini ifade ediyorsa (self-documenting code), ekstra yorum satırına ihtiyaç duymazsınız. Yorum satırlarını sadece "neden" böyle bir çözüm yapıldığını (iş kuralını) açıklamak için kullanın.

---

## Sonuç

Temiz kod yazmak bir günde kazanılan bir alışkanlık değildir; aksine bilinçli bir çaba ve sürekli pratik gerektiren bir zihniyettir. Okunabilir kod yazmak, hem ekip arkadaşlarınızın hem de gelecekteki sizin hayatını kurtaracaktır.

Bir sonraki yazımızda görüşmek üzere!
