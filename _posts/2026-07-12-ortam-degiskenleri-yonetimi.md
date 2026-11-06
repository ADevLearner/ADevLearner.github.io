---
layout: post
title: "Ortam Değişkenleri (Environment Variables) Yönetimi ve Güvenlik En İyi Pratikleri"
date: 2026-07-12 10:00:00 +0300
categories: [guvenlik]
tags: [env, guvenlik, devops, konfigurasyon, api-key]
excerpt: "Uygulama hassas verilerini ve konfigürasyonlarını koddan ayırmanın yolları, .env kullanımı ve üretim ortamında güvenlik pratikleri."
---

Modern yazılım geliştirme süreçlerinde karşılaşılan en büyük güvenlik açıklarından biri, veritabanı şifreleri, API anahtarları (`API Keys`) ve gizli token'ların doğrudan kaynak kodun içine yazılmasıdır (hardcoding). Bu tür hassas bilgilerin kaynak kodla birlikte GitHub gibi açık veya kapalı depolama alanlarına yüklenmesi, ciddi veri sızıntılarına yol açabilir.

Bu sorunu kökten çözmek için **Ortam Değişkenleri (Environment Variables)** kullanılır. Bu yazımızda, ortam değişkenlerinin mantığını, `.env` dosyalarının nasıl yönetilmesi gerektiğini ve üretim ortamındaki güvenlik pratiklerini inceleyeceğiz.

---

## 1. Ortam Değişkeni Nedir ve Neden Kullanılır?

Ortam değişkeni, çalışan işletim sisteminin veya uygulamanın çalıştığı konteynerin ortamından okuduğu dinamik bir named-value (isim-değer) çiftidir. 

### Kod İçinde Hardcoding Yapmanın Riskleri:
* **Güvenlik Açığı:** Kodunuzu bir ekip arkadaşınızla paylaştığınızda veya açık kaynaklı hale getirdiğinizde tüm gizli anahtarlar ifşa olur.
* **Esneklik Eksikliği:** Geliştirme (development), test (staging) ve canlı (production) ortamları için farklı veritabanı adresleri kullanmak gerektiğinde her defasında kodu değiştirmek imkansızdır.

Ortam değişkenleri sayesinde kodunuz aynı kalır; sadece değişen ortama göre değişkenlerin değerleri (örn. `DATABASE_URL`) farklı okunur.

---

## 2. Projelerde `.env` Dosyası Kullanımı

Yerel geliştirme (local development) ortamında bu değişkenleri yönetmek için genellikle kök dizinde bir `.env` dosyası oluşturulur.

### Tipik Bir `.env` Dosyası Örneği:

```env
PORT=3000
NODE_ENV=development
DATABASE_URL=postgres://kullanici:sifre@localhost:5432/veritabani
STRIPE_API_KEY=sk_test_51Mz...
```
Kod İçinden Okuma (Node.js Örneği):
Popüler dotenv kütüphanesini kullanarak bu değişkenleri güvenle projenize dahil edebilirsiniz:

```JavaScript
require('dotenv').config();

const port = process.env.PORT || 8080;
const dbUrl = process.env.DATABASE_URL;

console.log(`Sunucu ${port} portunda başlatılıyor...`);
```
### 3. Altın Kural: .gitignore Unutulmamalıdır!
Ortam değişkenleri dosyanız (.env) asla ama asla sürüm kontrol sistemine (Git) gönderilmemelidir.

Projenizin kök dizinindeki .gitignore dosyasına mutlaka .env eklenmelidir:

```Code snippet
# Hassas konfigürasyon dosyaları
.env
.env.local
.env.production
```
Bunun yerine, geliştiricilere rehber olması için projeye örnek bir .env.example dosyası eklenir (bu dosyada sadece değişken isimleri yer alır, gerçek gizli şifreler yazılmaz).

## 4. Üretim Ortamında (Production) Güvenlik Pratikleri
Canlı sunucularda veya bulut platformlarında (AWS, Heroku, Vercel, Docker) .env dosyası fiziksel olarak sunucuya kopyalanmak yerine şu yöntemlerle yönetilmelidir:

Bulut Servislerinin Secret Yöneticileri: AWS Secrets Manager, Google Cloud Secret Manager veya GitHub Actions Secrets gibi şifrelenmiş alanlar kullanılmalıdır.

Docker Ortam Değişkenleri: Konteyner ayağa kalkarken -e parametresi veya docker-compose.yml içindeki environment blokları ile güvenli şekilde enjekte edilmelidir.

Erişim Yetkilendirmesi (Principle of Least Privilege): Uygulamanın kullandığı veritabanı kullanıcısının yetkileri sadece gerektiği kadar olmalı, tüm veritabanı üzerinde tam yetkili (SUPERUSER) hesaplar uygulama içinde kullanılmamalıdır.

Sonuç
Ortam değişkenleri yönetimi, hem projelerinizin farklı ortamlara kolayca uyum sağlamasını (portability) hem de güvenlik standartlarının üst seviyede tutulmasını sağlar. Küçük bir dikkat eksikliği büyük sızıntılara yol açabileceğinden, .env dosyalarının gizliliğine her zaman özen gösterilmelidir.

Bir sonraki yazımızda görüşmek üzere!
