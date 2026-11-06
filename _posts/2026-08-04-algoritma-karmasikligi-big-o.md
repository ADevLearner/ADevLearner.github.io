---
layout: single
title: "Big O Notasyonu Nedir? Algoritma Karmaşıklığı ve Performans Analizi"
date: 2026-08-04 10:00:00 +0300
categories: [algoritma]
tags: [big-o, algoritma, performans, veri-yapilari, optimizasyon]
excerpt: "Yazılım mülakatlarının ve performans optimizasyonunun temeli olan Big O notasyonunu, zaman ve bellek karmaşıklığını örneklerle inceleyin."
---

Yazılım geliştirme sürecinde iki farklı geliştirici aynı problemi çözen iki farklı kod yazabilir; ancak bu kodlardan hangisinin daha "iyi" veya "verimli" olduğunu nasıl anlarız? Bilgisayarın işlemcisi hızlandıkça kodun hızı da artar, peki yazdığımız algoritmanın gerçekten optimize olup olmadığını donanımdan bağımsız nasıl ölçebiliriz?

İşte bu noktada **Big O Notasyonu (Big O Notation)** devreye girer. Bu yazımızda, algoritma karmaşıklığının ne anlama geldiğini, en sık karşılaşılan Big O türlerini ve kod yazarken dikkat etmemiz gerekenleri inceleyeceğiz.

---

## 1. Big O Notasyonu Nedir?

Big O, matematiksel bir kavram olup, bir algoritmanın çalışma süresinin veya bellek tüketiminin, girdi verisinin boyutu (`n`) büyüdükçe nasıl bir eğriyle arttığını ifade eder. 

* Donanımdan bağımsızdır (İster süper bilgisayarda çalıştırın ister eski bir telefonda, algoritmanın matematiksel büyüme hızı değişmez).
* Kodun milisaniye cinsinden süresine değil, girdi boyutu arttıkça işlem sayısının nasıl katlandığına odaklanır.

---

## 2. En Sık Karşılaşılan Big O Tipleri

### O(1) - Sabit Zaman (Constant Time)
Girdi boyutu (`n`) ne kadar büyürse büyüsün, algoritmanın çalışma süresi her zaman sabittir.
* *Örnek:* Bir dizinin ilk elemanına indis (`index[0]`) ile erişmek.

### O(n) - Doğrusal Zaman (Linear Time)
Girdi boyutu (`n`) arttıkça, çalışma süresi de tam olarak aynı oranda (doğrusal olarak) artar.
* *Örnek:* Bir dizinin içinde aranan bir sayıyı bulmak için baştan sona tek tek arama yapmak (`for` döngüsü).

### O(n^2) - Karesel Zaman (Quadratic Time)
Genellikle iç içe iki döngü (`nested loops`) içeren algoritmalarda görülür. Girdi boyutu arttıkça işlem yükü katlanarak artar. Büyük veri setlerinde performans kabusuna dönüşebilir.
* *Örnek:* İç içe döngülerle matris karşılaştırmaları veya kabarcık sıralaması (`Bubble Sort`) algoritmaları.

---

## 3. Pratik Örneklerle Zaman Karmaşıklığı

Aşağıdaki iki farklı yaklaşımı inceleyelim:

```python
# O(n) - Doğrusal arama (Liste uzadıkça işlem süresi artar)
def eleman_var_mi(liste, hedef):
    for eleman in liste:
        if eleman == hedef:
            return True
    return False
```
Eğer verileriniz sıralı ise, her seferinde aralığı yarıya bölen Binary Search (İkili Arama) algoritmasını kullanarak karmaşıklığı O(log n) seviyesine indirebilirsiniz. Bu da milyonlarca eleman içinde saniyeler yerine mikro saniyeler içinde sonuca ulaşmanızı sağlar.

## 4. Zaman (Time Complexity) vs Bellek (Space Complexity) Karmaşıklığı
Algoritma analizi yaparken sadece ne kadar sürede çalıştığına (Time Complexity) değil, çalışırken ne kadar RAM tükettiğine (Space Complexity) de dikkat edilmelidir. Bazı durumlarda hızı artırmak için fazladan bellek harcayabiliriz (Time-Memory Trade-off).

Sonuç
Big O notasyonunu bilmek ve kod yazarken karmaşıklığı hesaba katmak, ölçeklenebilir ve yüksek performanslı yazılımlar üretmenin temel anahtarıdır.

Bir sonraki yazımızda görüşmek üzere!
