# Kurulum — Yapman Gereken 3 Şey

Bu paket senin için hazırlanmış bir Jekyll (Minimal Mistakes teması) tech blog'u.
İçinde 4 örnek yazı, AdSense entegrasyonu için hazır alt yapı var. Yayına almak için:

## 1. GitHub'a yükle

```bash
# Zip'i açtığın klasörde:
git init
git add .
git commit -m "ilk commit"
git branch -M main
git remote add origin https://github.com/KULLANICI_ADIN/KULLANICI_ADIN.github.io.git
git push -u origin main
```

`KULLANICI_ADIN.github.io` isminde bir repo oluşturursan GitHub Pages otomatik
olarak kök domain'de (https://kullaniciadin.github.io) yayınlar.

## 2. _config.yml içindeki şu satırları kendi bilgilerinle değiştir

```yaml
name          : "SENIN_ADIN"          -> gerçek adın
url           : "https://KULLANICI_ADIN.github.io"  -> gerçek GitHub kullanıcı adın
repository    : "KULLANICI_ADIN/KULLANICI_ADIN.github.io"
```

## 3. AdSense onayı gelince tek bir satır ekle

```yaml
adsense_pub_id : "ca-pub-XXXXXXXXXXXXXXXX"
```

Aynı anda repo kökündeki `ads.txt` dosyasındaki `pub-XXXXXXXXXXXXXXXX` kısmını da
AdSense panelinden aldığın gerçek publisher ID ile değiştir (başındaki `ca-` olmadan,
sadece `pub-...` kısmı). Bu dosya `https://kullaniciadin.github.io/ads.txt` adresinden
erişilebilir olmalı — AdSense sahiplik doğrulamasını bu dosya üzerinden yapıyor.

Bu satır boş olduğu sürece hiçbir reklam kodu render edilmez, yani şu an siteyi
AdSense'e başvurmadan önce güvenle yayınlayabilirsin.

Onay geldikten sonra her yazının altına otomatik reklam çıkar (`_layouts/single.html`
içindeki `adsense-unit.html` include'u sayesinde). Farklı bir yere reklam eklemek
istersen aynı include'u istediğin dosyaya şu şekilde çağırabilirsin:

```liquid
{% include adsense-unit.html slot="REKLAM_SLOT_ID" %}
```

`REKLAM_SLOT_ID`'yi AdSense panelinden oluşturduğun her ad unit için ayrı ayrı alırsın.

## 4. SEO için yapman gerekenler

Tema zaten hazır: her yazı otomatik sitemap.xml'e giriyor, Open Graph/Twitter meta
etiketleri ekleniyor. Senin yapman gerekenler:

- **`robots.txt` içindeki `KULLANICI_ADIN`'ı değiştir** — gerçek kullanıcı adınla.
- **Her yazıya `excerpt` ekle** (örnekler zaten bunu yapıyor) — Google arama sonucunda
  bu metni gösterir, boş bırakırsan yazının ilk cümlelerini rastgele keser.
- **Google Search Console'a siteni ekle** (search.google.com/search-console), doğrulama
  kodunu `_config.yml` içindeki `google_site_verification` alanına yapıştır. Bu, Google'ın
  siteni ne zaman ve nasıl taradığını görmeni sağlar, indexlenmeyi hızlandırır.
- **Başlıkları (title) ve yazı içindeki H2/H3 başlıkları anlamlı tut** — arama motorları
  sayfanın konusunu bu yapıdan çıkarır.
- **Site yayına girdikten sonra `sitemap.xml`'i Search Console'a manuel gönder**
  (Sitemaps sekmesinden `sitemap.xml` yaz, Submit'e bas) — indexlenme haftalar yerine
  günler sürebilir.

İsteğe bağlı ama faydalı: her yazıda en az 1-2 iç link (başka yazılarına) kullanmak,
Google'ın sitedeki sayfaları keşfetmesini kolaylaştırır.

## 5. AI arama motorları için (llms.txt)

`llms.txt` dosyası eklendi — ChatGPT, Perplexity, Claude gibi AI arama sistemleri
siteni taradığında önce bu dosyaya bakıp içeriğin özetini alıyor (henüz resmi bir
standart değil ama 2026'da yaygın kabul görüyor).

Yapman gerekenler:

- **`KULLANICI_ADIN` placeholder'larını değiştir** — dosyada birden fazla yerde geçiyor.
- **Yazı linklerini build sonrası doğrula.** Kategori isimleri Türkçe karakter
  içerdiği için (`araçlar`, `yazılım-pratikleri` gibi) Jekyll'in ürettiği gerçek URL
  senin tahmininden farklı çıkabilir. Siteyi yayınladıktan sonra `sitemap.xml`
  adresine gidip gerçek URL'leri kontrol et, gerekirse `llms.txt`'i güncelle.
- **Yeni yazı ekledikçe `llms.txt`'e de bir satır ekle** — otomatik güncellenmiyor,
  elle senkron tutman gerekiyor (sitemap.xml aksine bu otomatik değil).

## Yerelde test etmek istersen

```bash
bundle install
bundle exec jekyll serve
```

http://localhost:4000 adresinde canlı önizleme görürsün.
