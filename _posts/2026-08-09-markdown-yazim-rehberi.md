---
title: "Markdown'ı Etkili Kullanmak İçin Pratik Bir Rehber"
date: 2026-08-09
categories:
  - araçlar
tags:
  - markdown
  - yazim
excerpt: "GitHub README'lerinden blog yazılarına kadar her yerde karşınıza çıkan Markdown'ın temel söz dizimi."
---

Markdown, düz metni hızlıca biçimlendirmenizi sağlayan hafif bir işaretleme
dili. GitHub, Notion, bu blogun kendisi dahil pek çok platformda karşınıza
çıkar.

## Başlıklar

```markdown
# Büyük Başlık
## Orta Başlık
### Küçük Başlık
```

## Vurgu

```markdown
**kalın metin**
*italik metin*
~~üstü çizili metin~~
```

## Listeler

```markdown
- Madde bir
- Madde iki
  - Alt madde

1. Birinci adım
2. İkinci adım
```

## Bağlantı ve Görsel

```markdown
[Bağlantı metni](https://ornek.com)
![Görsel açıklaması](gorsel.png)
```

## Kod Blokları

Satır içi kod için tek backtick, blok kod için üç backtick kullanılır:

```markdown
`satır içi kod`

```javascript
function selam() {
  console.log("merhaba");
}
```
```

Dil adını (`javascript`, `python` gibi) belirtmek, sözdizimi renklendirmesinin
doğru çalışmasını sağlar.

## Tablolar

```markdown
| Sütun 1 | Sütun 2 |
|---------|---------|
| Veri A  | Veri B  |
```

## Neden Öğrenmeye Değer?

Markdown, HTML'e göre çok daha hızlı yazılır ve README dosyalarından teknik
dokümantasyona, blog yazılarından proje notlarına kadar yazılım dünyasının
neredeyse her yerinde standart haline gelmiştir.
