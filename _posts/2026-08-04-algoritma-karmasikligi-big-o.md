---
title: "Big O Notasyonu: Algoritma Karmaşıklığını Anlamak"
date: 2026-08-04
categories:
  - programlama
tags:
  - algoritma
  - big-o
excerpt: "Kodunuzun veri büyüdükçe nasıl yavaşlayacağını tahmin etmenin standart yolu."
---

Big O notasyonu, bir algoritmanın girdi büyüdükçe ne kadar yavaşlayacağını
tanımlayan bir gösterimdir. Kesin çalışma süresini değil, büyüme eğilimini
ifade eder.

## O(1) — Sabit Zaman

Girdi boyutundan bağımsız, her zaman aynı sürede çalışır:

```javascript
function ilkEleman(dizi) {
  return dizi[0];
}
```

## O(n) — Doğrusal Zaman

Girdi büyüdükçe süre orantılı olarak artar:

```javascript
function topla(dizi) {
  let toplam = 0;
  for (const eleman of dizi) toplam += eleman;
  return toplam;
}
```

## O(n²) — Karesel Zaman

İç içe döngülerde sıkça karşılaşılır, girdi büyüdükçe süre çok hızlı artar:

```javascript
function tekrarEdenVarMi(dizi) {
  for (let i = 0; i < dizi.length; i++) {
    for (let j = i + 1; j < dizi.length; j++) {
      if (dizi[i] === dizi[j]) return true;
    }
  }
  return false;
}
```

1000 elemanlı bir dizide bu yaklaşık 500.000 karşılaştırma yapar; 10.000 elemanlı
bir dizide bu sayı 50 milyona çıkar.

## O(log n) — Logaritmik Zaman

Binary search gibi, her adımda arama alanını yarıya indiren algoritmalar bu
kategoriye girer. 1 milyon elemanlı bir dizide bile yalnızca ~20 adımda sonuca
ulaşılır — bu yüzden sıralı verilerde arama yaparken binary search, doğrusal
aramaya göre büyük fark yaratır.

## Neden Önemli?

Küçük veri setlerinde O(n²) bir algoritma fark yaratmayabilir, ama veri
büyüdükçe (binlerce, milyonlarca kayıt) yanlış algoritma seçimi uygulamanızı
kullanılamaz hale getirebilir. Big O, kod yazarken "bu ölçeklenir mi?" sorusunu
sormaya teşvik eder.
