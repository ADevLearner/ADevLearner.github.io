---
title: "Takım Halinde Çalışırken Git Branch Stratejisi Seçmek"
date: 2026-08-11
categories:
  - araçlar
tags:
  - git
  - takim-calismasi
excerpt: "Git Flow ve Trunk-Based Development gibi yaygın branch stratejilerinin karşılaştırması."
---

Bir takım büyüdükçe "herkes main'e direkt push atsın" yaklaşımı sürdürülemez
hale gelir. İşte en yaygın iki branch stratejisi ve hangi durumda hangisinin
tercih edilebileceği.

## Git Flow

Uzun ömürlü `develop` ve `main` branch'leri, her özellik için ayrı `feature/*`
branch'leri, sürüm hazırlığı için `release/*` branch'leri içeren yapılandırılmış
bir modeldir.

```
main
 └── develop
      ├── feature/giris-sayfasi
      ├── feature/odeme-entegrasyonu
      └── release/v2.0
```

**Ne zaman uygun:** Belirli sürüm takvimleri olan, birden fazla sürümü aynı anda
destekleyen (örn. v1 ve v2'yi paralel bakım yapan) projeler için mantıklıdır.

## Trunk-Based Development

Herkesin kısa ömürlü branch'lerde (genelde 1-2 gün) çalışıp sık sık `main`'e
merge ettiği, daha basit bir yaklaşımdır.

```
main
 ├── kisa-omurlu-branch-1 (birkaç saat)
 └── kisa-omurlu-branch-2 (bir gün)
```

**Ne zaman uygun:** Sürekli dağıtım (continuous deployment) yapan, hızlı iterasyon
isteyen küçük-orta ölçekli takımlar için daha az sürtünme yaratır.

## Pratik Tavsiye

Küçük bir takımda veya bireysel projede Git Flow'un tüm karmaşıklığı genelde
gereksizdir — basit bir `main` + kısa ömürlü feature branch'leri yaklaşımı
yeterlidir. Takım büyüdükçe ve sürüm yönetimi karmaşıklaştıkça daha yapılandırılmış
bir modele geçmek mantıklı olabilir.

Hangi stratejiyi seçerseniz seçin, önemli olan takımın o kurala tutarlı şekilde
uymasıdır — yarı Git Flow yarı trunk-based bir karışım genelde kafa karışıklığına
yol açar.
