# Yeni Zombi Zorluk Seviyeleri - Dutluk Mod

## Genel Bakış

Bu güncelleme ile 7 Days to Die oyununa **3 yeni zombi zorluk seviyesi** eklenmiştir. Mevcut Radiated (Yeşil), Charged (Mavi) ve Infernal (Sarı) zombilerin yanına **Corrupted (Mor)**, **Apocalyptic (Kırmızı)** ve **Legendary Boss (Altın)** zombiler eklenmiştir.

## Yeni Zorluk Seviyeleri

### 🟣 Corrupted (Bozulmuş) - Mor Zombiler
- **Renk**: Mor (Purple) - RGB değeri: `1.5,0,2.5, .8`
- **Zorluk**: Infernal zombilerden %25 daha güçlü
- **Sağlık**: 2000-3750 arası (zombi türüne göre)
- **Hasar**: 45 (Charged'dan %25 daha yüksek)
- **XP**: 2000-2300 arası
- **Özellikler**: 
  - Daha hızlı hareket kalıpları
  - Daha uzun zıplama mesafesi
  - Karanlık enerji ile bozulmuş

### 🔴 Apocalyptic (Kıyamet) - Kırmızı Zombiler
- **Renk**: Kırmızı (Pure Red) - RGB değeri: `3,0,0, .9`
- **Zorluk**: Çok yüksek zorluk seviyesi
- **Sağlık**: 2600-4875 arası (zombi türüne göre)
- **Hasar**: 60 (Corrupted'dan %33 daha yüksek)
- **XP**: 2800-3200 arası
- **Özellikler**:
  - Çok hızlı ve öngörülemez hareket kalıpları
  - Uzun zıplama mesafesi
  - Boss seviyesinden önceki en büyük tehdit

### 🟡 Legendary Boss (Efsanevi) - Altın Zombiler
- **Renk**: Altın (Golden) - RGB değeri: `3,2.5,0, 1.0`
- **Zorluk**: En yüksek boss seviyesi
- **Sağlık**: 7500 (sadece Spider Boss)
- **Hasar**: 85 (Boss seviyesi hasar)
- **XP**: 5000
- **Özellikler**:
  - Sadece Spider türünde mevcut
  - %30 daha büyük boyut
  - Knockdown ve stun'a dayanıklı
  - En hızlı hareket ve en uzun zıplama
  - Neredeyse yıkılmaz

## Eklenen Zombi Türleri

Her yeni zorluk seviyesi için aşağıdaki zombi türleri eklenmiştir:

### Corrupted Varyantları:
- `zombieArleneCorrupted` - Bozulmuş Arlene
- `zombieBusinessManCorrupted` - Bozulmuş İş Adamı
- `zombieJoeCorrupted` - Bozulmuş Joe
- `zombieBoeCorrupted` - Bozulmuş Boe
- `zombieSpiderCorrupted` - Bozulmuş Örümcek

### Apocalyptic Varyantları:
- `zombieArleneApocalyptic` - Kıyamet Arlene
- `zombieBusinessManApocalyptic` - Kıyamet İş Adamı
- `zombieJoeApocalyptic` - Kıyamet Joe
- `zombieBoeApocalyptic` - Kıyamet Boe
- `zombieSpiderApocalyptic` - Kıyamet Örümcek

### Boss Level:
- `dutSpiderBoss` - Efsanevi Örümcek Boss

## Spawn Sistemi

### Game Stage Gereksinimleri:
- **Corrupted zombiler**: Game Stage 150+ (Orta-yüksek seviye)
- **Apocalyptic zombiler**: Game Stage 300+ (Çok yüksek seviye)
- **Legendary Boss**: Game Stage 500+ (Ultra yüksek seviye)

### Yeni Spawner'lar:
- `EnhancedWanderingHorde` - Gelişmiş gezgin sürüleri
- `EnhancedBloodMoonHorde` - Gelişmiş kan ayı sürüleri
- `EnhancedSleeperHorde` - Gelişmiş uyuyan zombi grupları

### Karışık Gruplar:
- `mixedCorruptedGroup` - Karışık Corrupted zombi grupları
- `mixedApocalypticGroup` - Karışık Apocalyptic zombi grupları
- `progressiveHordeStageHigh` - Aşamalı yüksek zorluk grupları
- `progressiveHordeStageExtreme` - Aşamalı ekstrem zorluk grupları
- `nightmareHorde` - Kabus modu için ultra zorluk grubu

## Teknik Detaylar

### Dosya Yapısı:
- `dutZombiTier/zombie_classes.xml` - Zombi sınıfları, renk tanımları ve özellikleri
- `dutZombiTier/zombie_groups.xml` - Zombi grupları ve spawn oranları
- `dutZombiTier/zombie_stages.xml` - Game stage tabanlı spawn sistemi
- `dutZombiTier/zombie_weapons.xml` - Yeni zombi el silahları
- `Localization.txt` - Türkçe ve İngilizce isimler
- `items.xml` - Ana include dosyası

### Performans Optimizasyonu:
- Yüksek game stage'lerde spawn edilir
- Balanced spawn oranları
- Memory-friendly grup yapıları

## Oynanış Etkisi

### Zorluk Artışı:
- Yüksek seviye oyuncular için yeni meydan okumalar
- Daha stratejik yaklaşım gerektiren savaşlar
- Gelişmiş ekipman ihtiyacı

### Dengeleme:
- XP ödülleri zorlukla orantılı
- Sağlık değerleri dengeli artış
- Hareket kalıpları öngörülebilir ama zorlu

## Kurulum

Mod dosyaları otomatik olarak yüklenecektir. Oyunu yeniden başlatmanız yeterlidir.

## Uyumluluk

- 7 Days to Die v2.2+ ile uyumlu
- Diğer zombi modları ile çakışabilir
- Vanilla game stage sistemi ile uyumlu

## Gelecek Güncellemeler

- Daha fazla zombi türü için Corrupted/Apocalyptic varyantları
- Özel loot tabloları
- Yeni ses efektleri
- Görsel efekt iyileştirmeleri

---

**Not**: Bu zombiler yalnızca yüksek game stage'lerde görünür. Yeni başlayan oyuncular etkilenmeyecektir.

**Geliştirici**: Dutluk Mod Ekibi  
**Versiyon**: 1.0  
**Tarih**: Ağustos 2025
