---
title: "Okunaklı Kod Yazmanın Hız Kazandırdığı Anlar"
date: 2026-08-10
categories:
  - yazılım-pratikleri
tags:
  - clean-code
  - okunabilirlik
excerpt: "Kısa vadede zaman kaybı gibi görünen okunabilir kod alışkanlıklarının uzun vadede kazandırdıkları."
---

Bir fonksiyonu yazarken harcanan ekstra 2 dakika, altı ay sonra o kodu tekrar
anlamaya çalışırken saatler kazandırabilir.

## İsimlendirme Küçük Bir Detay Değildir

`d`, `tmp`, `data2` gibi isimler yazarken hızlı gelir ama okuyan kişi (genelde
gelecekteki siz) bu isimlerin ne anlama geldiğini tekrar çözmek zorunda kalır.
`kullaniciListesi`, `siparisToplami` gibi açıklayıcı isimler tercih edin.

## Fonksiyonları Küçük Tutun

Bir fonksiyon birden fazla iş yapıyorsa, muhtemelen ikiye bölünmeyi hak ediyordur.
Tek bir sorumluluğu olan fonksiyonlar hem test etmesi hem de anlaması daha kolaydır.

## Yorum Yerine Açık Kod

Karmaşık bir satırı açıklamak için yorum eklemek yerine, önce o satırı daha basit
yazmayı deneyin. Yorumlar zamanla kodla senkronizasyonunu kaybedebilir; kodun kendisi
asla yalan söylemez.

## Sonuç

Okunabilirlik, "güzel görünsün" kaygısından ibaret değil — takım halinde çalışırken
gerçek bir üretkenlik meselesi.
