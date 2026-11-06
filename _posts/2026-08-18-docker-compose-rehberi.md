---
layout: single
title: "Docker Compose Nedir? Çoklu Konteyner Yönetimi ve Pratik Rehber"
date: 2026-08-18 10:00:00 +0300
categories: [devops]
tags: [docker, docker-compose, devops, mikroservisler, konteyner]
excerpt: "Birden fazla Docker konteynerini tek bir komutla ve tek bir YAML dosyası üzerinden kolayca yönetmenizi sağlayan Docker Compose rehberi."
---

Önceki yazılarımızda tekil Docker konteynerlerinin hayatımızı nasıl kolaylaştırdığını incelemiştik. Ancak gerçek dünyadaki modern web projeleri asla tek başına çalışmaz. Tipik bir web uygulamasının arkasında; Node.js/Python tabanlı bir backend servisi, verileri saklamak için PostgreSQL veya MySQL, hızlı erişim için Redis ve ön yüzde Nginx gibi birden fazla bileşen bulunur.

Her birini ayrı ayrı `docker run` komutlarıyla ayağa kaldırmak ve aralarındaki ağ bağlantılarını manuel kurmak tam bir eziyettir. İşte bu noktada imdadımıza **Docker Compose** yetişir. Bu yazımızda Docker Compose'un ne olduğunu, nasıl yapılandırıldığını ve projelerinizi nasıl hızlandıracağını inceleyeceğiz.

---

## 1. Docker Compose Nedir?

**Docker Compose**, birden fazla Docker konteynerini tanımlamak ve tek bir YAML dosyası üzerinden yönetmek için kullanılan resmi bir araçtır. 

* **Tek Komutla Yönetim:** Tüm sistemi ayağa kaldırmak için tek bir `docker-compose up` komutu yeterlidir; tüm servisler sırasıyla, doğru ağ bağlantılarıyla ve hacimlerle (`volumes`) ayağa kalkar.
* **Bildirimsiz Yapı (Declarative):** Sistemin nasıl çalışması gerektiğini karmaşık bash komutlarıyla değil, sade bir YAML dosyasıyla net bir şekilde tanımlarsınız.

---

## 2. Örnek Bir `docker-compose.yml` Dosyası

Tipik bir web projesi için (Örn: Node.js API ve PostgreSQL veritabanı) hazırlanan örnek bir `docker-compose.yml` dosyası şu şekildedir:

```yaml
version: '3.8'

services:
  veritabani:
    image: postgres:15-alpine
    container_name: postgres_db
    restart: always
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: gizlisifre
      POSTGRES_DB: uygulama_db
    ports:
      - "5432:5432"
    volumes:
      - db_verileri:/var/lib/postgresql/data

  web-api:
    build: .
    container_name: node_api_servisi
    restart: always
    ports:
      - "3000:3000"
    environment:
      - DB_HOST=veritabani
      - DB_PORT=5432
    depends_on:
      - veritabani

volumes:
  db_verileri:
```
Bu Dosyada Neler Var?
services: Projede çalışacak her bir konteyneri (veritabani ve web-api) temsil eder.

ports: Bilgisayarınız ile konteyner arasındaki port eşitlemesini yapar.

depends_on: web-api servisinin, veritabanı ayağa kalkmadan başlamamasını sağlar.

volumes: Bilgisayar yeniden başlasa bile veritabanı verilerinin kalıcı (persistent) olarak saklanmasını garanti eder.

3. En Çok Kullanılan Docker Compose Komutları
Proje klasörünüzde docker-compose.yml dosyasının bulunduğu dizindeyken terminalde kullanabileceğiniz temel komutlar şunlardır:

```Bash
# Tüm servisleri arka planda (detached mode) ayağa kaldırır
docker-compose up -d

# Çalışan tüm servislerin log çıktıklarını anlık izler
docker-compose logs -f

# Tüm servisleri güvenli bir şekilde durdurur ve siler
docker-compose down
```
Sonuç
Docker Compose, çoklu konteyner mimarileriyle çalışan geliştiriciler için vazgeçilmez bir üretkenlik aracıdır. Yerel geliştirme ortamlarını standartlaştırmak ve saniyeler içinde tüm projeyi ayağa kaldırmak için mutlaka kullanılmalıdır.

Bir sonraki yazımızda görüşmek üzere!
