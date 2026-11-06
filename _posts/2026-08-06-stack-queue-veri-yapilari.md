---
layout: single
title: "Stack (Yığın) ve Queue (Kuyruk) Veri Yapıları: Temelleri ve Kullanım Alanları"
date: 2026-08-06 10:00:00 +0300
categories: [veri-yapilari]
tags: [stack, queue, veri-yapilari, algoritmalar, yazilim-temelleri]
excerpt: "Yazılım geliştirme mülakatlarının ve temel mimarilerin vazgeçilmezi olan Stack ve Queue veri yapılarının çalışma mantığını keşfedin."
---

Yazılım geliştirme süreçlerinde verileri RAM üzerinde nasıl sakladığımız ve hangi sıra ile işlediğimiz, yazdığımız programların performansını ve doğruluğunu doğrudan etkiler. Temel veri yapıları (`data structures`) arasında en sık kullanılan iki doğrusal yapı **Stack (Yığın)** ve **Queue (Kuyruk)** sistemleridir.

Bu yazımızda LIFO ve FIFO mantıklarını, bu veri yapılarının arkasındaki çalışma prensiplerini ve gerçek hayattaki yazılım senaryolarını detaylıca inceleyeceğiz.

---

## 1. Stack (Yığın) Veri Yapısı: LIFO Mantığı

Stack, verilerin depolandığı ve işlendiği **LIFO (Last In, First Out - Son Giren İlk Çıkar)** prensibine dayanan bir veri yapısıdır. Tıpkı üst üste dizilmiş tabaklar gibidir; en son koyduğunuz tabak en üstte yer alır ve ilk olarak oradan alabilirsiniz.

### Temel Stack Operasyonları:
* **Push:** Yığının en üstüne yeni bir eleman eklemek.
* **Pop:** Yığının en üstündeki elemanı listeden çıkarmak ve döndürmek.
* **Peek (veya Top):** Listeden çıkarmadan sadece en üstteki elemana bakmak.

### Gerçek Hayat Senaryoları:
* **Tarayıcı Geçmişi (Geri Tuşu):** Ziyaret ettiğiniz son web sayfası her zaman en üsttedir; geri tuşuna bastığınızda son girdiğiniz sayfadan geriye doğru gidersiniz.
* **Undo (Geri Al) Mekanizmaları:** Metin düzenleyicilerde yaptığınız son hamle, `Ctrl + Z` yaptığınızda ilk olarak geri alınır.
* **Fonksiyon Çağrıları (Call Stack):** Yazılımlarda fonksiyonlar iç içe çağrıldığında bellek yönetimi Stack mantığıyla çalışır.

---

## 2. Queue (Kuyruk) Veri Yapısı: FIFO Mantığı

Queue, verilerin depolandığı ve işlendiği **FIFO (First In, First Out - İlk Giren İlk Çıkar)** prensibine dayanan bir veri yapısıdır. Tıpkı süpermarket kasasındaki sıra gibidir; kuyruğa ilk giren kişi işini ilk halleder ve kuyruktan ilk ayrılır.

### Temel Queue Operasyonları:
* **Enqueue:** Kuyruğun sonuna (arkasına) yeni bir eleman eklemek.
* **Dequeue:** Kuyruğun başından (önünden) ilk elemanı çıkarmak.

### Gerçek Hayat Senaryoları:
* **Yazıcı Kuyruğu (Printer Spool):** Belgeyi yazdırmak için gönderdiğiniz sıraya göre çıktılar alınır.
* **Asenkron İş Kuyrukları (Message Queues):** RabbitMQ, Redis veya Kafka gibi modern mimarilerde arka plan görevleri FIFO mantığıyla sırayla işlenir.

---

## 3. Kod Üzerinden Basit Bir Örnek (Python)

Python'da listeleri kullanarak Stack ve Queue mantığını simüle etmek oldukça basittir:

```python
# --- STACK ÖRNEĞİ (LIFO) ---
stack = []
stack.append("Sayfa 1") # Push
stack.append("Sayfa 2") # Push

print(stack.pop()) # Çıktı: Sayfa 2 (Son giren ilk çıktı)

# --- QUEUE ÖRNEĞİ (FIFO) ---
from collections import deque
kuyruk = deque()
kuyruk.append("Müşteri A") # Enqueue
kuyruk.append("Müşteri B") # Enqueue

print(kuyruk.popleft()) # Çıktı: Müşteri A (İlk giren ilk çıktı)
```
Sonuç
Stack ve Queue, temel mantıkları oldukça basit olmasına rağmen yazılım mühendisliğinde en karmaşık sistemlerin bile omurgasını oluşturan güçlü veri yapılarıdır. Doğru yerde doğru yapıyı seçmek, kodunuzun verimliliğini artırır.

Bir sonraki yazımızda görüşmek üzere!
