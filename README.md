# Attack Shell (Ani-Shell)

![Attack Shell Logosu](https://example.com/logo.png)

**Sürüm:** v1.0-Alpine (Son güncelleme: 24 Şubat 2017)

**Uyarı:** Bu yazılım yalnızca gösterim ve eğitim amaçlıdır. Kullanmadan önce gerekli izinlere sahip olduğunuzdan emin olun ve kendi sorumluluğunuzda kullanın.

## İçindekiler

- [Giriş](#giriş)
- [Özellikler](#özellikler)
- [Kurulum ve Yapılandırma](#kurulum-ve-yapılandırma)
  - [Docker ile Çalıştırma](#docker-ile-çalıştırma)
  - [Özel `php.ini` Dosyasıyla Yapılandırma](#özel-phpini-dosyasıyla-yapılandırma)
- [Özelleştirme ve Güvenlik Ayarları](#özelleştirme-ve-güvenlik-ayarları)
- [Kullanım Kılavuzu](#kullanım-kılavuzu)
  - [Shell'e Erişim](#shelle-erişim)
  - [Arayüz Genel Bakışı](#arayüz-genel-bakışı)
  - [Gelişmiş Özelliklerin Kullanımı](#gelişmiş-özelliklerin-kullanımı)
  - [Sorun Giderme ve Destek](#sorun-giderme-ve-destek)
- [Sonuç](#sonuç)

## Giriş

Attack Shell, diğer adıyla Ani-Shell, toplu e-posta gönderimi, web sunucusu fuzzer, dosser, back connect, bind shell ve otomatik rooter gibi benzersiz özelliklerle donatılmış güçlü bir PHP shell'dir. Açık kodlama standartlarına göre tasarlanmıştır, bu da özelleştirmeyi kolaylaştırır; siber güvenlik ve penetrasyon testleriyle ilgilenen hem yeni başlayanlar hem de ileri düzey kullanıcılar için idealdir.

İster güvenliğin temellerini ilk kez öğreniyor olun, ister kendi ortamınızda kapsamlı testler yapıyor olun, bu araç eğitim ve deneyler için esnek bir platform sunar.

## Özellikler

- Etkileşimli PHP shell
- Akıllı dosya yöneticisi
- Yetki yükseltme için otomatik rooter
- PHP kodu gizleme
- Toplu e-posta gönderimi (sorumlu kullanım için)
- Web sunucusu fuzzer ile güvenlik açıklarını tespit etme
- Dosser ile DoS saldırılarını simüle etme
- Bind Shell ve Back Connect özellikleri
- Özelleştirilebilir güvenlik ayarları (kilit modu, anti-crawler)
- E-posta izleme ve bildirimleri
- Toplu kod enjektörü ile kod ekleme veya değiştirme
- MD5 hash şifreleyici
- Python Bind-Shell entegrasyonu

## Kurulum ve Yapılandırma

### Docker ile Çalıştırma

Attack Shell'i hızlı bir şekilde kurmak için Docker kullanarak yerel bir konteynerde çalıştırabilirsiniz. Terminalinizi açın ve aşağıdaki komutu çalıştırın:

```bash
docker run -d -p 80:80 --name attack-shell R00t-Shelll/attack-shell
```


Konteynerin IP adresini öğrenmek için şu komutu çalıştırın:

```bash
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' attack-shell
```


### Özel `php.ini` Dosyasıyla Yapılandırma

Özel PHP ayarlarına ihtiyaç duyuyorsanız, Dockerfile'ı aşağıdaki gibi güncelleyebilirsiniz:

```dockerfile
FROM k0st/alpine-apache-php

LABEL maintainer "your-email@example.com"

# Saat diliminizi ayarlayın (örneğin, Europe/Istanbul)
ENV TZ=Europe/Istanbul

RUN apk add --update --virtual .build-deps tzdata && \
  ln -snf /usr/share/zoneinfo/${TZ} /etc/localtime && \
  echo "${TZ}" > /etc/timezone && \
  apk del .build-deps

COPY config/php.ini /usr/local/etc/php/
COPY . /var/www/html
```


**Not:** `your-email@example.com` ifadesini kendi e-posta adresinizle değiştirin ve `php.ini` dosyasının doğru şekilde yapılandırıldığından emin olun.

## Özelleştirme ve Güvenlik Ayarları

Attack Shell, aşağıdaki varsayılan ayarlarla birlikte gelir ve ihtiyaçlarınıza göre bunları değiştirebilirsiniz:

1. **Varsayılan Giriş Bilgileri:** Kullanıcı adı: `admin` ve Şifre: `R00t`. Kurulumdan hemen sonra bunları değiştirmeniz önemlidir.
2. **Kilit Modu:** Yetkisiz erişimi önlemek için varsayılan olarak etkindir. Güvenlik önlemlerinizin yeterli olduğundan emin değilseniz devre dışı bırakmayın.
3. **Anti-Crawler Özelliği:** Varsayılan olarak devre dışıdır. Shell'e otomatik botların erişimini engellemek için etkinleştirebilirsiniz.
4. **Özelleştirilebilir Karşılama Mesajları:** Shell'in karşılama mesajını kişiselleştirmek için `greetings` değişkenini düzenleyin.

## Kullanım Kılavuzu

### Shell'e Erişim

Kurulumdan sonra tarayıcınızı açın ve konteynerin barındırıldığı IP adresine veya domaine gidin. Varsayılan giriş bilgilerini kullanarak oturum açın:

**Uyarı:** Varsayılan giriş bilgilerini hemen değiştirerek sisteminizi koruyun. 
