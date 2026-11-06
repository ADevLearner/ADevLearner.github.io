---
layout: single
title: "JSON vs YAML: Hangisi Neden Tercih Edilmeli? Karşılaştırmalı İnceleme"
date: 2026-07-10 10:00:00 +0300
categories: [konfigurasyon]
tags: [json, yaml, veri-formatlari, konfigurasyon]
excerpt: "Modern yazılım projelerinde veri değişimi ve konfigürasyon dosyaları için kullanılan JSON ile YAML formatlarının farkları, avantajları ve dezavantajları."
---

Modern yazılım geliştirme, bulut bilişim ve DevOps dünyasında farklı sistemlerin birbiriyle konuşabilmesi, verilerin depolanması ve uygulama ayarlarının yönetilmesi için çeşitli veri serileştirme formatları kullanılır. Bu formatlar arasında en popüler iki seçenek **JSON (JavaScript Object Notation)** ve **YAML (YAML Ain't Markup Language)** dilleridir.

Her iki format da insanların okuyabileceği (human-readable) metin tabanlı yapılardır; ancak kullanım amaçları, sözdizimleri (syntax) ve sağladıkları esneklikler açısından önemli farklılıklar gösterirler. Bu yazımızda JSON ve YAML formatlarını detaylıca karşılaştıracak, hangi senaryoda hangisini tercih etmeniz gerektiğini inceleyeceğiz.

---

## 1. JSON (JavaScript Object Notation) Nedir?

JSON, adından da anlaşılacağı üzere JavaScript'in nesne gösterim biçiminden türetilmiş, ancak dilden bağımsız olarak evrensel bir standart haline gelmiş hafif bir veri değişim formatıdır. Günümüzde RESTful API'lerin ve mikroservis mimarilerinin omurgasını oluşturur.

### Tipik Bir JSON Örneği

```json
{
  "sunucu": {
    "host": "127.0.0.1",
    "port": 8080,
    "aktif_mi": true,
    "yetkiler": ["admin", "editor"]
  }
}
```
JSON'ın Öne Çıkan Özellikleri:Evrensel Destek: Neredeyse tüm programlama dillerinde yerleşik (native) olarak parse edilebilir (işlenebilir).Katı Kurallar: Süslü parantezler {} ve çift tırnaklar "" zorunludur. Virgül veya tırnak unutulması anında hata (SyntaxError) üretir.Yorum Satırı Desteği Yoktur: Standart JSON spesifikasyonunda yorum satırı (// veya /* */) yazılmasına izin verilmez; bu da konfigürasyon dosyalarında dokümantasyon eklemeyi zorlaştırır.

## 2. YAML (YAML Ain't Markup Language) Nedir?

YAML, özellikle insan tarafından okunabilirliği en üst düzeye çıkarmak için tasarlanmış bir veri serileştirme dilidir. Süslü parantezler ve tırnaklar yerine girintileme (indentation) ve boşluk mantığına dayanır. Docker Compose, Kubernetes konfigürasyonları ve CI/CD pipeline dosyaları (GitHub Actions, GitLab CI) ağırlıklı olarak YAML kullanır.Tipik Bir YAML ÖrneğiYAMLsunucu:
```json 
 host: "127.0.0.1"
  port: 8080
  aktif_mi: true
  yetkiler:
    - admin
    - editor
```
YAML'ın Öne Çıkan Özellikleri:

Yüksek Okunabilirlik: Parantez kalabalığını ortadan kaldırdığı için özellikle büyük konfigürasyon dosyalarında çok temiz bir görünüm sunar.
Yorum Satırı Desteği: # işaretiyle satırlara kolayca açıklama ve yorum eklenebilir.
Karmaşık Yapılar: Çoklu belge (multi-document) desteği ve çapraz referanslama gibi gelişmiş özellikler barındırır.

## 3. Temel Karşılaştırma Tablosu

Özellik,JSON,YAML
Sözdizimi,Süslü parantez {} ve tırnaklar,Boşluk ve girintileme (indentation)
Yorum Satırı (Comments),Desteklemez ❌,Destekler (#) ✅
Okunabilirlik,Karmaşık yapılarda zorlaşabilir,Oldukça temiz ve sezgisel
İşleme Hızı (Parsing),Çok hızlı ve standart,Karmaşık yapıları parse etmek daha yavaştır
Ana Kullanım Alanı,"API veri alışverişi, NoSQL veritabanları","Konfigürasyon dosyaları, DevOps araçları"
## 4. Hangi Durumda Hangisini Seçmeliyiz?
JSON Tercih Etmelisiniz:

Sistemler arası anlık veri alışverişinde (REST API yanıtları).

Hızın ve veri işleme performansının kritik olduğu durumlarda.

Verinin programlar tarafından dinamik olarak üretilip tüketileceği senaryolarda.

YAML Tercih Etmelisiniz:

Uygulama ayar dosyalarında (config.yaml, docker-compose.yml).

İnsanların düzenleyeceği konfigürasyonlarda (açıklama satırlarına ihtiyaç duyulduğu için).

DevOps ve bulut altyapı yönetim araçlarında.

Sonuç
JSON ve YAML birbirinin rakibi değil, farklı alanlardaki ihtiyaçları çözen tamamlayıcı araçlardır. API dünyasında JSON tahtını korurken, konfigürasyon ve altyapı dünyasında YAML vazgeçilmez bir standarttır.

Bir sonraki yazımızda görüşmek üzere!
