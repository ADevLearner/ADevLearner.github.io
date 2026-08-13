---
title: "Git ile Çalışırken Bilmeniz Gereken Temel Komutlar"
date: 2026-08-01
categories:
  - araçlar
tags:
  - git
  - versiyon-kontrolu
excerpt: "Git'e yeni başlayanlar için günlük iş akışında en çok kullanılan komutların derli toplu bir özeti."
---

Git, yazılım projelerinde versiyon kontrolü için en yaygın kullanılan araç. Bu yazıda
günlük iş akışında en sık ihtiyaç duyacağınız komutları özetliyorum.

## Temel Komutlar

- `git status` — çalışma dizinindeki değişiklikleri gösterir
- `git add <dosya>` — değişiklikleri staging alanına ekler
- `git commit -m "mesaj"` — değişiklikleri kalıcı hale getirir
- `git push` — commit'leri uzak repoya gönderir
- `git pull` — uzak repodaki güncellemeleri çeker

## Branch Yönetimi

Yeni bir özellik üzerinde çalışırken ana koddan izole bir dal açmak iyi bir pratiktir:

```bash
git checkout -b yeni-ozellik
```

İşiniz bitince ana dala geri dönüp birleştirebilirsiniz:

```bash
git checkout main
git merge yeni-ozellik
```

## Sık Yapılan Hatalar

Yanlış bir commit mesajı yazdıysanız, henüz push etmediyseniz düzeltmek kolaydır:

```bash
git commit --amend -m "doğru mesaj"
```

Push ettikten sonra geçmişi değiştirmek takım çalışmasında sorun yaratabilir, bu yüzden
`--amend` ve `rebase` gibi geçmiş değiştiren komutları paylaşılan branch'lerde dikkatli kullanın.
