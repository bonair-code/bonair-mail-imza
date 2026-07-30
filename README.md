# Bonair Mail İmzası Oluşturucu

Çalışanların **ad, soyad, unvan, e-posta ve telefon** bilgilerini girerek
kurumsal mail imzası oluşturabildiği tek sayfalık web uygulaması.
Şablon herkes için sabittir; yalnızca kişisel bilgiler değişir.

**Canlı adres:** https://bonair-mail-imza.web.app

---

# 🔧 BAKIM REHBERİ — Link ve metinleri nasıl güncellerim?

> Aşağıdaki her şey **tek bir dosyada**: `index.html`
> Değişiklik yapmak için programlama bilmeniz gerekmez, sadece tırnak
> içindeki adresi/metni değiştirip kaydedersiniz.

## 1. Neyi nerede değiştireceğim?

Dosyayı açıp **Ctrl+F** ile aşağıdaki kelimeyi aratın:

| Değiştirmek istediğiniz | Arayın | Satır (yaklaşık) |
|---|---|---|
| **Instagram** linki | `imza-ig.png` | 226 |
| **LinkedIn** linki | `imza-in.png` | 227 |
| **Web sitesi** (dünya ikonu) linki | `imza-globe.png` | 228 |
| **Şirket sunumu PDF** linki | `imza-pdf.png` | 229 |
| İmzada yazan **web adresi metni** | `WEB_TEXT` | 234 |
| **Gizlilik metni (Türkçe)** | `DISCLAIMER_TR` | 231 |
| **Gizlilik metni (İngilizce)** | `DISCLAIMER_EN` | 232 |

Örnek — PDF linkini değiştirmek:

```js
{ img: 'imza-pdf.png',   url: 'https://technic.bonair.com.tr/assets/docs/bonair-technic-company-presentation.pdf', alt: 'Şirket Sunumu' }
                                └──────────────── SADECE BU KISMI DEĞİŞTİRİN ────────────────┘
```

⚠️ **Dikkat:** Tırnak işaretlerini (`'`) silmeyin, sadece aralarındaki
adresi değiştirin. Satır sonundaki virgülü de silmeyin.

## 2. Değişikliği nasıl yayınlarım?

### Yol A — GitHub üzerinden (en kolay, bilgisayara kurulum gerekmez)

1. https://github.com/bonair-code/bonair-mail-imza adresine gidin
2. `index.html` dosyasına tıklayın
3. Sağ üstteki **kalem (✏️ Edit)** simgesine tıklayın
4. Ctrl+F ile ilgili satırı bulup değiştirin
5. Sayfanın altındaki **Commit changes** düğmesine basın

Site **1–2 dakika içinde** otomatik güncellenir.
*(Bunun çalışması için "Otomatik yayın kurulumu" bölümündeki tek seferlik
ayarın yapılmış olması gerekir — bkz. aşağısı.)*

### Yol B — Kendi bilgisayarınızdan

```bash
git clone https://github.com/bonair-code/bonair-mail-imza.git
cd bonair-mail-imza

# index.html dosyasını herhangi bir metin düzenleyiciyle açıp değiştirin

npm install -g firebase-tools    # sadece ilk kez
firebase login                   # sadece ilk kez
firebase deploy --only hosting
```

## 3. Değişikliği kontrol etme

Yayından sonra siteyi **Ctrl+F5** ile açın (tarayıcı eski sürümü
göstermesin diye), imzayı yeniden oluşturup kopyalayın ve Outlook'taki
imzanızı güncelleyin.

---

## ⚙️ Otomatik yayın kurulumu (tek seferlik)

Bu ayar yapılırsa, GitHub'da dosyayı düzenleyip kaydettiğiniz anda site
kendiliğinden güncellenir; başka hiçbir şey yapmanız gerekmez.

1. Kendi bilgisayarınızda terminal açıp şunu çalıştırın:
   ```bash
   npm install -g firebase-tools
   firebase login:ci
   ```
   Tarayıcı açılır, Google hesabınızla giriş yaparsınız. Terminalde
   `1//...` ile başlayan **uzun bir kod** görünür — onu kopyalayın.

2. https://github.com/bonair-code/bonair-mail-imza/settings/secrets/actions
   adresine gidin → **New repository secret**

3. **Name:** `FIREBASE_TOKEN`
   **Secret:** 1. adımda kopyaladığınız kod → **Add secret**

Bu kadar. Artık her `index.html` düzenlemesi otomatik yayınlanır.
(Kurulum yapılmazsa sorun olmaz; sadece Yol B ile elle yayınlarsınız.)

---

## Teknik notlar

### İmza neden fotoğraf olarak üretiliyor?

Mail programları (özellikle Outlook) yazı tiplerini ve hizalamayı bozar.
Bu yüzden kişisel bilgiler, şablon görselinin üzerine tarayıcıda çizilip
tek bir PNG'ye dönüştürülür — böylece imza her yerde birebir aynı görünür.
Sağdaki sosyal medya ikonları ise tıklanabilir kalması için ayrı durur.

### Görsel adresleri

Kopyalanan imzadaki görsellerin mail istemcilerinde görünebilmesi için
mutlak URL gerekir. `BASE` değişkeni bunu otomatik yönetir: site hangi
adreste yayınlanıyorsa görseller de oradan servis edilir. Ekstra ayar
gerekmez — yeter ki `imza-*.png` dosyaları site köküne deploy edilsin.

### Dosyalar

| Dosya | Açıklama |
|---|---|
| `index.html` | Uygulamanın tamamı (form + imza üreteci + yönergeler) |
| `imza-sablon.png` | İmzanın boş şablonu (logo, hangar, ikonlar, adres) |
| `imza-ig / in / globe / pdf .png` | Sosyal ve link ikonları (tıklanabilir) |
| `fonts/` | Montserrat yazı tipi (imza fotoğrafında kullanılır) |
| `firebase.json`, `.firebaserc` | Firebase Hosting ayarları |

### Şablon görselini değiştirmek

`imza-sablon.png` dosyası; logo, hangar çizimi, iletişim ikonları ve
adres satırını içerir. Kişisel bilgiler (ad, unvan, e-posta, telefon)
bunun üzerine `index.html` içindeki `DRAW` ayarlarına göre çizilir.
Şablon değişirse `DRAW` içindeki koordinatların (`x`, `by`) yeniden
ayarlanması gerekir.
