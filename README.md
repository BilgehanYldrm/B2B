# 🏢 Kurumsal B2B Çok Kiracılı (Multi-Tenant) E-Ticaret ve Tedarik Zinciri Platformu

![PHP](https://img.shields.io/badge/PHP-8.x-777BB4?style=flat-square&logo=php&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-10.x-FF2D20?style=flat-square&logo=laravel&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-Relational-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Bootstrap](https://img.shields.io/badge/UI-Bootstrap%20%2F%20Blade-7952B3?style=flat-square&logo=bootstrap&logoColor=white)
![Architecture](https://img.shields.io/badge/Mimari-Multi--Tenant%20Isolation-blue?style=flat-square)
![Security](https://img.shields.io/badge/Uyumluluk-KVKK%20%2F%20Bot%20Protection-success?style=flat-square)

Toptancı, distribütör ve kurumsal bayiler arasındaki tedarik zincirini, toptan sipariş süreçlerini ve mağaza içi operasyonları dijitalleştirmek üzere geliştirilmiş çok kiracılı (multi-tenant) B2B e-ticaret yönetim platformudur. 

Sistem; bağımsız mağaza/bayi izolasyonu, toptancı onaylı sipariş kilit mekanizması, dinamik iskonto/fiyatlandırma, çoklu depo stok hareketleri ve resmi iade-fatura süreçlerini tek bir çatı altında toplar.

---

## 📌 Temel Sistem Yetenekleri ve Modüller

### 1. Çok Kiracılı Mimari & Veri İzolasyonu (Multi-Tenancy)
* **Tenant İzolasyonu:** Her bayi ve toptancı organizasyonu için veritabanı sorgu katmanında tam veri ayrımı ve bağımsız yetkilendirme.
* **Üç Aşamalı Giriş Alanı:** Bayi/Müşteri portalı, Toptancı operasyon yönetim paneli ve Süper Yönetici (Admin) denetim konsolu.
* **Rol ve İzin Yönetimi (RBAC):** Personel, depo sorumlusu, muhasebe ve mağaza yöneticileri için granüler yetki tanımları.

### 2. Toptancı Kilidi & Dinamik Fiyatlandırma Motoru
* **Bayi Bazlı Fiyat Listeleri:** Müşteri/bayi grubuna göre dinamik iskonto oranları, vadeli ödeme seçenekleri ve minimum sipariş kotası belirleme.
* **Sipariş Kilit Mekanizması:** Toptancı onayı gerektiren siparişlerde onay verilene kadar siparişin kilitlenmesi ve stok rezervasyonunun kontrollü yürütülmesi.

### 3. Çoklu Depo, Ürün & Stok Hareketleri
* **Depo Yönetimi:** Birden fazla fiziksel şube/depo tanımlama ve depolar arası transfer takibi.
* **Stok Hareket Geçmişi:** Giriş, çıkış, sayım farkı ve rezerve stok hareketlerinin zaman damgalı loglanması.
* **Kategori & Varyant Hiyerarşisi:** Marka, kategori, SKU ve barkod bazlı ürün katalog yönetimi ile varyantlı ürün desteği.

### 4. İade, Fatura ve Finansal Mutabakat
* **Gelişmiş İade Süreçleri:** Mağaza veya müşteri adına iade talepleri, iadesiz bakiye/para iadesi süreçleri ve iade faturası kaydı.
* **Fatura ve Muhasebe Uyum:** Resmi e-arşiv ve e-fatura süreçlerine uygun cari hareket dökümleri ve borç/alacak takibi.

### 5. Güvenlik, Yasal Metinler ve Bot Koruması
* **KVKK & Yasal Uyumluluk:** Açık rıza metinleri, mesafeli satış sözleşmeleri, aydınlatma bildirimleri ve dinamik çerez onay mekanizması.
* **Bot Koruması & İstek Sınırlandırma (Rate Limiting):** Yetkisiz veri kazıma (scraping) ve brute-force girişimlerini engelleyen güvenlik filtreleri.

---

## 🏗️ Mimari ve Bileşenler

| Katman | Teknoloji | İşlev |
| :--- | :--- | :--- |
| **Arka Yüz (Backend)** | PHP / Laravel (MVC) | Servis odaklı iş mantığı katmanı, Eloquent ORM ve middleware filtreleri |
| **Ön Yüz (Frontend)** | Blade, Bootstrap, Vite | Kurumsal B2B vitrini, duyarlı kontrol panelleri ve modüler arayüzler |
| **Veritabanı** | MySQL / PostgreSQL | Çok kiracılı ilişkisel model, indekslenmiş foreign key ilişkileri |
| **Güvenlik** | CSRF, Rate Limiting, RBAC | Tenant ID doğrulaması, policy & gate tabanlı yetki denetimi |
| **Depolama & Loglama** | Local / Cloud Storage | Sistem işlem kayıtları, fatura belgeleri ve ürün medya yönetimi |

---

## 📂 Proje Dizin Mimarisi

```text
.
├── app/
│   ├── Http/Controllers/     # Bayi, Toptancı ve Admin paneli denetleyicileri
│   ├── Models/               # Tenant, Ürün, Stok ve Sipariş ilişkisel modelleri
│   ├── Services/             # İade, stok hareketleri ve sipariş hesaplama servisleri
│   └── Policies/             # Çok kiracılı erişim denetim kuralları
├── bootstrap/                # Uygulama çekirdek yükleyicisi ve önbellek yapılandırması
├── config/                   # Veritabanı, oturum ve sistem parametreleri
├── database/
│   ├── migrations/           # Veritabanı şema tabloları
│   └── seeders/              # Rol, izin ve varsayılan sistem verileri
├── docs/                     # Sistem analiz ve mimari dokümantasyonu
├── lang/tr/                  # Türkçe arayüz, bildirim ve yasal metin çevirileri
├── public/                   # Web sunucusu giriş noktası ve derlenmiş varlıklar
├── resources/                # Blade şablonları, stil (CSS) ve script bileşenleri
├── routes/
│   ├── web.php               # B2B vitrin ve müşteri rotaları
│   ├── admin.php             # Toptancı ve sistem yöneticisi yönetim rotaları
│   └── api.php               # Entegrasyon ve harici veri uç noktaları
└── tests/                    # Birim ve entegrasyon test senaryoları