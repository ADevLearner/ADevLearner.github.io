---
layout: single
title: "REST API Tasarım İlkeleri: En İyi Pratikler ve Doğru Kullanım Rehberi"
date: 2026-08-05 10:00:00 +0300
categories: [backend]
tags: [rest-api, backend, http, tasarim, best-practices]
excerpt: "Modern web ve mobil uygulamalar için sürdürülebilir, anlaşılır ve standartlara uygun RESTful API tasarlamanın altın kurallarını keşfedin."
---

Günümüz yazılım dünyasında web siteleri, mobil uygulamalar, mikroservisler ve üçüncü taraf entegrasyonlar veri alışverişi için ağırlıklı olarak **REST (Representational State Transfer)** API mimarisini kullanırlar. REST, HTTP protokolünün yeteneklerini maksimum düzeyde kullanan, esnek ve bağımsız bir mimari stildir.

Ancak her API "RESTful" olduğunu iddia etse de, birçoğu standartlara uymadığı için zamanla bakım edilemez hale gelir. Bu yazımızda, sürdürülebilir ve temiz bir REST API tasarlamak için uymanız gereken temel kuralları ve en iyi pratikleri inceleyeceğiz.

---

## 1. URI (Endpoint) İsimlendirme Kuralları

API uç noktalarınız (`endpoints`), istemcilerin (client) kaynaklara (`resources`) nasıl erişeceğini belirler. İsimlendirme yaparken fiiller yerine **çoğul isimler** kullanılmalıdır.

* **❌ Yanlış Kullanım:** `/getKullanicilar`, `/create-user`, `/deleteUrun/5`
* **✅ Doğru Kullanım (RESTful):**
  * `GET /users` (Tüm kullanıcıları getir)
  * `POST /users` (Yeni kullanıcı oluştur)
  * `GET /users/5` (ID'si 5 olan kullanıcıyı getir)
  * `DELETE /users/5` (ID'si 5 olan kullanıcıyı sil)

İlişkisel verilere erişirken alt kaynak (nested resource) yolları tercih edilmelidir:
* `GET /users/5/orders` (ID'si 5 olan kullanıcının siparişlerini getir)

---

## 2. Doğru HTTP Metotlarının Kullanımı

HTTP protokolü, her işlemin amacına uygun standart metotlar barındırır. İstek atarken yanlış metot kullanmaktan kaçınılmalıdır:

* **`GET`:** Sunucudan veri okumak (listelemek veya detay çekmek) için kullanılır. Veriyi değiştirmez (safe & idempotent).
* **`POST`:** Sunucuda yeni bir kaynak oluşturmak için kullanılır.
* **`PUT`:** Mevcut bir kaynağın **tamamını** güncellemek (veya yoksa oluşturmak) için kullanılır.
* **`PATCH`:** Mevcut bir kaynağın sadece **belirli alanlarını** kısmi olarak güncellemek için kullanılır.
* **`DELETE`:** Belirtilen kaynağı sistemden silmek için kullanılır.

---

## 3. Anlamlı HTTP Status Kodları Döndürmek

İstemciye dönen yanıtın başarılı mı yoksa hatalı mı olduğunu anlamak için HTTP durum kodları doğru seçilmelidir:

* **`200 OK`:** İstek başarılı ve sonuç döndürüldü.
* **`201 Created`:** İstek başarılı ve yeni bir kaynak başarıyla oluşturuldu (Genellikle `POST` isteklerinden sonra döner).
* **`204 No Content`:** İstek başarılı ancak dönecek bir gövde (`body`) içeriği yok (Genellikle `DELETE` işlemlerinde tercih edilir).
* **`400 Bad Request`:** Eksik veya hatalı parametre gönderildi (İstemci hatası).
* **`401 Unauthorized`:** Kimlik doğrulama başarısız veya token geçersiz.
* **`403 Forbidden`:** Kullanıcının bu kaynağa erişim yetkisi yok.
* **`404 Not Found`:** Aranan kaynak sunucuda bulunamadı.
* **`500 Internal Server Error`:** Sunucu tarafında beklenmeyen, kritik bir hata oluştu.

---

## 4. Versiyonlama (Versioning) Stratejisi

API'nizde gelecekte yapacağınız breaking change (geriye dönük uyumsuzluk yaratan) değişiklikler mevcut mobil veya web istemcilerini bozabilir. Bu yüzden API'ler ilk günden itibaren versiyonlanmalıdır:

* **URL Üzerinden Versiyonlama (En Yaygın):** `https://api.ornek.com/v1/users`

---

## Sonuç

İyi tasarlanmış bir REST API; öngörülebilir, dokümante etmesi kolay ve geliştirici dostudur. Standartlara sadık kalmak, uzun vadede entegrasyon maliyetlerini minimuma indirir.

Bir sonraki yazımızda görüşmek üzere!
