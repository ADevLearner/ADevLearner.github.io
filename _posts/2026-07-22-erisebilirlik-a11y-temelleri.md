---
title: "Web Erişilebilirliği (a11y) Neden Görmezden Gelinmemeli?"
date: 2026-07-22
categories:
  - frontend
tags:
  - erisilebilirlik
  - a11y
excerpt: "Ekran okuyucu kullanan ziyaretçiler için basit ama etkili erişilebilirlik pratikleri."
---

Erişilebilirlik (accessibility, kısaca a11y), görme, işitme veya motor engeli
olan kullanıcıların da sitenizi kullanabilmesini sağlayan pratiklerin bütünüdür.
Genelde son dakikaya bırakılır, ama baştan düşünülürse eklemesi çok zor değildir.

## Anlamlı HTML Kullanın

`<div onclick="...">` yerine `<button>` kullanmak, ekran okuyucuların elementin
tıklanabilir olduğunu otomatik anlamasını sağlar. Semantik etiketler (`<nav>`,
`<main>`, `<article>`) sayfanın yapısını hem tarayıcıya hem de yardımcı
teknolojilere netleştirir.

## Görsellerde alt Metni

```html
<img src="grafik.png" alt="2026 yılı satış artışını gösteren çizgi grafik">
```

`alt` metni boş bırakılırsa ekran okuyucu kullanıcısı görselin ne içerdiğini
anlayamaz. Sadece dekoratif görsellerde `alt=""` (boş) bırakmak doğrudur, `alt`
etiketini tamamen atlamak değil.

## Klavye ile Gezinme

Bir siteyi sadece Tab tuşuyla gezmeyi deneyin. Tüm interaktif elementlere
(butonlar, linkler, formlar) klavye ile ulaşılabiliyor mu? Odaklanan elemanın
görsel olarak belirgin olması (focus outline'ı kaldırmamak) da bu konunun önemli
bir parçasıdır.

## Renk Kontrastı

Metin ve arka plan rengi arasındaki kontrast yetersizse, düşük görme keskinliğine
sahip kullanıcılar içeriği okuyamaz. WCAG standardı normal metin için en az 4.5:1
kontrast oranı öneriyor; bunu Chrome DevTools'un renk seçici aracıyla kolayca
kontrol edebilirsiniz.

## Neden Önemli?

Erişilebilirlik sadece etik bir sorumluluk değil — birçok ülkede yasal bir
gereklilik ve aynı zamanda SEO'yu da olumlu etkileyen bir pratiktir.
