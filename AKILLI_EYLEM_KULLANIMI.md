# 🎯 Akıllı Eylem Önerileri - Kullanım Kılavuzu

## Nerede Bulabilirim?

**Sol Menü → 🎯 Akıllı Eylem Önerileri**

## Ne İşe Yarar?

Bu özellik tedarikçi performans problemlerini otomatik tespit eder ve yapay zeka ile spesifik aksiyon önerileri sunar.

## Nasıl Kullanılır?

### 1. Sekmeyi Açın
- Sol menüden "🎯 Akıllı Eylem Önerileri" tıklayın

### 2. Otomatik Analiz
- Sistem tedarikçi verilerini analiz eder (5-10 saniye)
- Yapay zeka problemleri tespit eder
- Her problem için öneriler oluşturur

### 3. Önerileri İnceleyin
Aksiyonlar 4 öncelik seviyesinde gruplandırılır:
- 🔴 **KRİTİK** - Acil müdahale gerekli
- 🟠 **YÜKSEK** - Yakında aksiyona ihtiyaç var
- 🟡 **ORTA** - Önemli ama acil değil
- 🟢 **DÜŞÜK** - Planlanabilir

### 4. Aksiyonları Takip Edin
Her aksiyon kartında:
- Problem açıklaması
- 3-5 spesifik öneri
- Zaman çizelgesi
- İki buton:
  - ✓ **Tamamlandı** - İşlemi bittiğinde işaretle
  - 🗑️ **Kapat** - Önemsiz ise kapat

### 5. Yeniden Analiz
- Sağ üstteki "🔄 Yenile" butonuna tıklayın
- Veri değişikliklerinden sonra yeni analiz yapılır

## Örnek Senaryolar

### Senaryo 1: Düşük Teslimat Performansı
```
Tespit: Tedarikçi A'nın teslimat skoru %65 (hedef: %70+)

Öneriler:
1. Alternatif tedarikçi araştır
2. Acil toplantı planla  
3. Stok güvenlik seviyelerini artır

Öncelik: 🔴 KRİTİK
Zaman: Hemen
```

### Senaryo 2: Kalite Sorunu
```
Tespit: Tedarikçi B'nin kalite skoru 72 (hedef: 75+)

Öneriler:
1. Kalite denetimi planla
2. Üretim sürecini incele
3. Detaylı geri bildirim ver

Öncelik: 🟠 YÜKSEK
Zaman: Bu hafta
```

### Senaryo 3: Yüksek İade Oranı
```
Tespit: Ürün kategorisi X'de %8 iade oranı (hedef: %5 altı)

Öneriler:
1. Kök neden analizi yap
2. Kalite kontrol sıkılaştır
3. Tedarikçi eğitimi düzenle

Öncelik: 🔴 KRİTİK
Zaman: Hemen
```

## İpuçları

### Günlük Rutin
1. Sabah işe başlarken "Akıllı Eylem Önerileri"ni kontrol et
2. Kırmızı (kritik) aksiyonları öncelikle yap
3. Tamamlananları işaretle
4. Gün sonunda yenile ve ilerlemeyi gör

### Haftalık Kontrol
- Pazartesi: Haftalık aksiyon planı oluştur
- Çarşamba: Orta dönem kontrol
- Cuma: Hafta sonu özeti ve tamamlananları işaretle

### Ekip İşbirliği
- Kritik aksiyonları ekiple paylaş
- Sorumluluk ata
- Tamamlanma durumunu takip et

## Sık Sorulan Sorular

**S: Hiç öneri çıkmıyor?**
C: Bu iyi haber! Tüm tedarikçilerin performansı hedeflerin üzerinde.

**S: Çok fazla öneri var?**
C: Önce kırmızı (kritik) olanları halledelim. Diğerleri zamanla azalır.

**S: AI yanlış öneri veriyorsa?**
C: "🗑️ Kapat" butonuyla kapatabilirsiniz. Sistem öğrenir.

**S: Öneriler nasıl güncellenir?**
C: "🔄 Yenile" butonuna tıklayın. Veri değişiklikleri yeni analiz tetikler.

## Teknik Detaylar

### Tespit Edilen Sorunlar
- Teslimat performansı < %70
- Kalite skoru < 75
- İade oranı > %5

### AI Motoru
- Google Gemini 2.0 Flash
- Türkçe prompt engineering
- Bağlam farkında öneriler
- Gerçek zamanlı analiz

### Veri Kaynakları
- Tedarikçi performans verileri
- Kalite skorları
- İade istatistikleri
- Geçmiş trendler

## Destek

Sorun yaşarsanız:
1. Sayfayı yenileyin (F5)
2. "🔄 Yenile" butonunu kullanın
3. Veri yüklenmiş olduğundan emin olun
4. GEMINI_API_KEY yapılandırılmış olmalı

---

**Hazırlayan:** AI Geliştirme Ekibi  
**Tarih:** 12 Şubat 2026  
**Versiyon:** 1.0
