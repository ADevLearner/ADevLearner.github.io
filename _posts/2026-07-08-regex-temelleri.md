---
layout: single
title: "Regex'e Giriş: Karmaşık Görünen Söz Dizimini Çözmek ve Pratik Desenler"
date: 2026-07-08 10:00:00 +0300
categories: [programlama]
tags: [regex, metin-isleme, optimizasyon, ipuclari]
excerpt: "Regular expression'ların temel yapı taşları, e-posta ve telefon doğrulama desenleri ve günlük geliştirme süreçlerinde dikkat edilmesi gerekenler."
---

Yazılım geliştirme süreçlerinde metin işleme (text processing), veri doğrulama (validation) ve arama operasyonları kaçınılmazdır. Kullanıcının girdiği bir e-posta adresinin, telefon numarasının veya şifrenin doğru formatta olup olmadığını kontrol etmek için en güçlü araç **Regular Expression (Regex)** yani Düzenli İfadelerdir. 

İlk bakışta anlamsız karakter yığınları gibi görünse de, Regex mantığı kavrandıktan sonra karmaşık string manipülasyonlarını tek satırda çözmenizi sağlayan sihirli bir değneğe dönüşür. Bu yazımızda, regex'in temel yapı taşlarını, gerçek hayat senaryolarını ve kaçınılması gereken performans tuzaklarını inceleyeceğiz.

---

## 1. Temel Karakterler ve Meta-Karakterler

Regex, metin içinde belirli kalıpları aramak için özel karakterler kullanır. Bu temel karakterlerin ne anlama geldiğini bildiğinizde, herhangi bir deseni okumak çok daha kolay hale gelecektir:

* **`.` (Nokta):** Yeni satır karakteri hariç her türden tek bir karakteri temsil eder.
* **`*` (Yıldız):** Önceki karakterin **sıfır veya daha fazla** kez tekrar edebileceğini belirtir.
* **`+` (Artı):** Önceki karakterin **bir veya daha fazla** kez tekrar etmesi gerektiğini belirtir.
* **`?` (Soru İşareti):** Önceki karakterin **sıfır veya bir kez** geçebileceğini (isteğe bağlı olduğunu) gösterir.
* **`\d`:** Herhangi bir rakamı (`0-9` aralığını) temsil eder.
* **`\w`:** Harf, rakam veya alt çizgi karakterini (`a-z`, `A-Z`, `0-9`, `_`) temsil eder.
* **`\s`:** Boşluk, sekme (tab) veya yeni satır gibi boşluk karakterlerini yakalar.

---

## 2. Gerçek Hayat Senaryoları: E-posta ve Telefon Doğrulama

Regex, özellikle form validasyonlarında verinin doğruluğunu denetlemek için kritik rol oynamaktadır.

### Örnek 1: Basit E-posta Doğrulama Deseni
Bir kullanıcının girdiği metnin standart e-posta yapısına uyup uymadığını kontrol etmek için şu kalıp kullanılabilir:

```regex
^[\w.-]+@[\w-]+\.[a-zA-Z]{2,}$
^ ve $: Satırın başlangıcını ve bitişini ifade eder (tüm metnin eşleşmesini sağlar).

[\w.-]+: Kullanıcı adında harf, rakam, nokta veya tire bulunabileceğini ve bunun en az bir karakter uzunluğunda olacağını belirtir.

@: E-posta adreslerinin olmazsa olmazı olan et işaretini arar.

[a-zA-Z]{2,}: Uzantı kısmının (örn. .com, .org) en az 2 harfli olması gerektiğini sınırlar.
```
Örnek 2: Telefon Numarası Formatı Yakalama
123-4567 formatındaki telefon numaralarını yakalamak ve parçalarına ayırmak için parantez gruplamaları kullanılabilir:
```regex
(\d{3})-(\d{4})
```
## 3. Gruplar ve Yakalama (Capturing Groups)
Parantez (...) kullanarak regex içinde alt gruplar oluşturabilirsiniz. Bu gruplar, eşleşen metnin belirli bölümlerini sonradan kod içinde (örneğin Python veya JavaScript ile) yakalayıp manipüle etmenizi sağlar:
```python
import re

metin = "İletişim: 555-0192"
desen = r"(\d{3})-(\d{4})"
sonuc = re.search(desen, metin)

if sonuc:
    print("Alan Kodu:", sonuc.group(1)) # Çıktı: 555
    print  ("Numara:", sonuc.group(2)) # Çıktı: 0192
```
## 4. En İyi Pratikler ve Dikkat Edilmesi Gerekenler
Online Test Araçları Kullanın: Karmaşık bir regex yazarken regex101.com gibi platformları kullanarak kalıbınızı canlı veriler üzerinde test edin ve ne eşleşiyor adım adım görün.

Aşırı Karmaşıklıktan Kaçının: Her şey için regex yazmaya çalışmayın. Yüzlerce karakter uzunluğundaki devasa regex kalıplarının bakımı (debugging) son derece zordur.

Alternatifleri Değerlendirin: Basit metin kontrollerinde (örn. bir kelimenin belirli bir karakterle başlayıp başlamadığını bulmak için) startswith() veya split(), replace() gibi yerleşik string metotları regex'e göre çok daha okunabilir ve hızlı çalışabilir.

Sonuç
Regex, yazılımcının çantasında bulundurması gereken en keskin bıçaklardan biridir. Temel kuralları öğrendikten sonra metin arama ve veri süzme işlemlerinde büyük bir zaman kazandırır.

Bir sonraki yazımızda görüşmek üzere!
