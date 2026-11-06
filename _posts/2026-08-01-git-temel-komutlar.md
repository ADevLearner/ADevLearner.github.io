---
layout: single
title: "Git Versiyon Kontrol Sistemine Giriş: En Çok Kullanılan Temel Komutlar"
date: 2026-08-01 10:00:00 +0300
categories: [gelistirme]
tags: [git, versiyon-kontrol, github, komutlar, yazilim-gelistirme]
excerpt: "Yazılım geliştirme süreçlerinin kalbi olan Git versiyon kontrol sisteminin mantığını ve günlük iş akışında en çok kullanılan temel komutları keşfedin."
---

Yazılım geliştirme dünyasında ister bireysel bir proje üzerinde çalışın ister devasa bir ekibin parçası olun, yazdığınız kodların geçmişini takip edebilmek, hata yaptığınızda eski çalışan sürüme dönebilmek ve başkalarıyla ortak çalışabilmek hayati önem taşır. Bu ihtiyacı kusursuz bir şekilde karşılayan araç **Git** versiyon kontrol sistemidir.

Bu yazımızda Git'in temel çalışma mantığını, dosya yaşam döngüsünü ve terminal üzerinden günlük olarak en çok ihtiyaç duyacağınız temel komutları inceleyeceğiz.

---

## 1. Git Nedir ve Neden Kullanılmalıdır?

Git, Linus Torvalds tarafından 2005 yılında geliştirilmiş dağıtık (distributed) bir versiyon kontrol sistemidir. Klasik yöntem olan "proje_v1_son_final.zip" şeklinde klasörler saklamak yerine, projenin her aşamasını ve yapılan her küçük değişikliği güvenli bir şekilde kaydeder.

### Git Kullanmanın Sağladığı Temel Avantajlar:
* **Zaman Yolculuğu:** Kodunuzun geçmişindeki herhangi bir dakikaya veya güne tek komutla geri dönebilirsiniz.
* **Takım Çalışması:** Birden fazla geliştiricinin aynı dosya üzerinde birbirlerinin kodunu ezmeden aynı anda çalışmasını sağlar.
* **Güvenlik ve Yedekleme:** Kodlarınız uzak depolarda (`GitHub`, `GitLab`, `Bitbucket`) güvenle saklanır.

---

## 2. Git Dosya Yaşam Döngüsü (File Lifecycle)

Git ile çalışırken dosyalarınız üç farklı durumda bulunabilir:
1. **Modified (Değiştirilmiş):** Üzerinde değişiklik yaptığınız ancak henüz Git'e kaydetmediğiniz dosyalar.
2. **Staged (Aşama Alınmış):** `git add` komutuyla bir sonraki commit için işaretlenmiş dosyalar.
3. **Committed (Kaydedilmiş):** `git commit` komutuyla kalıcı olarak Git geçmişine işlenmiş dosyalar.

---

## 3. En Çok Kullanılan Temel Git Komutları

Günlük geliştirme döngüsünde en sık kullanılan komutlar ve ne işe yaradıkları şunlardır:

### `git init`
Mevcut bir klasörü Git tarafından takip edilen bir proje deposu haline getirir.
```bash
git init
git status
```
Projenizin o anki durumunu gösterir; hangi dosyaların değiştirildiğini, hangilerinin eklendiğini listeler.

```Bash
git status
git add
```
Değişen dosyaları commit işlemine hazırlamak (staged alanına almak) için kullanılır.

```Bash
# Sadece belirli bir dosyayı ekleme
git add index.html
```

# Değişen tüm dosyaları ekleme
git add .
git commit
İşaretlenen dosyaları anlamlı bir mesajla birlikte kalıcı olarak yerel geçmişe kaydeder.

```Bash
git commit -m "Anasayfa tasarımı güncellendi ve hatalar giderildi"
git push
```
Yerel depoda yaptığınız commit'leri uzak sunucuya (GitHub vb.) gönderir.

```Bash
git push origin main
git pull
```
Uzak sunucudaki güncel değişiklikleri yerel bilgisayarınıza çeker ve senkronize eder.

```Bash
git pull origin main
```
En İyi Pratikler (Best Practices)
Anlamlı Commit Mesajları Yazın: "asdf", "update" veya "fix" gibi belirsiz mesajlar yerine, neyin değiştirildiğini özetleyen net mesajlar yazın (Örn: feat: kullanıcı giriş formu eklendi).

Küçük ve Sık Commit'ler Yapın: Gün sonunda tek bir devasa commit atmak yerine, her mantıklı küçük görevi tamamladıkça ayrı commit'ler oluşturun.

Sonuç
Git bilmek, modern bir yazılımcı için olmazsa olmaz temel bir beceridir. Temel komutları kas hafızanıza kazıdıktan sonra proje yönetimi son derece akıcı hale gelecektir.

Bir sonraki yazımızda görüşmek üzere!
