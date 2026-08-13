---
title: "JSON mu YAML mı? Yapılandırma Dosyaları İçin Doğru Seçim"
date: 2026-07-10
categories:
  - araçlar
tags:
  - json
  - yaml
excerpt: "İki yaygın veri formatının okunabilirlik, esneklik ve kullanım alanları açısından karşılaştırması."
---

Proje yapılandırma dosyası yazarken karşınıza genelde iki seçenek çıkar: JSON ve
YAML. İkisi de aynı işi yapıyor gibi görünse de kullanım senaryolarına göre biri
diğerinden daha uygun olabilir.

## JSON'un Avantajları

- Neredeyse her programlama dilinde native destek var
- Sözdizimi katı ve öngörülebilir, ayrıştırma hataları nadir
- API'ler arası veri alışverişinde standart format

```json
{
  "isim": "örnek",
  "aktif": true,
  "port": 8080
}
```

## YAML'ın Avantajları

- İnsan tarafından okunması çok daha kolay, girintileme temel yapı taşı
- Yorum satırı ekleyebilirsiniz (`#` ile), JSON'da bu mümkün değil
- Docker Compose, Kubernetes, GitHub Actions gibi araçların çoğu YAML kullanıyor

```yaml
isim: örnek
aktif: true
port: 8080
```

## Hangisini Seçmeli?

Makineler arası veri alışverişi (API cevapları, programatik veri) için JSON daha
güvenli bir seçim çünkü ayrıştırma kuralları çok net. İnsanların elle düzenleyeceği
yapılandırma dosyaları (CI/CD pipeline'ları, uygulama config'leri) için YAML daha
okunabilir bir deneyim sunar.

Tek dikkat edilmesi gereken nokta: YAML'da girintileme hataları sessizce farklı bir
yapı üretebilir, bu yüzden editörünüzde YAML linter kullanmak iyi bir alışkanlıktır.
