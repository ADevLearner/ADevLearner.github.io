---
title: "CI/CD Pipeline Nedir? Temel Kavramlar"
date: 2026-07-30
categories:
  - devops
tags:
  - cicd
  - otomasyon
excerpt: "Sürekli entegrasyon ve dağıtımın ne olduğu ve küçük projelerde bile neden fayda sağladığı."
---

CI/CD (Continuous Integration / Continuous Deployment), kod değişikliklerinin
otomatik olarak test edilip yayına alınmasını sağlayan bir süreçtir. Büyük
şirketlere özgü karmaşık bir konu gibi görünse de küçük projelerde bile kurulumu
oldukça kolaydır.

## Continuous Integration (CI)

Her kod push'unda otomatik olarak testlerin çalıştırılmasıdır. Amaç, bir
hatanın ana branch'e karışmadan önce fark edilmesi.

```yaml
# .github/workflows/test.yml örneği
name: Test
on: [push]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test
```

Bu basit yapılandırma, her push'ta testlerin otomatik çalışmasını sağlar.

## Continuous Deployment (CD)

Testler başarılı olduğunda kodun otomatik olarak production ortamına
yayınlanmasıdır. Bazı ekipler bu adımı tamamen otomatik bırakırken, bazıları
manuel bir onay adımı ekler (Continuous Delivery olarak da anılır).

## Neden Küçük Projelerde de Kullanmalı?

- Her değişiklikte manuel test yapma yükünü ortadan kaldırır
- Bir hatanın production'a sızma riskini azaltır
- Yeni katılan bir geliştirici bile "push et, testler otomatik çalışsın" akışına
  hemen alışır

## Başlangıç İçin Öneri

GitHub Actions, GitLab CI veya CircleCI gibi araçların ücretsiz planları küçük
projeler için fazlasıyla yeterlidir. İlk pipeline'ınızı sadece "testleri
çalıştır" adımıyla başlatıp, zamanla deploy adımını eklemek makul bir yol
haritasıdır.
