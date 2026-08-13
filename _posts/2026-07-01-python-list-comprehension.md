---
title: "Python'da List Comprehension Ne Zaman Kullanılmalı?"
date: 2026-07-01
categories:
  - python
tags:
  - python
  - performans
excerpt: "List comprehension'ın klasik for döngüsüne göre avantajları ve okunabilirliği bozduğu sınır noktalar."
---

List comprehension, Python'a özgü ve oldukça sevilen bir sözdizimi. Ama her yerde
kullanmak kodu daha karmaşık hale getirebilir.

## Temel Kullanım

```python
kareler = [x**2 for x in range(10)]
```

Aynı işi klasik döngüyle yazsanız üç satır tutar; list comprehension tek satırda
hem daha kısa hem de Python yorumlayıcısı için genelde daha hızlıdır.

## Koşullu Filtreleme

```python
ciftler = [x for x in range(20) if x % 2 == 0]
```

## Ne Zaman Kullanmamalı

İç içe birden fazla koşul veya döngü gerektiğinde list comprehension okunabilirliği
ciddi şekilde düşürür:

```python
# Okunması zor
sonuc = [x*y for x in range(10) for y in range(10) if x != y if (x+y) % 2 == 0]
```

Bu durumda klasik bir for döngüsü, kod inceleyen bir başkası (ya da altı ay sonraki
siz) için çok daha anlaşılır olur.

## Sonuç

List comprehension, tek seviyeli dönüşüm ve filtreleme işlemlerinde harika bir araç.
Karmaşıklık arttığında okunabilirliği performanstan önce düşünmek gerekir.
