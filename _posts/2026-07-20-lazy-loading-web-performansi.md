---
layout: post
title: "Web Performansını Uçuran Strateji: Lazy Loading (Tembel Yükleme) Nedir ve Nasıl Uygulanır?"
date: 2026-07-20 10:00:00 +0300
categories: [frontend]
tags: [web-performansi, lazy-loading, optimization, frontend, ux]
excerpt: "Web sitelerinin açılış hızını artıran, bant genişliğinden tasarruf sağlayan Lazy Loading mantığı ve modern tarayıcılarda kullanımı."
---

Günümüz web siteleri; yüksek çözünürlüklü görseller, animasyonlar, gömülü videolar (iframe) ve ağır JavaScript dosyalarıyla doludur. Bir kullanıcı web sitenizi ziyaret ettiğinde, tarayıcı sayfadaki **tüm içeriği aynı anda** indirmeye ve yüklemeye çalışır. Kullanıcı henüz sayfanın en altındaki görselleri görmese bile sunucu o görselleri indirmek için bant genişliği harcar. Bu durum özellikle mobil cihazlarda yavaş açılış sürelerine ve yüksek veri tüketimine yol açar.

Bu performans sorununu kökten çözen modern yaklaşım **Lazy Loading (Tembel Yükleme)** stratejisidir. Bu yazımızda, lazy loading'in mantığını, tarayıcı düzeyindeki yerleşik desteklerini ve web sitenizde nasıl uygulayacağınızı inceleyeceğiz.

---

## 1. Lazy Loading (Tembel Yükleme) Nedir?

Lazy loading, web sayfasındaki kaynakların (görseller, videolar veya bileşenler) tamamının sayfa ilk açıldığında yüklenmesi yerine, **kullanıcı o içeriği ekranında göreceği (viewport içine gireceği) ana kadar yüklenmesini erteleyen** bir optimizasyon tekniğidir.

### Sağladığı Avantajlar:
* **Hızlı İlk Açılış (Initial Load):** Tarayıcı daha az veri indirerek sayfayı çok daha hızlı çizer (`First Contentful Paint`).
* **Bant Genişliği Tasarrufu:** Kullanıcı sayfanın sadece üst kısmında (`above the fold`) kalırsa, alt kısımdaki devasa görseller asla indirilmez; bu da mobil kullanıcılar için veri tasarrufu sağlar.
* **Sunucu Yükünün Azalması:** Eş zamanlı gelen gereksiz istekler (`HTTP requests`) önlenir.

---

## 2. Yerleşik (Native) HTML Lazy Loading

Geçmişte lazy loading uygulamak için karmaşık JavaScript kütüphanelerine (Intersection Observer API vb.) ihtiyaç duyulurdu. Günümüzde ise modern tüm tarayıcılar HTML düzeyinde yerleşik (`native`) destek sunar.

Görsellerinize veya iframe'lerinize ekleyeceğiniz basit bir **`loading="lazy"`** niteliği bu işi otomatik olarak yapar:

```html
<!-- Sayfa ilk açıldığında yüklenmez, kullanıcı kaydırdıkça yüklenir -->
<img src="yuksek-cozunurluklu-foto.jpg" alt="Manzara Fotoğrafı" loading="lazy" width="800" height="600" />

<!-- YouTube videoları veya haritalar için de kullanılabilir -->
<iframe src="[https://www.youtube.com/embed/ornek-video](https://www.youtube.com/embed/ornek-video)" loading="lazy"></iframe>
```
Yükleme Stratejileri:
loading="lazy": Görsel görüntü alanına yaklaşırken yüklenir.

loading="eager": (Varsayılan değer) Görsel neredeyse sayfa açılır açılmaz anında indirilir.

## 3. JavaScript ile Gelişmiş Kontroller (Intersection Observer API)
Eğer yerleşik tarayıcı desteğinden daha karmaşık senaryolarınız varsa (örneğin arka planda bir bileşeni tetiklemek veya animasyon başlatmak), JavaScript dünyasının modern standartı olan Intersection Observer kullanılabilir:

```JavaScript
const gorseller = document.querySelectorAll('img.lazy');

const gozlemciKriterleri = {
  root: null, // viewport
  rootMargin: '0px',
  threshold: 0.1 // %10'u göründüğünde tetikle
};

const gorselYukleyici = (entries, observer) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src; // Gerçek görsel adresini yükle
      observer.unobserve(img);   // İzlemeyi durdur
    }
  });
};

const observer = new IntersectionObserver(gorselYukleyici, gozlemciKriterleri);
gorseller.forEach(img => observer.observe(img));
```
## 4. Dikkat Edilmesi Gereken Hatalar ve En İyi Pratikler
Sayfanın Üst Kısmında (Above the Fold) Asla Kullanmayın: Kullanıcının ekranı açar açmaz gördüğü ilk ekran alanındaki (hero banner, logo vb.) ana görsellere asla loading="lazy" vermeyin. Bu durum LCP (Largest Contentful Paint)metriğini olumsuz etkileyerek sitenizin açılış hızını yavaşlatır.

Boyut Belirtin (width ve height): Lazy loading uygulanan görsellerde tarayıcının yer tutucu (placeholder) boyutunu önceden rezerve edebilmesi için width ve height değerleri mutlaka belirtilmelidir; aksi takdirde görsel yüklendikçe sayfa aşağı kayma yapabilir (CLS - Cumulative Layout Shift).

Sonuç
Lazy loading, kullanıcı deneyimini bozmadan web performansını artıran en düşük maliyetli ve en etkili optimizasyonlardan biridir. HTML5'in loading="lazy" özelliği sayesinde ekstra kod yazmadan sitenizi hızlandırabilirsiniz.

Bir sonraki yazımızda görüşmek üzere!
