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

# 📢 İMZADAKİ DUYURU

İmzanın altında, gizlilik metninin üstünde duran duyuru alanı.
Fuar katılımı, bakım/sistem duyurusu, bayram mesajı — ne isterseniz.

```
┌──────────────────────────────────────┬────┐
│  Talha DUYGU                         │ ig │
│  Technical Quality & SMS Engineer    │ in │
│  +90 546 269 23 09                   │ 🌐 │
│  tduygu@bonair.com.tr                │pdf │
├───────────────────────────────────────────┤
│  ▌ FUAR KATILIMI                          │  ← DUYURU
│  ▌ MRO Middle East 2026        STAND      │
│  ▌ 3–4 Şubat 2026 · Dubai      B-114      │
├───────────────────────────────────────────┤
│  UYARI: Bu elektronik posta ve ekleri...  │
└───────────────────────────────────────────┘
```

## ⚠️ Duyuru BU DEPODAN yönetilmez

Duyuruyu yayınlamak için bu dosyalara dokunmanız **gerekmez**:

> **Portal → Mail İmzası** sayfasından PNG yükleyin. Hepsi bu.
> Deploy yok, GitHub yok, token yok.

Yüklediğiniz görsel, imzasını **daha önce kopyalamış olan herkeste de**
değişir — kimsenin imzasını yenilemesi gerekmez.

Görsel kuralı: **PNG, 1240 × 160 piksel** (imzada 620 × 80 görünür).
Depodaki `ornek-duyuru.png` hazır şablondur; Canva'ya yükleyip yazılarını
değiştirerek kullanabilirsiniz.

## Nasıl çalışıyor?

İmzaya her zaman tek satırlık bir duyuru hanesi konur ve o hane **sabit bir
adrese** bakar:

```
https://firebasestorage.googleapis.com/v0/b/bonappetit-c2db2.firebasestorage.app/o/mail-imza%2Fduyuru.png?alt=media
```

Portaldan yeni görsel yüklendiğinde aynı adrese yazıldığı için, o adrese
bakan **bütün imzalar** aynı anda güncellenir.

**Duyuru yokken** bu adreste 1240×2 şeffaf bir görsel durur; imzada yüksekliği
~1px olur, yani görünmez. Bu yüzden duyuru hanesine `height` attribute'u
**bilerek verilmiyor** — sabit yükseklik verilseydi duyuru kapalıyken her
imzada 80px boş bir şerit kalırdı.

| Parça | Nerede |
|---|---|
| Duyuru görseli | Firebase Storage · `mail-imza/duyuru.png` |
| Duyuru bilgisi (link) | Firebase Storage · `mail-imza/duyuru.json` |
| Yükleme ekranı | Portal → Mail İmzası (`bonappetit-web`) |
| Yetki | Müdür/admin, ya da Yetki Matrisi'nden `mailImza` |
| Kural | `bonappetit-web/storage.rules` → `match /mail-imza/{fileName}` |

Storage'daki `mail-imza/` klasörü, o kural dosyasındaki **tek herkese açık
yoldur**: mail istemcilerinin Firebase oturumu olmadığı için görselin
kimlik aramayan bir adresten servis edilmesi gerekir. Kapsam iki dosyalık
beyaz listeyle sınırlıdır; başka bir ad yazılamaz ve okunamaz.

## Bilinmesi gerekenler

- **Outlook harici görselleri bloklayabilir.** Alıcı sizi tanımıyorsa duyuru
  yerine boş kutu görüp "Resimleri indir"e basması gerekebilir. Mevcut
  sosyal medya ikonlarında da aynı durum var — yeni bir sorun değil.
- Görseli **çok yazıyla doldurmayın.** İmzada 620px genişliğinde görünür;
  3 satırdan fazlası okunmaz.
- Duyuru **herkeste otomatik** çıkar; kişi başına açıp kapatma yoktur.
- Değişiklik imzalara **5 dakika içinde** yansır (görselin önbellek süresi).

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
| `ornek-duyuru.png` | Duyuru için hazır tasarım şablonu (1240×160) |
| `imza-ig / in / globe / pdf .png` | Sosyal ve link ikonları (tıklanabilir) |
| `fonts/` | Montserrat yazı tipi (imza fotoğrafında kullanılır) |
| `firebase.json`, `.firebaserc` | Firebase Hosting ayarları |

### Şablon görselini değiştirmek

`imza-sablon.png` dosyası; logo, hangar çizimi, iletişim ikonları ve
adres satırını içerir. Kişisel bilgiler (ad, unvan, e-posta, telefon)
bunun üzerine `index.html` içindeki `DRAW` ayarlarına göre çizilir.
Şablon değişirse `DRAW` içindeki koordinatların (`x`, `by`) yeniden
ayarlanması gerekir.
