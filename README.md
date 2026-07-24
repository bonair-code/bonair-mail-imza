# Bonair Mail İmzası Oluşturucu

Kullanıcıların **ad-soyad, unvan, e-posta ve telefon** bilgilerini girerek
Bonair Technic kurumsal mail imzası oluşturabildiği tek sayfalık statik web
uygulaması. Şablon herkes için sabittir; yalnızca kişisel bilgiler değişir.

## Özellikler

- Word taslağına birebir uyan imza tasarımı (logo, isim, unvan, iletişim,
  bina illüstrasyonu, sosyal/link ikonları, gizlilik dipnotu)
- Canlı önizleme
- Tek tıkla **zengin metin** olarak kopyalama (doğrudan Gmail/Outlook imza
  alanına yapıştırılır) veya **HTML kodu** olarak kopyalama
- Bağımlılık yok — saf HTML/CSS/JS, tek dosya (`index.html`)

## Dosyalar

| Dosya | Açıklama |
|---|---|
| `index.html` | Uygulamanın tamamı (form + imza üreteci) |
| `imza-building.png` | Sağdaki bina illüstrasyonu |
| `imza-ic-*.png` | İletişim ikonları (e-posta / web / telefon) |
| `imza-ig / in / globe / pdf .png` | Sosyal ve link ikonları |
| `bonair-logo.png` | Kurumsal logo |

## Kişisel bilgiler dışında sabit olanlar

Web adresi, şirket adı, açık adres, sosyal medya linkleri (Instagram,
LinkedIn, web, şirket sunumu PDF'i) ve gizlilik notu `index.html` içinde
sabittir. Güncellemek için ilgili değişkenleri (`WEB_URL`, `ADDRESS`,
`SOCIAL`, `DISCLAIMER` …) düzenlemeniz yeterlidir.

## Görsel adresleri (önemli)

Kopyalanan imzadaki görsellerin mail istemcilerinde görünebilmesi için
**mutlak URL** gerekir. `BASE` değişkeni bunu otomatik yönetir: site hangi
adreste yayınlanıyorsa görseller de oradan servis edilir. Ekstra ayar
gerekmez — yeter ki `imza-*.png` dosyaları site köküne deploy edilsin.

## Yayınlama (Firebase Hosting)

```bash
# İlk kez:
firebase login
firebase use --add        # kullanılacak Firebase projesini seç

# Her deploy:
firebase deploy --only hosting
```

Vercel / Netlify / GitHub Pages gibi herhangi bir statik barındırıcı da
çalışır; bu klasörü kök olarak yayınlamanız yeterlidir.
