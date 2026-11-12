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

---

# 📢 GEÇİCİ DUYURU HANESİ

İmzanın altında, gizlilik metninin üstünde duran **geçici duyuru alanı**.
Fuar katılımı, bakım/sistem duyurusu, bayram mesajı — ne isterseniz.

```
┌──────────────────────────────────────┬────┐
│  Talha DUYGU                         │ ig │
│  Technical Quality & SMS Engineer    │ in │
│  +90 546 269 23 09                   │ 🌐 │
│  tduygu@bonair.com.tr                │pdf │
├───────────────────────────────────────────┤
│  ▌ FUAR KATILIMI                          │  ← DUYURU HANESİ
│  ▌ MRO Middle East 2026        STAND      │
│  ▌ 3–4 Şubat 2026 · Dubai      B-114      │
├───────────────────────────────────────────┤
│  UYARI: Bu elektronik posta ve ekleri...  │
└───────────────────────────────────────────┘
```

## ⭐ En önemli kural: dosya adı `imza-duyuru.png` olarak KALMALI

Duyuru görseli imzanın içine gömülmez — **sunucudan çekilir.** Bu sayede:

> Dosyayı **aynı adla** değiştirdiğinizde, imzasını çoktan kopyalamış olan
> **herkesin Outlook'undaki duyuru da kendiliğinden değişir.**
> Kimsenin imzasını yeniden oluşturmasına gerek kalmaz.

Dosya adını değiştirirseniz bu özellik bozulur ve 100+ kişiye
"imzanızı yenileyin" maili atmanız gerekir. **Değiştirmeyin.**

## 1. Duyuru görselini hazırlama

| Kural | Değer |
|---|---|
| Ölçü | **1240 × 160 piksel** (imzada 620 × 80 görünür) |
| Format | PNG |
| Dosya adı | `imza-duyuru.png` |
| Dosya boyutu | 300 KB altı olsun (mailde hızlı yüklensin) |

Depodaki **`ornek-duyuru.png`** hazır bir şablondur — Canva'ya yükleyip
üstündeki yazıları değiştirerek kullanabilirsiniz.
(Kurumsal dil: Montserrat, Bonair kırmızısı `#E2201C`, beyaz zemin.)

## 2. Duyuruyu AÇMA

**Adım 1 — Görseli yükleyin**

1. https://github.com/bonair-code/bonair-mail-imza adresine gidin
2. Üstteki **Add file ▾ → Upload files**
3. Hazırladığınız görseli sürükleyin — **adı `imza-duyuru.png` olmalı**
4. Altta **Commit changes**

**Adım 2 — Duyuruyu aktif edin**

1. `index.html` dosyasına tıklayın → sağ üstteki **kalem (✏️)**
2. **Ctrl+F** ile `aktif:` aratın, şu bloğu bulun:

```js
var DUYURU = {
  aktif: false,                 // duyuru yayinda mi?
  img:   'imza-duyuru.png',     // DEGISTIRMEYIN
  url:   '',                    // tiklaninca gidecek adres (bos ise link olmaz)
  alt:   'Bonair duyuru'        // gorsel yuklenmezse gorunecek yazi
};
```

3. `false` → **`true`** yapın
4. Tıklanınca bir yere gitsin istiyorsanız `url` kısmını doldurun:
   `url: 'https://bonair.com.tr/fuar',` — istemiyorsanız boş bırakın
5. **Commit changes**

**Adım 3 — Kontrol**

1–2 dakika sonra siteyi **Ctrl+F5** ile açın, imzayı oluşturun; duyuru
görünüyor olmalı.

## 3. Duyuruyu KAPATMA

Kapatma **iki yerden** yapılır, çünkü iki ayrı kitle var:

| Kim | Ne yapmalı | Niçin |
|---|---|---|
| **Bundan sonra** imza oluşturacaklar | `index.html` → `aktif: true` → **`false`** | Yeni imzalarda duyuru hiç eklenmez |
| İmzasını **zaten kopyalamış** olanlar | `imza-duyuru-bos.png`'i indirip adını `imza-duyuru.png` yapıp yükleyin | Onların imzasındaki görsel boşalır |

İkisini birlikte yapın; duyuru tamamen kalkar.

> `imza-duyuru-bos.png` depoda hazır duruyor — tamamen şeffaf bir görsel.
> İndirip adını değiştirip yüklemeniz yeterli.
>
> ⚠️ Kapattıktan sonra eski imzalarda duyurunun yerinde ~80px'lik **boş bir
> alan** kalır. Gözle fark edilmez (hemen altında gizlilik metni var).
> Tamamen sıfırlamak isterseniz tek bir "imzanızı yenileyin" maili gerekir.

## 4. Bilinmesi gerekenler

- **Outlook harici görselleri bloklayabilir.** Alıcı sizi tanımıyorsa duyuru
  yerine boş kutu görüp "Resimleri indir"e basması gerekebilir. Mevcut
  sosyal medya ikonlarında da aynı durum var — yeni bir sorun değil.
- Görseli **çok yazıyla doldurmayın.** İmzada 620px genişliğinde görünür;
  3 satırdan fazlası okunmaz.
- Duyuru **herkeste otomatik** çıkar; kişi başına açıp kapatma yoktur.

---

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
| `imza-duyuru.png` | **Geçici duyuru görseli** — bkz. "Geçici duyuru hanesi" |
| `imza-duyuru-bos.png` | Duyuruyu kapatmak için şeffaf yedek görsel |
| `ornek-duyuru.png` | Duyuru için hazır tasarım şablonu |
| `imza-ig / in / globe / pdf .png` | Sosyal ve link ikonları (tıklanabilir) |
| `fonts/` | Montserrat yazı tipi (imza fotoğrafında kullanılır) |
| `firebase.json`, `.firebaserc` | Firebase Hosting ayarları |

### Şablon görselini değiştirmek

`imza-sablon.png` dosyası; logo, hangar çizimi, iletişim ikonları ve
adres satırını içerir. Kişisel bilgiler (ad, unvan, e-posta, telefon)
bunun üzerine `index.html` içindeki `DRAW` ayarlarına göre çizilir.
Şablon değişirse `DRAW` içindeki koordinatların (`x`, `by`) yeniden
ayarlanması gerekir.
