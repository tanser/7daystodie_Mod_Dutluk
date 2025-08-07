# 7 Days to Die Modding - Best Practices & Format Guide

## 🎯 TEMEL KURAL: Her Zaman Orjinal Oyun Formatını Takip Et!

### 📁 Mod Dosya Yapısı
```
mods/ModName/
├── config/
│   ├── items.xml (ana include dosyası)
│   ├── Localization.txt
│   └── subFolder/ (organize etmek için)
│       ├── specific_feature.xml
│       └── another_feature.xml
└── README.md
```

---

## 🔧 XML Mod Formatı - ZORUNLU YAPISI

### ✅ DOĞRU Mod Formatı:
```xml
<?xml version="1.0" encoding="UTF-8"?>

<configs>
  <append xpath="/root_element_name">
    
    <!-- Mod içeriği buraya -->
    
  </append>
</configs>
```

### ❌ YANLIŞ Format (Asla Kullanma):
```xml
<?xml version="1.0" encoding="UTF-8"?>

<root_element_name>
  <!-- Bu format sadece orjinal oyun dosyalarında kullanılır -->
</root_element_name>
```

---

## 📋 Dosya Türlerine Göre Formatlar

### 1. **Entity Classes** (zombi sınıfları)
```xml
<configs>
  <append xpath="/entity_classes">
    
    <!-- Renk tanımları -->
    <color name="newColor" value="R,G,B, emissive_power"/>
    
    <!-- Sağlık değerleri -->
    <replace_passive_effect>
      <property name="healthZombieType" value="1500"/>
    </replace_passive_effect>
    
    <!-- Hareket kalıpları -->
    <replace_properties>
      <property name="moveSpeedPattern" value="2.5, .9, .8, 1.8"/>
    </replace_properties>
    
    <!-- Zombi sınıfları -->
    <entity_class name="newZombie" extends="existingZombie">
      <property name="MatColor" value="newColor"/>
      <property name="ExperienceGain" value="2000"/>
      <!-- diğer özellikler -->
    </entity_class>
    
  </append>
</configs>
```

### 2. **Entity Groups** (zombi grupları)
```xml
<configs>
  <append xpath="/entity_groups">
    
    <!-- Basit grup -->
    <entitygroup name="singleZombieGroup">
      zombieName
    </entitygroup>
    
    <!-- Karışık grup -->
    <entitygroup name="mixedGroup" count="2,5">
      zombieName1, .3
      zombieName2, .4
      zombieName3, .3
    </entitygroup>
    
  </append>
</configs>
```

### 3. **Game Stages** (spawn sistemi)
```xml
<configs>
  <append xpath="/gamestages">
    
    <!-- ÖNCE grup tanımları (ZORUNLU!) -->
    <group name="zombieName" spawner="zombieName"/>
    
    <!-- SONRA spawner tanımları -->
    <spawner name="zombieName">
      <gamestage stage="150">
        <spawn group="zombieName" duration="10"/>
      </gamestage>
    </spawner>
    
  </append>
</configs>
```

### 4. **Items** (silahlar, eşyalar)
```xml
<configs>
  <append xpath="/items">
    
    <item name="newItem">
      <property name="Tags" value="melee,zombie"/>
      <property name="DisplayType" value="meleeHand"/>
      <!-- diğer özellikler -->
      
      <effect_group name="newItem">
        <passive_effect name="EntityDamage" operation="base_set" value="45"/>
      </effect_group>
    </item>
    
  </append>
</configs>
```

---

## 🎨 Zombi Zorluk Seviyeleri Ekleme Rehberi

### 1. **Renk Sistemi**
- Mevcut renkler: Yeşil (Radiated), Mavi (Charged), Sarı (Infernal)
- RGB değerleri: `R,G,B, emissive_power` (0-3 arası, 1'den büyük değerler "blow out" yapar)
- Emissive power: Parlaklık (.5 = %150, 1.0 = maksimum)

### 2. **Sağlık Değerleri**
- Her zombi türü için ayrı sağlık tanımla
- Mevcut zorluk seviyelerinden %25-50 artış yap
- `healthZombieTypeNewDifficulty` formatını kullan

### 3. **Hareket Kalıpları**
- `moveSpeedPattern` ile hız kalıpları tanımla
- Daha yüksek zorluk = daha hızlı ve öngörülemez

### 4. **Spawn Gereksinimleri**
- Game Stage thresholds belirle (örn: GS 150+, 300+)
- Performans için `maxAlive` limitleri koy
- Boss seviyesi için özel encounter grupları oluştur

---

## 🔗 Entity Groups - Kritik XML Formatı

### ⚠️ KRİTİK: XPath Referansları

**XPATH REFERANSLARI MUTLAKA REFERANS DOSYALARINDA KONTROL EDİLMELİ!**

Referans dosyalardaki root element isimlerini kullan:
- `entitygroups.xml` → `<entitygroups>` → xpath="/entitygroups"
- `gamestages.xml` → `<gamestages>` → xpath="/gamestages"
- `entity_classes` → `<entity_classes>` → xpath="/entity_classes"

❌ **YANLIŞ:** `<append xpath="/entity_groups">`
✅ **DOĞRU:** `<append xpath="/entitygroups">`

### ✅ DOĞRU Entity Group Formatı:
```xml
<configs>
  <append xpath="/entitygroups">
    
    <!-- Tek entity içeren grup -->
    <entitygroup name="zombieCustomBoss">
      <entity name="zombieCustomBoss" />
    </entitygroup>
    
    <!-- Çoklu entity içeren grup (olasılık ile) -->
    <entitygroup name="mixedZombieGroup" count="2,4">
      zombieArlene, .3
      zombieBoe, .3
      zombieJoe, .4
    </entitygroup>
    
  </append>
</configs>
```

### ❌ YANLIŞ Entity Group Formatları:
```xml
<!-- HATA 1: Entity elementi eksik -->
<entitygroup name="zombieCustomBoss">
  zombieCustomBoss  <!-- Bu YANLIŞ! -->
</entitygroup>

<!-- HATA 2: Yanlış XML yapısı -->
<entitygroup name="zombieCustomBoss">
  <zombieCustomBoss />  <!-- Bu da YANLIŞ! -->
</entitygroup>
```

### 🚨 Entity Group ile İlgili Yaygın Hatalar:

**1. "EntityGroup 'groupName' unknown!" Hatası:**
- **Sebep:** Entity group tanımında `<entity name="..." />` elementi eksik
- **Çözüm:** Her grup için doğru entity elementini kullan

**2. "Object not found" Spawn Hatası:**
- **Sebep:** Entity group yanlış tanımlanmış veya entity class mevcut değil
- **Çözüm:** 
  - Entity group formatını kontrol et
  - Referenced entity class'ın tanımlı olduğunu doğrula
  - Base entity'den doğru extend edildiğini kontrol et

**3. Gamestages.xml Loading Hatası:**
- **Sebep:** Spawner'da referans edilen entity group bulunamıyor
- **Çözüm:** Entity group isminin tam olarak eşleştiğini kontrol et

### 📝 Entity Group Kontrol Listesi:
- [ ] `<entity name="..." />` formatı kullanılmış
- [ ] Entity class tanımları mevcut
- [ ] Base entity'ler (örn: zombieArleneCharged) referans dosyalarda var
- [ ] Group isimleri gamestages.xml ile tam eşleşiyor
- [ ] XML syntax doğru (kapatma tag'leri)

---

## ⚠️ KRITIK HATALAR ve Çözümleri

### 1. **Entity Groups Format Hatası**
❌ YANLIŞ:
```xml
<entity name="zombieName" prob="0.3"/>
```
✅ DOĞRU:
```xml
zombieName, .3
```

### 2. **Gamestages Group Tanımları**
❌ Grup tanımlarını unutma!
✅ Her entity group için `<group name="..." spawner="..."/>` ekle

### 3. **Mod Yapısı**
❌ Orjinal oyun formatını kullanma
✅ Her zaman `<configs>` + `<append xpath="...">` kullan

### 4. **Dosya Organizasyonu**
❌ Tek dosyada her şeyi karıştırma
✅ Anlamlı klasörler ve dosya isimleri kullan

---

## 🔍 Kontrol Listesi

### Yeni Zombi Zorluk Seviyesi Eklerken:
- [ ] `zombie_classes.xml` - Renk, sağlık, hareket kalıpları
- [ ] `zombie_groups.xml` - Entity grupları (basit format)
- [ ] `zombie_stages.xml` - Grup tanımları + spawner'lar
- [ ] `zombie_weapons.xml` - Zombi silahları
- [ ] `Localization.txt` - İsimler ve açıklamalar
- [ ] `items.xml` - Include dosyalarını ekle

### Format Kontrolü:
- [ ] Tüm dosyalar `<configs>` + `<append>` kullanıyor
- [ ] Entity groups orjinal format (virgül + nokta)
- [ ] Gamestages'de grup tanımları var
- [ ] XML syntax doğru (kapatma tag'leri)

---

## 📚 Referans Dosyaları

Orjinal oyun dosyalarını her zaman referans al:
- `/mods/v2.2 Reference Config Files/entityclasses.xml`
- `/mods/v2.2 Reference Config Files/entitygroups.xml`
- `/mods/v2.2 Reference Config Files/gamestages.xml`
- `/mods/v2.2 Reference Config Files/items.xml`

---

## 🎮 Test Süreci

1. **Syntax Kontrolü**: XML dosyalarının geçerli olduğunu kontrol et
2. **Oyun İçi Test**: Yeni zombilerin spawn olduğunu kontrol et
3. **Performance Test**: MaxAlive limitleri ile performansı test et
4. **Balance Test**: Zorluk seviyelerinin dengeli olduğunu kontrol et

---

## 💡 İpuçları

- **Modüler Yaklaşım**: Her özelliği ayrı dosyalarda organize et
- **Anlamlı İsimler**: Dosya ve klasör isimlerini açıklayıcı yap
- **Yorum Satırları**: Karmaşık kısımları açıkla
- **Versiyon Kontrolü**: Değişiklikleri dokümante et
- **Backup**: Çalışan versiyonları sakla

---

## 🔍 Hata Ayıklama Metodolojisi

### 📋 Sistematik Hata Çözme Süreci:

**1. Error Log Analizi:**
```bash
# Error log'u gerçek zamanlı takip et
tail -f "path/to/7DaysToDie/logs/error.log"

# Spesifik hataları ara
grep -i "error\|exception\|failed" error.log
```

**2. Referans Dosya Karşılaştırması:**
- Orjinal oyun dosyalarından doğru formatı öğren
- `entityclasses.xml`, `items.xml`, `entitygroups.xml` referans al
- Syntax ve property isimlerini karşılaştır

**3. Hata Kategorileri ve Çözüm Öncelikleri:**

**🔴 Kritik (Oyun Yüklenmez):**
- XML parsing hataları
- Missing entity references
- Gamestages.xml loading failures

**🟡 Orta (Özellik Çalışmaz):**
- Spawn menu'de görünmeme
- Yanlış entity properties
- BuffResistance format hataları

**🟢 Düşük (Performans/Görsel):**
- Texture/model sorunları
- Ses dosyası eksiklikleri

**4. Hata Çözme Araçları:**
```bash
# Pattern arama
grep -r "meleeHandZombieCharged" mods/

# Dosya içeriği kontrol
find . -name "*.xml" -exec grep -l "zombieArleneCorrupted" {} \;

# XML syntax kontrol (eğer xmllint varsa)
xmllint --noout zombie_groups.xml
```

**5. Test Stratejisi:**
- Her düzeltmeden sonra oyunu yeniden başlat
- Minimal test case oluştur (sadece problematik entity)
- Debug mode kullan (`dm`, `cm` komutları)
- Yeni save file ile test et

**6. Dokümantasyon:**
- Çözülen hataları kaydet
- Öğrenilen kuralları not al
- Working configurations'ı backup'la

### 🎯 Hızlı Tanı Kontrol Listesi:
- [ ] XML syntax doğru mu? (açılış/kapanış tag'leri)
- [ ] Entity isimleri tam eşleşiyor mu?
- [ ] Base entity'ler mevcut mu?
- [ ] Property isimleri doğru mu?
- [ ] File paths ve includes doğru mu?
- [ ] Mod load order problemi var mı?

---

*Bu rehber, 7 Days to Die modding deneyiminden çıkarılan pratik bilgileri içerir. Her zaman orjinal oyun dosyalarını referans alarak çalış!*
