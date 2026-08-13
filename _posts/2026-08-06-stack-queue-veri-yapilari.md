---
title: "Stack ve Queue: İki Temel Veri Yapısının Farkı"
date: 2026-08-06
categories:
  - programlama
tags:
  - veri-yapilari
  - algoritma
excerpt: "LIFO ve FIFO mantığıyla çalışan iki temel veri yapısının gerçek dünya kullanım alanları."
---

Stack ve Queue, birbirine benzeyen ama tamamen farklı mantıkla çalışan iki temel
veri yapısıdır. İkisi de eleman ekleme/çıkarma işlemi yapar, fark sırada.

## Stack (Yığın): LIFO

"Last In, First Out" — son eklenen eleman ilk çıkar. Bir tabak yığınını
düşünün: en üste koyduğunuz tabağı ilk siz alırsınız.

```javascript
const stack = [];
stack.push(1);
stack.push(2);
stack.push(3);
stack.pop(); // 3 döner
```

**Gerçek dünya kullanımı:** Tarayıcınızın "geri" butonu bir stack ile çalışır —
en son ziyaret ettiğiniz sayfa, geri gittiğinizde ilk gösterilendir. Fonksiyon
çağrı yığını (call stack) da aynı mantıkla işler.

## Queue (Kuyruk): FIFO

"First In, First Out" — ilk eklenen eleman ilk çıkar. Bir market kuyruğu gibi:
sıraya ilk giren, ilk hizmet alır.

```javascript
const queue = [];
queue.push(1);
queue.push(2);
queue.push(3);
queue.shift(); // 1 döner
```

**Gerçek dünya kullanımı:** Bir yazıcıya gönderilen belgeler sırayla işlenir;
ilk gönderilen belge ilk basılır. Görev kuyrukları (task queue) ve mesaj
kuyrukları (RabbitMQ, SQS gibi sistemler) da bu mantıkla çalışır.

## Ne Zaman Hangisini Kullanmalı?

İşlem sırasının "en son geleni önce işle" mantığında olması gerekiyorsa
(geri alma işlemleri, parantez eşleştirme gibi problemler) stack; "sıraya
girme sırasıyla işle" mantığı gerekiyorsa (görev kuyrukları, genişlik öncelikli
arama/BFS) queue tercih edilir.
