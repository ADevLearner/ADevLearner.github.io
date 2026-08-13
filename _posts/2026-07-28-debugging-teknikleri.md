---
title: "console.log'dan Öteye: Etkili Debugging Teknikleri"
date: 2026-07-28
categories:
  - programlama
tags:
  - debugging
  - verimlilik
excerpt: "Hata ayıklama sürecini hızlandıran araç ve yaklaşımların pratik bir özeti."
---

`console.log` her zaman elimizin altında olan pratik bir araç, ama tek başına
karmaşık hataları çözmek için genelde yetersiz kalır.

## Debugger Kullanmak

Tarayıcı DevTools'unda veya IDE'nizde breakpoint koymak, kodun her adımda ne
yaptığını canlı olarak izlemenizi sağlar. `debugger;` ifadesini kod içine
eklemek, tarayıcı geliştirici araçları açıkken otomatik olarak o satırda
durmasını sağlar.

```javascript
function hesapla(a, b) {
  debugger;
  return a + b;
}
```

## Binary Search Yaklaşımı

Hatanın nerede olduğunu bilmiyorsanız, kodun ortasına bir kontrol noktası koyup
hatanın o noktadan önce mi sonra mı oluştuğunu tespit edin. Sonra o aralığı
ikiye bölerek devam edin — büyük bir kod tabanında hatayı çok daha hızlı
bulmanızı sağlar.

## Hata Mesajını Dikkatlice Okuyun

Stack trace'in en üstündeki satır her zaman hatanın kaynağı olmayabilir; bazen
asıl sorun birkaç satır aşağıdaki bir çağrıdan kaynaklanır. Tüm stack trace'i
okumak, hatanın gerçek kök nedenini bulmada zaman kazandırır.

## İzole Bir Ortamda Yeniden Üretin

Büyük bir uygulamada hatayı ayıklamak yerine, sorunu minimal bir örnekle (sadece
hatayı tetikleyen kod parçasıyla) yeniden üretmek hem hatayı anlamayı kolaylaştırır
hem de başkalarından yardım isterken paylaşmanız gereken kod miktarını azaltır.

## Rubber Duck Debugging

Kodu bir başkasına (ya da masanızdaki bir plastik ördeğe) satır satır anlatmaya
çalışmak, genelde açıklama sürecinin ortasında hatayı fark etmenizi sağlar —
şaşırtıcı derecede etkili bir yöntemdir.
