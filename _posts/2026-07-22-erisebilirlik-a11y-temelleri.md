---
layout: single
title: "Web Erişilebilirliği (a11y) Nedir? Her Geliştiricinin Bilmesi Gereken Temel Kurallar"
date: 2026-07-22 10:00:00 +0300
categories: [frontend]
tags: [erisilebilirlik, a11y, frontend, web-standartlari, ux]
excerpt: "Görme, işitme veya motor engeli olan kullanıcılar için web sitenizi nasıl erişilebilir hale getirebilirsiniz? Temel a11y pratikleri rehberi."
---

Yazılım geliştirme süreçlerinde genellikle tasarıma, performansa ve yeni özelliklere odaklanırız; ancak web sitelerinin **herkes** tarafından kullanılabilir olması gerektiği gerçeği sıklıkla göz ardı edilir. Görme, işitme, motor becerileri kısıtlı veya geçici engelleri (örneğin kolu kırık olan veya güneş ışığında ekranı göremediği için ekran okuyucu kullanan) olan milyonlarca insan interneti deneyimliyor.

İngilizce'de "accessibility" kelimesinin ilk ve son harfi arasındaki 11 harfi simgeleyen **a11y** kısaltmasıyla bilinen web erişilebilirliği, modern web standartlarının vazgeçilmez bir parçasıdır. Bu yazımızda, projelerinize ekleyebileceğiniz temel ve etkili a11y pratiklerini inceleyeceğiz.

---

## 1. Semantik (Anlamlı) HTML Kullanımı

Erişilebilir bir web sitesi inşa etmenin ilk ve en önemli kuralı, doğru HTML etiketlerini (`semantic HTML`) kullanmaktır. 

* **`<div>` yerine `<button>`:** Tıklanabilir öğeler için `div` veya `span` kullanmak yerine doğrudan `<button>` kullanmak, ekran okuyucuların o elementin tıklanabilir ve odaklanılabilir olduğunu otomatik olarak anlamasını sağlar.
* **Yapısal Etiketler:** `<nav>`, `<main>`, `<article>`, `<header>` ve `<footer>` gibi etiketler, ekran okuyucu kullanıcılarının sayfa içinde hızlıca başlıklar ve bölümler arasında gezinmesine (`landmark navigation`) olanak tanır.

---

## 2. Görsellerde Doğru `alt` Metni Kullanımı

Görseller, görme engelli kullanıcılar için tek başına bir şey ifade etmez. Bu yüzden `<img>` etiketlerinde `alt` (alternative text) niteliği hayati önem taşır.

```html
<!-- ✅ Doğru ve açıklayıcı alt metni -->
<img src="grafik.png" alt="2026 yılı aylık satış artış oranlarını gösteren çizgi grafik" />

<!-- ❌ Yetersiz veya eksik kullanım -->
<img src="grafik.png" alt="grafik" />
```
Dekoratif Görseller: Eğer görsel tamamen süs amaçlıysa ve bilgi içermiyorsa, ekran okuyucuların gereksiz yere okumaması için alt="" (boş bırakılmalı) şeklinde tanımlanmalıdır. alt etiketini tamamen silmek hata olarak kabul edilir.

## 3. Klavye ile Gezinme (Keyboard Navigation)
Birçok engelli kullanıcı fare (mouse) kullanamaz; bunun yerine klavyedeki Tab, Shift + Tab ve Enter tuşlarıyla sitelerde gezinirler.

Sitenizi test etmek için farenizi bir kenara bırakın ve sadece Tab tuşunu kullanarak tüm sayfanın içinde gezinmeyi deneyin.

Bütün interaktif elementlere (linkler, butonlar, form girdileri) klavye ile ulaşılabiliyor mu?

Focus Outline: CSS ile stil verirken odaklanan (:focus) elemanların etrafındaki çerçeveyi (outline: none;) asla tamamen kaldırmayın. Kullanıcının şu an sayfanın neresinde olduğunu görsel olarak görebilmesi gerekir.

## 4. Renk Kontrastı (Color Contrast)
Metinler ile arka plan rengi arasındaki kontrast oranı, görme keskinliği düşük kullanıcıların yazıları rahat okuyabilmesi için kritik bir eşiktir.

WCAG Standartları: Normal boyutlu metinler için arka planla aradaki kontrast oranının en az 4.5:1 olması önerilir.

Bu oranları manuel hesaplamak zorunda değilsiniz; Chrome DevTools'un renk seçicisi veya Lighthouse denetim araçları kontrast sorunlarını otomatik olarak tespit edebilir.

## 5. Neden Önemli ve Avantajları Nelerdir?
Kapsayıcılık (Inclusion): İnternet herkes için eşit bir hak olmalıdır; web sitenizin kapılarını tüm kullanıcılara açarsınız.

Yasal Zorunluluklar: Birçok ülkede kamu ve özel sektör web sitelerinin belirli erişilebilirlik standartlarını (WCAG) sağlaması yasal bir zorunluluk haline gelmiştir.

SEO (Arama Motoru Optimizasyonu): Erişilebilir bir site, semantik HTML yapısı ve doğru alt etiketleri sayesinde arama motorları tarafından çok daha iyi taranır ve anlaşılır.

Sonuç
Web erişilebilirliği, projenin en başında mimari aşamada düşünüldüğünde sonradan düzeltilmeye çalışılmasından çok daha kolay ve maliyetsizdir. Küçük dokunuşlarla sitenizi herkes için erişilebilir kılabilirsiniz.

Bir sonraki yazımızda görüşmek üzere!
