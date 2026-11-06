---
layout: single
title: "Git Branch (Dal) Stratejileri: Büyük Ekipler İçin Sürdürülebilir Git İş Akışları"
date: 2026-08-11 10:00:00 +0300
categories: [gelistirme]
tags: [git, branch, workflow, devops, gitflow]
excerpt: "Birden fazla geliştiricinin aynı projede birbirinin kodunu ezmeden, düzenli ve hatasız çalışmasını sağlayan popüler Git branch stratejilerini keşfedin."
---

Yazılım geliştirme süreçlerinde tek başınıza kod yazarken her şeyi ana dal (`main`) üzerinde yapmak kolay gelebilir; ancak işin içine birden fazla geliştirici girdiğinde bu yaklaşım tam bir kaosa dönüşür. Aynı dosya üzerinde aynı anda yapılan değişiklikler çakışmalara (`merge conflict`), test edilmemiş kodların canlıya çıkmasına ve projenin patlamasına yol açabilir.

Bu karmaşayı önlemek ve ekiplerin uyum içinde çalışmasını sağlamak için **Git Branch (Dal) Stratejileri** kullanılır. Bu yazımızda, en popüler Git iş akışlarını ve projelerinizde nasıl uygulamanız gerektiğini inceleyeceğiz.

---

## 1. Git Branch Mantığı Nedir?

Git üzerinde `branch`, projenizin o anki halinden bağımsız bir kopya oluşturarak ana yapıyı bozmadan yeni özellikler geliştirmenize, hataları düzeltmenize veya deneysel çalışmalar yapmanıza olanak tanıyan izole çalışma alanlarıdır.

* İşiniz bittiğinde bu dalı ana dala güvenli bir şekilde birleştirebilir (`merge`) veya silebilirsiniz.

---

## 2. Popüler Git İş Akışı Stratejileri

Projelerinizin büyüklüğüne ve yayın sıklığına göre tercih edebileceğiniz temel stratejiler şunlardır:

### 1. Feature Branch Workflow (Özellik Dalları İş Akışı)
Küçük ve orta ölçekli ekipler için en ideal ve en sade yaklaşımdır:
* `main` dalı her zaman canlıya çıkmaya hazır, stabil ve temiz tutulur.
* Yeni bir özellik eklemek veya bir hatayı çözmek için `main` üzerinden yeni bir dal açılır (Örn: `git checkout -b feature/karsilama-sayfasi`).
* Geliştirme bitip testler tamamlandığında `Pull Request (PR)` açılarak koda ekip arkadaşları tarafından inceleme (`code review`) yapılır ve `main` dalına dahil edilir.

### 2. Git Flow
Geniş ekipler ve belirli periyotlarla versiyon çıkılan (`v1.0`, `v1.1` vb.) büyük projeler için tasarlanmış kurallı bir modeldir:
* **`main`:** Canlıdaki (`production`) en kararlı kodun bulunduğu dal.
* **`develop`:** Gelecek sürüm için hazırlanan tüm özelliklerin toplandığı ana geliştirme dalı.
* **`feature/...`:** Yeni özelliklerin geliştirildiği dallar.
* **`release/...`:** Canlıya alınmadan önce son testlerin ve hata düzeltmelerinin yapıldığı sürüm dalı.
* **`hotfix/...`:** Canlı ortamda ani patlayan kritik hataları anında çözmek için kullanılan acil durum dalları.

---

## 3. En İyi Pratikler ve İsimlendirme Kuralları

1. **Anlamlı İsimler Kullanın:** Dal isimleri ne amaçla açıldığını açıkça belirtmelidir.
   * `feature/kullanici-giris-ekrani`
   * `bugfix/sepet-hesaplama-hatasi`
2. **Dal Ömrünü Kısa Tutun:** Haftalarca süren ve devasa değişiklikler barındıran branch'ler yerine, küçük parçalara bölünmüş ve 1-2 günde `main` dalına merge edilebilecek kısa ömürlü dallar tercih edin.

---

## Sonuç

Doğru bir Git branch stratejisi benimsemek, ekip içi iletişimi güçlendirir, hata oranlarını minimuma indirir ve sürüm yayınlama süreçlerini son derece akıcı hale getirir.

Bir sonraki yazımızda görüşmek üzere!
