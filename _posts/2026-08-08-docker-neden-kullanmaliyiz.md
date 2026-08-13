---
title: "Docker Nedir ve Neden Kullanmalısınız?"
date: 2026-08-08
categories:
  - devops
tags:
  - docker
  - container
excerpt: "Konteynerleştirmenin geliştirme ve dağıtım süreçlerine kattığı somut faydalar."
---

"Benim makinemde çalışıyordu" cümlesi yazılım dünyasında en tanıdık şikayetlerden
biridir. Docker, tam olarak bu sorunu çözmek için var.

## Konteyner ile Sanal Makine Farkı

Sanal makineler tüm bir işletim sistemini simüle ederken, konteynerler ana sistemin
çekirdeğini paylaşır ve sadece uygulamayı çalıştırmak için gerekli katmanı izole eder.
Bu da onları çok daha hafif ve hızlı başlatılabilir yapar.

## Basit Bir Örnek

Bir Node.js uygulamasını konteynerleştirmek için gereken Dockerfile oldukça kısadır:

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["node", "index.js"]
```

## Ne Zaman Gerçekten İşe Yarar?

Docker'ın en büyük faydası ekip büyüdükçe ve dağıtım ortamları çeşitlendikçe ortaya
çıkar: geliştirme, test ve production ortamlarının birebir aynı olmasını garanti eder.
Tek kişilik küçük bir script projesinde fazladan karmaşıklık da katabilir, bu yüzden
her projeye otomatik eklenmesi gereken bir araç değildir.
