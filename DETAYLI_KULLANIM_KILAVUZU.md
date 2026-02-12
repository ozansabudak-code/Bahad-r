# 📚 Tedarikçi Performans Analiz Sistemi - Detaylı Kullanım Kılavuzu

## 📖 İçindekiler

1. [Giriş ve Genel Bakış](#giriş-ve-genel-bakış)
2. [Sistem Gereksinimleri](#sistem-gereksinimleri)
3. [İlk Kurulum ve Yapılandırma](#ilk-kurulum-ve-yapılandırma)
4. [Ana Ekran ve Menü Yapısı](#ana-ekran-ve-menü-yapısı)
5. [Tüm Sekmeler Detaylı Kullanım](#tüm-sekmeler-detaylı-kullanım)
6. [Yapay Zeka Özellikleri](#yapay-zeka-özellikleri)
7. [Adım Adım Kullanım Senaryoları](#adım-adım-kullanım-senaryoları)
8. [Sık Sorulan Sorular](#sık-sorulan-sorular)
9. [Sorun Giderme](#sorun-giderme)

---

## 🎯 Giriş ve Genel Bakış

### Uygulama Hakkında

**Tedarikçi Performans Analiz Sistemi**, Defacto'nun tedarikçi performansını analiz eden, yapay zeka destekli bir masaüstü uygulamasıdır.

### Ana Özellikler

✅ **Otomatik Veri Yükleme** - Excel dosyalarından otomatik veri çekme
✅ **Çok Boyutlu Analiz** - Teslimat, kalite, fiyat, şikayet analizi
✅ **Yapay Zeka Desteği** - Gemini 2.0 Flash ile akıllı analizler
✅ **Email Otomasyonu** - AI destekli email oluşturma ve yönetimi
✅ **Doğal Dil Sorguları** - Türkçe sorularla veri sorgulama
✅ **Akıllı Eylem Önerileri** - Proaktif problem çözme
✅ **Görsel Raporlama** - Grafikler ve göstergeler
✅ **Sektör Haberleri** - Anlık bilgi akışı

---

## 💻 Sistem Gereksinimleri

### Minimum Gereksinimler

- **İşletim Sistemi:** Windows 10/11, macOS 10.14+, Linux
- **Python:** 3.8 veya üzeri
- **RAM:** 4 GB
- **Disk Alanı:** 500 MB
- **İnternet:** Yapay zeka özellikleri için gerekli

### Gerekli Kütüphaneler

```
tkinter (GUI)
pandas (Veri işleme)
numpy (Hesaplamalar)
matplotlib (Grafikler)
google-generativeai (AI - Gemini)
requests (API çağrıları)
openpyxl (Excel okuma)
Pillow (Görüntü işleme)
```

---

## 🚀 İlk Kurulum ve Yapılandırma

### 1. Uygulama Başlatma

```bash
python tedarikci_rapor_gui_auto.py
```

### 2. İlk Açılışta Yapılacaklar

**a) API Anahtarı Yapılandırması (AI Özellikleri İçin)**

Kod içinde 95. satırda:
```python
GEMINI_API_KEY = "BURAYA_API_ANAHTARINIZI_YAZIN"
```

**API Anahtarı Alma:**
1. https://makersuite.google.com/app/apikey adresine gidin
2. Google hesabınızla giriş yapın
3. "Create API Key" butonuna tıklayın
4. Oluşturulan anahtarı kopyalayın
5. Koda yapıştırın

**b) Email Yapılandırması (Email Özellikleri İçin)**

Kod içinde 102-103. satırda:
```python
GMAIL_USER = "email@gmail.com"
GMAIL_APP_PASSWORD = "uygulama_sifresi"
```

**Gmail Uygulama Şifresi Alma:**
1. Google Hesap ayarlarına gidin
2. Güvenlik → 2 Adımlı Doğrulama
3. Uygulama şifreleri
4. "Posta" için şifre oluşturun
5. Oluşturulan şifreyi kopyalayın

### 3. Veri Kaynakları

Uygulama şu konumlardaki dosyaları otomatik okur:

**Merkezi Konumlar:**
- `X:\01.Public\TEDARİKÇİ PERFORMANS\Tedarik\Tedarik AI.xlsx`
- `X:\01.Public\TEDARİKÇİ PERFORMANS\Reklamasyon\Reklamasyon.xlsx`

**Alternatif (Manuel Yükleme):**
- Masaüstü veya herhangi bir konum
- "Veri Yükle" butonu ile manuel seçim

---

## 📱 Ana Ekran ve Menü Yapısı

### Sol Menü (Gezinme)

```
📊 Ana Sayfa
├── Genel bakış ve özetler
├── Hızlı istatistikler
└── Son analizler

📈 Analiz
├── Detaylı performans analizi
├── Grafikler ve tablolar
└── Filtreleme seçenekleri

🤖 YZ Raporu
├── AI destekli analiz sonuçları
├── Öneriler ve içgörüler
└── 🔮 Tahmine Dayalı Risk Analizi

📧 Akıllı Email (AI)
├── AI ile email oluşturma
├── 8 farklı senaryo
└── Otomatik profesyonel yazışma

📥 Email Gelen Kutusu
├── Email okuma ve yanıtlama
├── Thread yönetimi
└── AI destekli yanıt hazırlama

🗣️ Doğal Dil Sorguları (AI)
├── Türkçe soru sorma
├── Anlık cevaplar
└── Veri sorgulama

🎯 Akıllı Eylem Önerileri (AI)
├── Otomatik problem tespiti
├── AI önerileri
└── Öncelikli aksiyonlar

📰 Sektör Haberleri
├── Güncel haberler
├── Filtreleme
└── Detay görüntüleme
```

---

## 📑 Tüm Sekmeler Detaylı Kullanım

## 1️⃣ Ana Sayfa

### Amaç
Genel performans özeti ve hızlı erişim noktası.

### Özellikler

**Üst Bilgi Kartları:**
- 📊 Toplam Tedarikçi Sayısı
- ✅ Başarılı Teslimat Oranı
- ⭐ Ortalama Kalite Skoru
- 📦 Toplam İade Oranı

**Grafikler:**
- Teslimat performansı dağılımı
- Kalite skoru histogramı
- Kategori bazlı analiz

**Hızlı İşlemler:**
- Veri yenileme
- Son analiz tarihi
- Otomatik güncelleme ayarı

### Kullanım

```
1. Uygulamayı açın
2. Otomatik veri yükleme başlar
3. Ana sayfa kartları güncellenir
4. Genel durumu inceleyin
5. Detay için diğer sekmelere geçin
```

---

## 2️⃣ Analiz Sekmesi

### Amaç
Detaylı tedarikçi performans analizi ve filtreleme.

### Özellikler

**Filtreleme Seçenekleri:**
- 🔍 Tedarikçi ara (isim veya kod)
- 📅 Tarih aralığı seçimi
- 📊 Performans aralığı
- 🏷️ Kategori seçimi
- ⚠️ Aykırı değer filtresi

**Analiz Türleri:**
- **Teslimat Performansı:** Zamanında teslimat oranı
- **Kalite Skoru:** Ürün kalitesi değerlendirmesi
- **İade Oranı:** Geri gönderim yüzdesi
- **Fiyat Karşılaştırması:** Rekabetçi fiyatlandırma
- **Şikayet Analizi:** Müşteri şikayetleri

**Görselleştirmeler:**
- Bar grafikleri
- Pasta grafikleri
- Çizgi grafikleri
- Dağılım grafikleri
- Isı haritaları

### Kullanım Adımları

```
📝 Adım 1: Filtreleme
1. Sol panelden filtre kriterlerini seçin
2. Tedarikçi ismi veya kodu girin
3. Tarih aralığını belirleyin
4. "Filtrele" butonuna tıklayın

📊 Adım 2: Analiz
1. Analiz sonuçları tabloda görünür
2. Grafikleri inceleyin
3. Detaylı bilgi için satıra tıklayın
4. Excel'e aktarmak için "Export" butonunu kullanın

🔄 Adım 3: Güncelleme
1. Veriyi yenilemek için "Yenile" butonuna tıklayın
2. Otomatik güncelleme için checkbox'ı işaretleyin
```

### İpuçları

💡 **Aykırı Değer Filtresi:** Anormal verileri görmezden gelmek için
💡 **Çoklu Seçim:** Ctrl tuşuyla birden fazla tedarikçi seçin
💡 **Excel Export:** Sonuçları başkalarıyla paylaşın

---

## 3️⃣ YZ Raporu (AI Raporu)

### 🤖 YAPAY ZEKA KULLANIMI #1

### Amaç
Gemini AI kullanarak tedarikçi verilerini analiz eder ve içgörüler üretir.

### AI Motor: Google Gemini 2.0 Flash

**Kullanılan Model:** `models/gemini-2.0-flash`

**AI Ne Yapar:**
- Tedarikçi verilerini analiz eder
- Performans trendlerini tespit eder
- Güçlü ve zayıf yönleri belirler
- Türkçe rapor oluşturur
- Stratejik öneriler sunar

### Özellikler

**Otomatik AI Analizi:**
- Tedarikçi profilleme
- Trend analizi
- Karşılaştırmalı değerlendirme
- Risk değerlendirmesi

**Rapor Bölümleri:**
1. **Genel Değerlendirme** - Özet durum
2. **Güçlü Yönler** - Başarılı alanlar
3. **Zayıf Yönler** - İyileştirilmesi gereken alanlar
4. **Öneriler** - Aksiyon önerileri
5. **Gelecek Beklentisi** - Tahminler

**🔮 Tahmine Dayalı Risk Analizi Butonu**

### 🤖 YAPAY ZEKA KULLANIMI #2

Bu butona tıklandığında:
- AI geçmiş verileri analiz eder
- Gelecekteki riskleri tahmin eder
- Risk skorları oluşturur
- Önleyici aksiyonlar önerir

### Kullanım

```
🚀 Adım 1: Rapor Oluşturma
1. "YZ Raporu" sekmesine geçin
2. Tedarikçi seçin
3. "AI Rapor Oluştur" butonuna tıklayın
4. AI analiz yapar (10-15 saniye)
5. Rapor ekranda görünür

🔮 Adım 2: Risk Analizi
1. "🔮 Tahmine Dayalı Risk Analizi" butonuna tıklayın
2. AI geçmiş verileri analiz eder
3. Gelecek riskler tahmin edilir
4. Risk skorları ve öneriler gösterilir

💾 Adım 3: Kaydetme
1. Raporu PDF olarak kaydedin
2. Veya metni kopyalayın
3. Başkalarıyla paylaşın
```

### AI Prompt Yapısı (Teknik)

```python
prompt = f"""
Tedarikçi Analizi: {tedarikçi_adı}

Veriler:
- Teslimat Performansı: {performans}
- Kalite Skoru: {kalite}
- İade Oranı: {iade}
...

Lütfen detaylı bir Türkçe analiz raporu oluştur.
"""
```

---

## 4️⃣ Akıllı Email (Smart Email)

### 🤖 YAPAY ZEKA KULLANIMI #3

### Amaç
Gemini AI ile profesyonel Türkçe emailler otomatik oluşturur.

### AI Motor: Google Gemini 2.0 Flash

**AI Ne Yapar:**
- Senaryoya uygun email içeriği üretir
- Profesyonel ton kullanır
- Türkçe dil bilgisi kurallarına uyar
- Tedarikçi bilgilerini entegre eder
- Uygun konu başlığı oluşturur

### 8 Email Senaryosu

#### 1. 📦 Teslimat Gecikmesi
**Ne zaman kullanılır:** Sipariş gecikmelerinde
**AI'nin yaptığı:**
- Gecikme süresini analiz eder
- Kibar ama kararlı ton kullanır
- Aciliyet ifade eder
- Çözüm talep eder

**Örnek:**
```
Konu: Teslimat Gecikmesi Takibi - Sipariş #12345

Sayın [Tedarikçi],

DF-2024-12345 numaralı siparişinizin teslimat tarihinin 3 gün 
geçmiş olmasına rağmen henüz teslim alınamadığını üzülerek 
belirtmek isteriz.

Mevcut durum hakkında acil bilgilendirme bekliyoruz.

Saygılarımızla,
Defacto Tedarik Zinciri Ekibi
```

#### 2. ⚠️ Kalite Sorunu
**Ne zaman kullanılır:** Ürün kalitesi problemlerinde
**AI'nin yaptığı:**
- Sorunu net açıklar
- Beklentileri bildirir
- Düzeltici aksiyon ister

#### 3. 💰 Fiyat Görüşmesi
**Ne zaman kullanılır:** Fiyat pazarlığı için
**AI'nin yaptığı:**
- Rekabetçi fiyat vurgular
- İş birliği önerir
- Uzun vadeli ilişki vurgular

#### 4. 📅 Toplantı Daveti
**Ne zaman kullanılır:** Performans görüşmesi için
**AI'nin yaptığı:**
- Kibar davet dili
- Tarih/saat önerileri
- Gündem maddelerini belirtir

#### 5. 📄 Eksik Evrak Hatırlatma
**Ne zaman kullanılır:** Belge eksikliklerinde
**AI'nin yaptığı:**
- Eksik belgeler listeler
- Son tarih belirtir
- İş akışı önemini vurgular

#### 6. 📊 Performans Değerlendirmesi
**Ne zaman kullanılır:** Periyodik raporlama için
**AI'nin yaptığı:**
- Objektif değerlendirme
- Güçlü yönler vurgular
- İyileştirme alanları belirtir

#### 7. 🙏 Teşekkür / Takdir
**Ne zaman kullanılır:** Başarılı iş için
**AI'nin yaptığı:**
- Samimi teşekkür
- Başarıyı detaylandırır
- Gelecek beklentisi

#### 8. ⚡ Uyarı / Escalation
**Ne zaman kullanılır:** Ciddi problemlerde
**AI'nin yaptığı:**
- Net uyarı
- Sonuçları bildirir
- Acil aksiyon talep eder

### Kullanım

```
📧 Adım 1: Senaryo Seçimi
1. "📧 Akıllı Email" sekmesine gidin
2. 8 senaryodan birini seçin (radio button)

🏢 Adım 2: Tedarikçi Seçimi
1. Dropdown'dan tedarikçi seçin
2. Otomatik bilgileri doldurur

📝 Adım 3: Bağlam Ekleme (Opsiyonel)
1. Ek detaylar girin
2. Sipariş numarası, tarih vb.

🤖 Adım 4: AI ile Oluşturma
1. "🤖 Email Oluştur" butonuna tıklayın
2. AI email üretir (5-10 saniye)
3. Email önizlemede görünür

✏️ Adım 5: Düzenleme ve Gönderme
1. Email içeriğini düzenleyin
2. Konu başlığını kontrol edin
3. "📧 Email Gönder" butonuna tıklayın
4. Veya "💾 Taslak Kaydet" ile kaydedin
```

### AI Prompt Örneği

```python
scenario_prompts = {
    "teslimat_gecikmesi": """
    Senaryo: Teslimat Gecikmesi
    Tedarikçi: {supplier_name}
    Gecikme: {delay_days} gün
    Sipariş: {order_number}
    
    Lütfen profesyonel bir Türkçe email oluştur:
    - Kibar ama kararlı
    - Durumu net açıkla
    - Acil çözüm talep et
    - İş ilişkisini koru
    """
}
```

### Başarı Kriterleri

✅ Email 100% Türkçe
✅ Profesyonel ton
✅ Dilbilgisi kurallarına uygun
✅ Bağlama uygun içerik
✅ Aksiyon odaklı

---

## 5️⃣ Email Gelen Kutusu

### Amaç
Gmail hesabınızdan emaill okuma ve yanıtlama. Program içinden email yönetimi.

### Özellikler

**Email Okuma (IMAP):**
- Gmail'den otomatik çekme
- 50 en son email
- Konu, gönderen, tarih gösterimi
- Okundu/Okunmadı işaretleme
- Thread yönetimi

**Email Yanıtlama:**
- Direkt yanıt
- Orijinal mesajı alıntılama
- 🤖 **AI ile Yanıt Hazırlama**

### 🤖 YAPAY ZEKA KULLANIMI #4

**AI Destekli Yanıt:**
- "🤖 AI ile Hazırla" butonu
- Orijinal emaili analiz eder
- Uygun yanıt oluşturur
- Türkçe, profesyonel

### Kullanım

```
📥 Adım 1: Email Çekme
1. "📥 Email Gelen Kutusu" sekmesine gidin
2. "🔄 Yenile" butonuna tıklayın
3. Gmail'den emailler çekilir (5-10 saniye)
4. Liste görünür

📧 Adım 2: Email Okuma
1. Listeden bir email seçin
2. İçerik sağda görünür
3. Otomatik "okundu" işaretlenir

💬 Adım 3: Yanıtlama
1. "💬 Cevapla" butonuna tıklayın
2. Yanıt penceresi açılır
3. İki seçenek:
   a) Manuel yazın
   b) "🤖 AI ile Hazırla" butonuna tıklayın

🤖 Adım 4: AI Yanıt (Opsiyonel)
1. "🤖 AI ile Hazırla" tıklayın
2. AI orijinal emaili analiz eder
3. Uygun yanıt üretir (10 saniye)
4. Düzenleyin
5. "📧 Gönder" butonuna tıklayın

🔍 Adım 5: Filtreleme
1. "✓ Sadece Okunmamış" checkbox'ını işaretleyin
2. Sadece yeni emailler görünür
```

### Email Database

Emailler yerel SQLite veritabanında saklanır:
- `email_inbox.db`
- Offline erişim
- Hızlı arama
- Thread takibi

---

## 6️⃣ Doğal Dil Sorguları

### 🤖 YAPAY ZEKA KULLANIMI #5

### Amaç
Türkçe soru sorarak verileri sorgulama. SQL bilgisi gerektirmez!

### AI Motor: Google Gemini 2.0 Flash

**AI Ne Yapar:**
- Türkçe soruyu anlar
- Veritabanı yapısını bilir
- Uygun sorgu oluşturur
- Sonuçları Türkçe açıklar
- Görselleştirme önerir

### Örnek Sorular

```
❓ "En iyi 5 tedarikçiyi göster"
❓ "Teslimat performansı 80'in altında olan tedarikçiler kimler?"
❓ "Bu ayki kalite skorları nasıl?"
❓ "Geçen aya göre performans değişimi nedir?"
❓ "Hangi kategoride en çok problem var?"
❓ "Toplam iade oranı nedir?"
❓ "En pahalı tedarikçiler hangileri?"
❓ "Son 3 ayda en çok şikayet alan tedarikçi?"
```

### Kullanım

```
🗣️ Adım 1: Soru Sorma
1. "🗣️ Doğal Dil Sorguları" sekmesine gidin
2. Soru kutusuna Türkçe sorunuzu yazın
3. Enter'a basın veya "🔍 Sorgula" butonuna tıklayın

🤖 Adım 2: AI İşleme
1. AI soruyu analiz eder (5 saniye)
2. Veritabanını sorgular
3. Sonuçları hazırlar

📊 Adım 3: Sonuçlar
1. Cevap metni görünür
2. Varsa tablo gösterilir
3. Varsa grafik oluşturulur
4. Açıklama eklenir

💡 Adım 4: Takip Soruları
1. Sonucu gördükten sonra
2. Detay için yeni soru sorun
3. "Bunların detaylarını göster" gibi
```

### AI Prompt Yapısı

```python
prompt = f"""
Veritabanı Şeması:
- Tedarikçiler tablosu
- Teslimat_performansı sütunu
- Kalite_skoru sütunu
...

Kullanıcı Sorusu: "{user_question}"

Lütfen:
1. Soruyu analiz et
2. Uygun SQL sorgusu oluştur
3. Sonuçları Türkçe açıkla
"""
```

### Desteklenen Soru Tipleri

✅ Filtreleme soruları
✅ Sıralama soruları
✅ Karşılaştırma soruları
✅ İstatistik soruları
✅ Trend soruları
✅ Top N soruları

---

## 7️⃣ Akıllı Eylem Önerileri

### 🤖 YAPAY ZEKA KULLANIMI #6

### Amaç
Tedarikçi problemlerini otomatik tespit edip çözüm önerileri sunar.

### AI Motor: Google Gemini 2.0 Flash

**AI Ne Yapar:**
- Verileri sürekli izler
- Problemleri otomatik tespit eder
- Önem seviyesi belirler
- Spesifik aksiyonlar önerir
- Zaman çizelgesi oluşturur

### Problem Tespit Kuralları

**6 Tür Problem:**

1. **📉 Düşük Teslimat Performansı**
   - Kural: < 70%
   - Kritik seviye: < 50%

2. **⚠️ Kalite Skoru Düşük**
   - Kural: < 75
   - Kritik seviye: < 60

3. **🔄 Yüksek İade Oranı**
   - Kural: > 5%
   - Kritik seviye: > 10%

4. **💰 Fiyat Artışı**
   - Kural: > 10% artış
   - Kritik seviye: > 20%

5. **📝 Çok Şikayet**
   - Kural: > 3 şikayet
   - Kritik seviye: > 5

6. **📄 Eksik Evraklar**
   - Kural: Herhangi eksik
   - Kritik seviye: 3+ eksik

### 4 Öncelik Seviyesi

**🔴 KRİTİK (Critical)**
- Acil müdahale gerekli
- Aynı gün içinde aksiyon
- Kırmızı renk kodlu

**🟠 YÜKSEK (High)**
- Yakında aksiyon gerekli
- Bu hafta içinde
- Turuncu renk kodlu

**🟡 ORTA (Medium)**
- Önemli ama acil değil
- Bu ay içinde
- Sarı renk kodlu

**🟢 DÜŞÜK (Low)**
- Planlanabilir
- Önümüzdeki dönem
- Yeşil renk kodlu

### Kullanım

```
🎯 Adım 1: Sekmeyi Açma
1. "🎯 Akıllı Eylem Önerileri" sekmesine gidin
2. Otomatik analiz başlar (10-15 saniye)

🤖 Adım 2: AI Analizi
1. AI tüm tedarikçileri tarar
2. Problemleri tespit eder
3. Öneriler oluşturur
4. Önceliklere göre gruplar

📊 Adım 3: Önerileri İnceleme
1. Her öncelik seviyesine bakın
2. Kırmızılarla başlayın (kritik)
3. Her kart bir problem gösterir

📋 Adım 4: Aksiyon Kartları
Her kart gösterir:
- Problem açıklaması
- Etkilenen tedarikçi
- Metrik değerler
- 3-5 spesifik aksiyon
- Zaman çizelgesi
- Tamamla/Kapat butonları

✅ Adım 5: Tamamlama
1. Aksiyonu yaptınız mı?
2. "✓ Tamamlandı" butonuna tıklayın
3. Kart işaretlenir
4. Veya "🗑️ Kapat" ile kapatın

🔄 Adım 6: Yenileme
1. "🔄 Yenile" butonuna tıklayın
2. AI yeniden analiz yapar
3. Güncel öneriler görünür
```

### AI Öneri Örneği

```
🔴 KRİTİK EYLEM

⚠️ Problem: Kalite Skoru Düşük
Tedarikçi: ABC Tekstil
Metrik: Kalite skoru 58 (hedef: 75+)

Önerilen Aksiyonlar:
1. Acil kalite denetimi planla (Bu hafta)
2. Üretim sürecini detaylı incele
3. Kalite kontrol protokollerini gözden geçir
4. Alternatif tedarikçi araştır
5. Performans iyileştirme planı talep et

⏰ Zaman Çizelgesi: Hemen
📈 Beklenen İyileşme: +20 puan

[✓ Tamamlandı] [🗑️ Kapat]
```

### Proaktif Yönetim

Bu özellik sayesinde:
- ✅ Sorunlar büyümeden önce tespit edilir
- ✅ Sistematik çözüm yaklaşımı
- ✅ Hiçbir şey atlanmaz
- ✅ Zamanında müdahale
- ✅ Performans iyileşir

---

## 8️⃣ Sektör Haberleri

### Amaç
Tekstil ve tedarik zinciri haberlerini takip etme.

### Özellikler

**Haber Kaynakları:**
- NewsAPI entegrasyonu
- Tekstil sektörü
- Tedarik zinciri
- E-ticaret
- Moda

**Görüntüleme:**
- Başlık ve özet
- Tarih ve kaynak
- Detay butonu
- Tarayıcıda açma

### Kullanım

```
📰 Adım 1: Haberleri Görme
1. "📰 Sektör Haberleri" sekmesine gidin
2. Otomatik haberler yüklenir

🔍 Adım 2: Filtreleme
1. Anahtar kelime girin
2. Tarih aralığı seçin
3. "Filtrele" butonuna tıklayın

📖 Adım 3: Detay
1. Habere tıklayın
2. Tam metin görünür
3. "Tam Haberi Aç" butonu
4. Tarayıcıda açılır

🔄 Adım 4: Yenileme
1. "Yenile" butonuna tıklayın
2. En son haberler çekilir
```

---

## 🤖 Yapay Zeka Özellikleri - Özet

### Tüm AI Kullanımları

| # | Özellik | AI Kullanım Amacı | Model |
|---|---------|-------------------|-------|
| 1 | YZ Raporu | Tedarikçi analizi ve rapor oluşturma | Gemini 2.0 Flash |
| 2 | Risk Tahmini | Gelecek risklerini tahmin etme | Gemini 2.0 Flash |
| 3 | Akıllı Email | Otomatik email içeriği oluşturma | Gemini 2.0 Flash |
| 4 | Email Yanıtlama | Gelen emaillere yanıt hazırlama | Gemini 2.0 Flash |
| 5 | Doğal Dil Sorguları | Türkçe soruları SQL'e çevirme | Gemini 2.0 Flash |
| 6 | Akıllı Eylem Önerileri | Problem tespit ve çözüm önerme | Gemini 2.0 Flash |

### AI Kullanımının Avantajları

✅ **Zaman Tasarrufu:** %90 daha hızlı
✅ **Tutarlılık:** Her zaman profesyonel
✅ **Türkçe Destek:** Doğal dil işleme
✅ **Öğrenme:** Sürekli iyileşir
✅ **24/7:** Her zaman hazır
✅ **Hatasız:** Dilbilgisi kontrolü
✅ **Kişiselleştirme:** Bağlama uygun

### AI Limitasyonları

⚠️ **İnternet Gerekli:** API erişimi için
⚠️ **API Kotası:** Günlük limit var
⚠️ **İnsan Kontrolü:** Sonuçlar kontrol edilmeli
⚠️ **Veri Kalitesi:** Girdi kalitesine bağlı

---

## 📚 Adım Adım Kullanım Senaryoları

### Senaryo 1: Yeni Tedarikçi Değerlendirmesi

```
Amaç: Yeni bir tedarikçiyi sistem üzerinden değerlendirmek

Adımlar:
1. "Analiz" sekmesine git
2. Tedarikçi ismini ara
3. Performans metriklerini incele
4. "YZ Raporu" oluştur
5. AI analizini oku
6. "🔮 Risk Analizi" yap
7. Karar ver: Devam / Red
```

### Senaryo 2: Performans Düşüşüne Müdahale

```
Amaç: Performansı düşen tedarikçiye aksiyonlar

Adımlar:
1. "🎯 Akıllı Eylem Önerileri"ne bak
2. Problemi tespit et
3. AI önerilerini oku
4. "📧 Akıllı Email" ile email hazırla
5. Senaryo: "Performans Değerlendirmesi"
6. AI emaili oluştur
7. Gönder
8. Eylem kartını "✓ Tamamlandı" işaretle
```

### Senaryo 3: Aylık Performans Raporu

```
Amaç: Tüm tedarikçiler için aylık rapor

Adımlar:
1. "Analiz"de tarih filtresini ayarla (son 30 gün)
2. Tüm tedarikçileri görüntüle
3. "Excel'e Aktar" butonuna tıkla
4. Her tedarikçi için "YZ Raporu" oluştur
5. Raporları PDF olarak kaydet
6. Yöneticiye sun
```

### Senaryo 4: Acil Durum Yönetimi

```
Amaç: Kritik problemlere hızlı müdahale

Adımlar:
1. "🎯 Akıllı Eylem Önerileri" sekmesi
2. 🔴 Kritik önerilere odaklan
3. En acil problemi seç
4. AI'nin önerdiği aksiyonları uygula
5. "📧 Akıllı Email" ile uyarı gönder
6. Senaryo: "Uyarı / Escalation"
7. Takip için hatırlatıcı kur
```

### Senaryo 5: Veri Analizi (SQL Bilmeden)

```
Amaç: Veritabanından bilgi çekme

Adımlar:
1. "🗣️ Doğal Dil Sorguları" sekmesi
2. Türkçe sorunuzu yazın
3. Örnek: "En başarılı 10 tedarikçi kimler?"
4. AI sonuçları gösterir
5. Takip sorusu sorun
6. "Bunların ortalama teslimat süresi?"
7. Sonuçları kaydedin
```

---

## ❓ Sık Sorulan Sorular

### Genel Sorular

**S: Uygulama ücretsiz mi?**
C: Evet, ancak Gemini API için Google'dan API key gerekir (ücretsiz plan mevcut).

**S: Offline çalışır mı?**
C: Temel özellikler evet, AI özellikleri için internet gerekir.

**S: Veri güvenli mi?**
C: Evet, tüm veriler yerel olarak saklanır. AI analizleri için sadece özet bilgi gönderilir.

**S: Hangi diller destekleniyor?**
C: Arayüz ve AI Türkçe dilinde çalışır.

### AI Soruları

**S: AI her zaman doğru mu?**
C: Hayır, sonuçları her zaman kontrol edin. AI destek aracıdır, karar verme yetkisi sizde.

**S: API kotam bitti, ne yapmalıyım?**
C: Gemini'nin ücretsiz planında günlük limit var. Ertesi gün sıfırlanır veya ücretli plana geçin.

**S: AI Türkçe'yi iyi biliyor mu?**
C: Evet, Gemini 2.0 Flash Türkçe'de çok başarılı. Dilbilgisi ve ton kontrolü yapar.

**S: AI'ye güvenebilir miyim?**
C: AI yardımcıdır. Kritik kararlar için mutlaka insan kontrolü yapın.

### Teknik Sorular

**S: Uygulama yavaş çalışıyor?**
C: AI işlemleri 5-15 saniye sürebilir. Normal durum. İnternet hızınızı kontrol edin.

**S: Email gönderemiyorum?**
C: Gmail uygulama şifrenizi kontrol edin. 2 adımlı doğrulama aktif olmalı.

**S: Verileri nasıl yedeklerim?**
C: Excel export özelliğini kullanın. Tüm analiz sonuçları kaydedilebilir.

---

## 🔧 Sorun Giderme

### Problem 1: AI Özellikler Çalışmıyor

**Belirtiler:**
- "API_KEY hatası"
- "Gemini yanıt vermiyor"

**Çözüm:**
1. API Key'i kontrol edin (satır 95)
2. İnternet bağlantısını test edin
3. API kotanızı kontrol edin
4. Firewall ayarlarını kontrol edin

### Problem 2: Email Gönderilmiyor

**Belirtiler:**
- "Email gönderme hatası"
- "Authentication failed"

**Çözüm:**
1. Gmail kullanıcı adını kontrol edin
2. Uygulama şifresini kontrol edin
3. 2 adımlı doğrulama aktif mi?
4. SMTP ayarlarını test edin

### Problem 3: Veri Yüklenmiyor

**Belirtiler:**
- "Dosya bulunamadı"
- "Veri yükleme hatası"

**Çözüm:**
1. Dosya yollarını kontrol edin
2. Excel dosyası açık olmasın
3. Okuma izinlerini kontrol edin
4. Manuel yükleme deneyin

### Problem 4: Grafikler Görünmüyor

**Belirtiler:**
- Boş grafik alanları
- "Matplotlib hatası"

**Çözüm:**
1. Matplotlib kurulu mu?
2. Veri var mı?
3. Filtreleri kontrol edin
4. Uygulamayı yeniden başlatın

---

## 📊 Performans İpuçları

### Hızlı Kullanım İpuçları

💡 **Kısayol Tuşları:**
- `Ctrl + R`: Veriyi yenile
- `Ctrl + F`: Ara
- `Ctrl + E`: Excel'e aktar
- `Ctrl + Q`: Çıkış

💡 **Verimli Filtreleme:**
- Tarih aralığını daraltın
- Spesifik tedarikçi seçin
- Sadece gerekli metrikleri görüntüleyin

💡 **AI Kullanımında:**
- Soruları net yazın
- Bağlam bilgisi ekleyin
- Sonuçları kaydedin (tekrar üretilmez)

💡 **Email Yönetimi:**
- Taslakları kaydedin
- Template'ler oluşturun
- Toplu gönderim için liste yapın

---

## 🎓 En İyi Uygulamalar

### Günlük Rutin

```
☀️ Sabah (09:00)
1. Uygulamayı aç
2. Veri otomatik yüklensin
3. "🎯 Akıllı Eylem Önerileri"ni kontrol et
4. Kritik (🔴) önerilere bak
5. Günlük aksiyonları planla

🌅 Öğlen (12:00)
1. "📥 Email Gelen Kutusu"nu kontrol et
2. Acil maillere yanıt ver
3. AI desteği kullan

🌙 Akşam (17:00)
1. "Analiz" sekmesinde günlük özet
2. Tamamlanan aksiyonları işaretle
3. Ertesi gün planla
```

### Haftalık Rutin

```
📅 Pazartesi
- Haftalık hedefler belirle
- "YZ Raporu" oluştur
- Risk analizi yap

📊 Çarşamba
- Performans trend kontrolü
- Problemleri tespit et
- Müdahale planla

📈 Cuma
- Haftalık sonuçları topla
- Raporları hazırla
- Gelecek hafta planı
```

### Aylık Rutin

```
📆 Ay Başı
- Geçen ay performans raporu
- Tüm tedarikçileri değerlendir
- Hedefler belirle

📊 Ay Sonu
- Hedef gerçekleşme kontrolü
- AI trend analizi
- Yıllık projeksiyon
```

---

## 📞 Destek ve İletişim

### Teknik Destek

**Uygulama Sorunları:**
- GitHub Issues: [Repository linki]
- Email: support@example.com

**API/AI Sorunları:**
- Google AI Studio: https://makersuite.google.com
- Gemini Dokümantasyon: https://ai.google.dev

### Eğitim Materyalleri

📺 Video Tutoriallar: [Link]
📄 PDF Kılavuz: [Link]
🎓 Online Kurs: [Link]

---

## 🔄 Versiyon Geçmişi

### v2.0.0 (Şubat 2024)
- ✨ Akıllı Eylem Önerileri eklendi
- ✨ Email Gelen Kutusu eklendi
- ✨ Doğal Dil Sorguları eklendi
- ✨ Gemini 2.0 Flash entegrasyonu
- 🐛 Thread-safety iyileştirmeleri
- 🐛 UI/UX geliştirmeleri

### v1.0.0 (Aralık 2023)
- 🎉 İlk sürüm
- Temel analiz özellikleri
- YZ Raporu
- Akıllı Email

---

## 📝 Notlar

### Önemli Hatırlatmalar

⚠️ **Veri Yedekleme:** Düzenli olarak verilerinizi yedekleyin
⚠️ **API Kotası:** Gemini ücretsiz planında günlük limit var
⚠️ **İnsan Kontrolü:** AI önerilerini mutlaka kontrol edin
⚠️ **Güvenlik:** API key'leri paylaşmayın

### Gelecek Özellikler (Roadmap)

🔮 **Planlanıyor:**
- Çoklu dil desteği (İngilizce, Almanca)
- Mobil uygulama
- Web arayüzü
- Daha fazla AI modeli desteği
- Otomatik raporlama
- Dashboard customization

---

## 🎯 Sonuç

Bu detaylı kılavuz, **Tedarikçi Performans Analiz Sistemi**'nin tüm özelliklerini ve özellikle **Yapay Zeka kullanımlarını** kapsamaktadır.

### Özet

✅ **6 Ana AI Özelliği**
✅ **8+ Sekme/Ekran**
✅ **Türkçe Doğal Dil İşleme**
✅ **Otomatik Email Yönetimi**
✅ **Proaktif Problem Çözme**
✅ **Tahmine Dayalı Analiz**

### Başarının Anahtarları

1. 🔑 **Düzenli Kullanım** - Her gün kontrol edin
2. 🔑 **AI'ye Güvenin** - Ama kontrol edin
3. 🔑 **Proaktif Olun** - Sorunları erkenden yakalayın
4. 🔑 **Veri Kalitesi** - Doğru veri, doğru analiz
5. 🔑 **Sürekli Öğrenin** - Yeni özellikler deneyin

---

**🎉 İyi Kullanımlar! 🎉**

*Bu kılavuz sürekli güncellenmektedir. En son versiyonu repository'den kontrol edin.*

**Versiyon:** 2.0.0
**Güncelleme:** Şubat 2024
**Hazırlayan:** Defacto AI Ekibi
