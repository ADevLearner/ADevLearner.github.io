---
layout: single
title: "CI/CD Pipeline Temelleri: Sürekli Entegrasyon ve Dağıtım Süreçleri Nasıl Kurulur?"
date: 2026-07-30 10:00:00 +0300
categories: [devops]
tags: [cicd, devops, github-actions, otomasyon, surec-yonetimi]
excerpt: "Yazılım geliştirme yaşam döngüsünü hızlandıran ve hata oranlarını minimuma indiren CI/CD pipeline mimarisinin temellerini keşfedin."
---

Yazılım geliştirme dünyasında eskiden yeni bir sürüm (`release`) yayınlamak haftalar hatta aylar süren zahmetli manuel süreçler gerektirirdi. Kodlar yazılır, testler elle yapılır, sunucuya FTP ile dosyalar atılır ve sıklıkla beklenmedik hatalar (bug) yüzünden sistem patlardı. Günümüzün çevik (`agile`) ve hızlı yazılım dünyasında bu yöntemler tarihe karıştı.

Bugün modern ekipler, kodun yazıldığı andan canlı ortama (`production`) ulaşana kadar geçen tüm süreci otomatikleştiren **CI/CD (Continuous Integration / Continuous Deployment)** pipeline mimarisini kullanırlar. Bu yazımızda CI/CD kavramının ne anlama geldiğini, aşamalarını ve projelerinizde nasıl kurgulayabileceğinizi inceleyeceğiz.

---

## 1. CI (Continuous Integration - Sürekli Entegrasyon) Nedir?

Sürekli Entegrasyon, ekip içerisindeki farklı geliştiricilerin yazdığı kod parçalarının gün içerisinde sık sık (genellikle günde birkaç kez) ortak ana depoya (`main` veya `master` branch) birleştirilmesi sürecidir.

* **Otomatik Testler:** Her kod birleştirme (`merge`) işleminde, sistem arka planda otomatik olarak unit testleri ve entegrasyon testlerini çalıştırır.
* **Erken Hata Tespiti:** Bir geliştiricinin yazdığı kod başka bir modülü bozdugunda, bu durum saatler sonra değil, saniyeler içinde tespit edilir ve ekibe bildirilir.

---

## 2. CD (Continuous Delivery / Continuous Deployment - Sürekli Teslimat / Dağıtım)

CD kavramı, CI adımından sonra devreye giren ve kodun canlıya alınma sürecini otomatikleştiren aşamadır.

* **Continuous Delivery (Sürekli Teslimat):** Testlerden başarıyla geçen kod, her an canlıya alınmaya hazır bir şekilde paketlenir. Canlıya çıkış düğmesine (`deploy`) basmak tek tıkla gerçekleşir.
* **Continuous Deployment (Sürekli Dağıtım):** Testleri geçen kodun hiçbir insan müdahalesine gerek kalmadan, tamamen otomatik olarak canlı sunuculara yüklenmesi ve kullanıcıya sunulması sürecidir.

---

## 3. Tipik Bir CI/CD Pipeline (İş Akışı) Aşamaları

Bir kod satırının geliştirici bilgisinden çıkıp canlıya ulaşana kadar geçtiği standart adımlar şunlardır:

1. **Source (Kaynak Kod):** Geliştirici kodu yazar ve GitHub / GitLab deposuna `push` eder.
2. **Build (Derleme):** Sunucu üzerindeki pipeline aracı (Örn: GitHub Actions, GitLab CI, Jenkins) kodu indirir ve çalıştırılabilir hale getirmek için derler.
3. **Test (Otomatik Testler):** Birim testler, güvenlik taramaları (`lint`, `SAST`) ve kod kalitesi denetimleri çalıştırılır.
4. **Deploy (Canıya Alma):** Tüm testler yeşil ışık yaktığında kod otomatik olarak üretim sunucusuna veya bulut ortamına gönderilir.

---

## 4. GitHub Actions ile Basit Bir Örnek Pipeline

GitHub üzerinde projelerinize kolayca CI/CD entegre etmek için `.github/workflows` klasörü altına YAML dosyaları ekleyebilirsiniz. Örneğin, her `push` işleminde çalışan basit bir test pipeline'ı:

```yaml
name: Node.js CI Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build-ve-test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    
    - name: Node.js Ortamını Kur
      uses: actions/setup-node@v4
      with:
        node-version: '20'
        
    - name: Bağımlılıkları Yükle
      run: npm install
      
    - name: Otomatik Testleri Çalıştır
      run: npm test
```
Sonuç
CI/CD pipeline süreçleri, yazılım kalitesini artıran ve geliştiricilerin rutin işlerle zaman kaybetmesini önleyen en güçlü DevOps pratikleridir. Otomasyona yatırım yapmak, uzun vadede projelerin sürdürülebilirliğini doğrudan güvence altına alır.

Bir sonraki yazımızda görüşmek üzere!
