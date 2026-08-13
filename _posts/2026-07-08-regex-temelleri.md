---
title: "Regex'e Giriş: Karmaşık Görünen Söz Dizimini Çözmek"
date: 2026-07-08
categories:
  - programlama
tags:
  - regex
  - metin-isleme
excerpt: "Regular expression'ların temel yapı taşları ve en sık kullanılan kalıpların pratik örnekleri."
---

Regex (regular expression), metin içinde desen aramak için kullanılan güçlü bir
araç. İlk bakışta şifreli görünse de birkaç temel kuralı öğrenince mantığı oturur.

## Temel Karakterler

- `.` — herhangi bir karakter
- `*` — önceki karakterin sıfır veya daha fazla tekrarı
- `+` — önceki karakterin bir veya daha fazla tekrarı
- `?` — önceki karakterin sıfır veya bir kez geçmesi
- `\d` — herhangi bir rakam
- `\w` — harf, rakam veya alt çizgi

## Örnek: E-posta Doğrulama

```regex
^[\w.-]+@[\w-]+\.[a-zA-Z]{2,}$
```

Bu kalıp, basit bir e-posta formatını doğrular. Gerçek dünyada e-posta doğrulama
standardı çok daha karmaşıktır, ama günlük kullanım için bu yeterli olur.

## Gruplar ve Yakalama

Parantez kullanarak bir deseni "yakalayabilir" ve sonradan referans alabilirsiniz:

```regex
(\d{3})-(\d{4})
```

Bu, telefon numarası gibi `123-4567` formatındaki metinleri iki gruba ayırır.

## Pratik Tavsiye

Karmaşık bir regex yazmadan önce online test araçlarından (regex101.com gibi)
faydalanmak, kalıbı canlı olarak test edip anlamanızı kolaylaştırır. Ayrıca çok
karmaşık regex'lerin bakımı zor olur — bazen basit string işlemleri (split,
replace) regex'ten daha okunabilir bir çözüm sunar.
