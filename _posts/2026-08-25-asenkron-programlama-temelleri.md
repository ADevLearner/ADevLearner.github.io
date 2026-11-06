---
layout: post
title: "Asenkron Programlama Nedir? Async/Await ve Callback Mantığı"
date: 2026-08-25 10:00:00 +0300
categories: [yazilim-temelleri]
tags: [asenkron, async-await, javascript, performans, backend]
excerpt: "Yazılımların donmadan, verimli ve eş zamanlı çalışmasını sağlayan asenkron programlama mantığını, Promise ve Async/Await yapılarıyla keşfedin."
---

Bilgisayarlar ve yazılımlar hayatımızın her alanında hızla işlem yaparken, bazen uzun süren işlemlerle (örneğin devasa bir dosya okuma, uzak bir sunucudan API isteği ile veri çekme veya veritabanı sorgulama) karşılaşırız. Eğer bu tür işlemler **senkron (sıralı)** bir şekilde çalıştırılırsa, işlem bitene kadar tüm program kilitlenir ve kullanıcı arayüzü donar.

Uygulamaların kesintisiz ve yüksek performanslı çalışmasını sağlayan en temel kavram **Asenkron Programlama (Asynchronous Programming)** sistemidir. Bu yazımızda asenkron mantığın ne anlama geldiğini, evrim sürecini ve modern dillerdeki kullanım şekillerini inceleyeceğiz.

---

## 1. Senkron vs Asenkron Çalışma Mantığı

* **Senkron (Synchronous):** Kod satırları yukarıdan aşağıya sırayla çalışır. Birinci satırdaki işlem bitmeden, ikinci satıra asla geçilemez. Eğer birinci işlem uzun sürerse, tüm sistem beklemek zorunda kalır (bloklayıcı yapı - blocking).
* **Asenkron (Asynchronous):** Uzun süren işlemler arka planda çalışmaya bırakılırken, program ana akışında diğer görevleri yerine getirmeye devam eder. İşlem tamamlandığında ise ilgili geri çağırım (`callback`) tetiklenir ve sonuç işlenir.

---

## 2. Asenkron Programlamanın Evrimi

Geçmişten günümüze asenkron işlemlerle başa çıkmak için farklı yaklaşımlar geliştirilmiştir:

### 1. Callback (Geri Çağırım) Fonksiyonları
Asenkron işlemlerin ilk ve en temel yöntemidir. Bir işlem bittiğinde çalıştırılmak üzere başka bir fonksiyona argüman olarak verilir. Ancak çok fazla iç içe callback kullanıldığında kod okunmaz hale gelir ve buna yazılım dünyasında **Callback Hell (Geri Çağırım Cehennemi)** denir.

### 2. Promise (Sözler)
Callback hell sorununu çözmek için geliştirilen yapıdır. Bir işlemin gelecekte başarılı (`resolved`) veya hatalı (`rejected`) sonuçlanacağını taahhüt eden nesnelerdir. `.then()` ve `.catch()` zincirleriyle okunabilirlik artırılmıştır.

### 3. Async / Await (Modern Yaklaşım)
Günümüz modern programlama dillerinde (JavaScript, C#, Python vb.) standart haline gelen en temiz yöntemdir. Asenkron kodları tıpkı senkron kodlar gibi yazmanıza olanak tanır, bu sayede hata ayıklamak (`debugging`) ve kodu okumak son derece kolaylaşır.

---

## 3. Pratik Örnek: Async/Await Kullanımı (JavaScript)

Aşağıdaki örnekte bir API'den veri çekme işleminin `async/await` ile ne kadar temiz yazıldığı görülmektedir:

```javascript
async function kullaniciBilgisiniGetir() {
    try {
        console.log("Veri yükleniyor...");
        
        // Sunucudan veri gelene kadar burada bekler (diğer kodları bloklamaz)
        let yanıt = await fetch('[https://api.ornek.com/kullanici/1](https://api.ornek.com/kullanici/1)');
        let veri = await yanıt.json();
        
        console.log("Kullanıcı Bilgisi:", veri.isim);
    } catch (hata) {
        console.error("Bir hata oluştu:", hata);
    }
}

kullaniciBilgisiniGetir();
```
Sonuç
Asenkron programlama mantığını kavramak; özellikle web ve mobil uygulamalarda kullanıcı deneyimini iyileştiren, sunucu kaynaklarını verimli kullanan yüksek performanslı yazılımlar geliştirmek için şarttır.

Bir sonraki yazımızda görüşmek üzere!
