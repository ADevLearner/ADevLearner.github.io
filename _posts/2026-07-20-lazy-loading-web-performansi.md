---
title: "Lazy Loading ile Sayfa Açılış Hızını Artırmak"
date: 2026-07-20
categories:
  - frontend
tags:
  - performans
  - lazy-loading
excerpt: "Görsellerin ve bileşenlerin ihtiyaç anında yüklenmesinin sayfa hızına etkisi."
---

Kullanıcı bir sayfayı açtığında görmediği (henüz kaydırmadığı) içeriği hemen
yüklemek, ilk açılış süresini gereksiz yere uzatır. Lazy loading bu sorunu çözer.

## Görsellerde Lazy Loading

Modern tarayıcılar artık native destek sunuyor:

```html
<img src="foto.jpg" loading="lazy" alt="Açıklama">
```

Bu tek satır, görsel ekranda görünür hale gelene kadar tarayıcının onu yüklemesini
erteler. Ekstra kütüphaneye gerek kalmadan çalışır.

## React'te Bileşen Bazlı Lazy Loading

Büyük bileşenleri (örneğin bir modal veya grafik kütüphanesi) sadece kullanıcı o
kısma ihtiyaç duyduğunda yüklemek mümkün:

```javascript
const AgirBilesen = React.lazy(() => import('./AgirBilesen'));

function App() {
  return (
    <React.Suspense fallback={<div>Yükleniyor...</div>}>
      <AgirBilesen />
    </React.Suspense>
  );
}
```

Bu yaklaşım, ilk yüklenen JavaScript paketinin boyutunu küçültür — kullanıcı
sayfayı ilk açtığında sadece o an gerekli kod indirilir.

## Ne Zaman Kullanmamalı

Sayfanın ilk görünen kısmındaki (above-the-fold) kritik görselleri veya
bileşenleri lazy loading ile geciktirmek, kullanıcının ilk izlenimini kötüleştirir.
Lazy loading, "kullanıcının hemen görmeyeceği" içerik için mantıklıdır, sayfanın
ana içeriği için değil.

## Ölçmeden Optimize Etmeyin

Lighthouse veya Chrome DevTools'un Performance sekmesi, hangi kaynağın gerçekten
yavaşlattığını gösterir. Körlemesine her şeye lazy loading eklemek yerine, önce
ölçüp sonra optimize etmek daha sağlıklı bir yaklaşımdır.
