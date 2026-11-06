---
layout: post
title: "JWT (JSON Web Token) Nedir ve Nasıl Çalışır? Güvenli Kimlik Doğrulama Rehberi"
date: 2026-08-16 10:00:00 +0300
categories: [guvenlik]
tags: [jwt, auth, guvenlik, api, backend]
excerpt: "Modern web ve mobil uygulamalarda güvenli, durumsuz (stateless) kimlik doğrulama sağlamak için kullanılan JWT mimarisini ve yapısını keşfedin."
---

Modern web ve mobil uygulamalarda kullanıcıların sisteme giriş yaptıklarını doğrulamak (`authentication`) ve yetkilerini yönetmek (`authorization`) en kritik mimari kararlardan biridir. Geçmişte sunucu tarafında oturum (`session`) bilgileri bellek üzerinde veya veritabanında saklanırken, günümüzün dağıtık mikroservis mimarilerinde standart haline gelen yaklaşım **JWT (JSON Web Token)** kullanmaktır.

Bu yazımızda JWT'nin ne anlama geldiğini, yapısını, nasıl çalıştığını ve güvenlik açısından dikkat edilmesi gerekenleri inceleyeceğiz.

---

## 1. JWT (JSON Web Token) Nedir?

JWT, iki taraf (örneğin istemci ile sunucu) arasında güvenli bir şekilde JSON formatında bilgi taşımaya yarayan, açık standart (`RFC 7519`) tabanlı kompakt bir yöntemdir. 

* **Stateful (Durumlu) vs Stateless (Durumsuz):** Klasik session yöntemlerinde sunucu kullanıcının oturum açtığını hafızasında tutmak zorundadır. JWT ise tamamen **stateless (durumsuz)** çalışır; oturumla ilgili tüm bilgiler token'ın kendi içinde şifrelenmiş olarak taşınır. Sunucu ek bir veritabanı sorgusu yapmadan token'ın geçerliliğini doğrular.

---

## 2. JWT'nin Yapısı (Üç Parçalı Mimari)

Bir JWT token, nokta (`.`) işaretleriyle birbirine ayrılmış üç temel bölümden oluşur: `Header.Payload.Signature`

### 1. Header (Başlık)
Token'ın türünü (JWT) ve kullanılan imzalama algoritmasını (örneğin `HMAC SHA256` veya `RSA`) içerir.
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```
2. Payload (Veri Gövdesi)
Kullanıcıya ait bilgilerin (claims) saklandığı kısımdır. Kimlik (sub), kullanıcı adı, rolü ve token'ın son kullanma tarihi (exp) burada yer alır.

```JSON
{
  "sub": "1234567890",
  "name": "Ahmet Yılmaz",
  "role": "admin",
  "iat": 1723800000
}
```
⚠️ Not: Payload kısmı sadece Base64 ile kodlanır; şifrelenmez. Bu yüzden içerisine asla şifre gibi hassas veriler koyulmamalıdır.

3. Signature (İmza)
Header ve Payload kısımlarının sunucudaki gizli bir anahtar (secret key) ile birleştirilerek imzalandığı kısımdır. Token'ın yolda biri tarafından değiştirilip değiştirilmediğini (tamper-proof) doğrulamak için hayati önem taşır.

3. JWT Kimlik Doğrulama Akışı
Giriş (Login): Kullanıcı kullanıcı adı ve şifresiyle sunucuya istek atar.

Token Üretimi: Sunucu bilgileri doğrular ve kullanıcıya özel imzalanmış bir JWT üretip istemciye döner.

Saklama ve İstek Atma: İstemci (tarayıcı veya mobil uygulama) bu token'ı localStorage veya HttpOnly Cookie içinde saklar. Sonraki isteklerde Authorization: Bearer <token> başlığıyla sunucuya gönderir.

Doğrulama: Sunucu gelen token'ın imzasını kendi gizli anahtarıyla kontrol eder; geçerliyse isteğe onay verir.

4. Güvenlik İçin En İyi Pratikler (Best Practices)
Kısa Ömürlü Token'lar Kullanın: Erişim token'ları (Access Token) kısa süreli (örneğin 15 dakika) olmalıdır. Süresi dolduğunda yenilemek için Refresh Token mekanizması kurgulanmalıdır.

Hassas Veriler Saklamayın: Token içeriği Base64 ile okunabildiği için asla kredi kartı veya şifre barındırmayın.

Güvenli Saklama: XSS saldırılarından korunmak için token'ları JavaScript ile erişilemeyen HttpOnly ve Secure Cookie içinde saklamak en güvenli yaklaşımdır.

Sonuç
JWT, doğru yapılandırıldığında ölçeklenebilir, hızlı ve güvenli kimlik doğrulama süreçleri sunan harika bir araçtır.

Bir sonraki yazımızda görüşmek üzere!
