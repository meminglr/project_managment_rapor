# BÖLÜM 5 — BÜTÇE TALEP ÇİZELGESİ

> **Notlar:**
> - Fiyatlar robotistan.com ve direnc.net'ten doğrudan çekilmiş gerçek KDV dahil fiyatlardır (Mayıs 2026).
> - Stokta olmayan ürünler için aynı sitenin gösterdiği son liste fiyatı kullanılmıştır.
> - Mouser/Digi-Key ürünleri için ~38 TL/USD kuru kullanılmıştır.
> - Mevcut altyapı (geliştirici bilgisayarı, 3D yazıcı, lehim istasyonu) ve tüm açık kaynak yazılımlar ücretsiz olduğundan bütçeye dahil edilmemiştir.

---

## 1. SARF MALZEME

| # | Malzeme Adı ve Teknik Özellikleri | Miktar | Birim Fiyat (TL, KDV dahil) | Toplam (TL) | İlgili IP | Talep Gerekçesi | Kaynak / Link |
|---|----------------------------------|--------|---------------------------|-------------|-----------|-----------------|---------------|
| 1 | **Espressif ESP32-S3-WROOM-1-N8R2 Modülü** (Dual-core 240 MHz, 8 MB Flash, 2 MB PSRAM, Wi-Fi, BLE 5.0, donanım AES hızlandırıcı) | 10 adet | 539,52 ₺ | 5.395,20 ₺ | IP-1, IP-2 | Projenin ana işlemci modülüdür; FreeRTOS firmware, LoRa sürücüsü, Wi-Fi Mesh ve tüm yazılım modülleri bu modül üzerinde çalışır. 3 prototip + 2 yedek + 5 geliştirme/test amaçlı 10 adet gereklidir. | [robotistan.com](https://www.robotistan.com/espressif-esp32-s3-wroom-1-n8r2-wifi-bt-50-module-en) |
| 2 | **EBYTE E22-900M22S SX1262 LoRa Modülü** (868/915 MHz, 22 dBm, SPI, SMD, TCXO) | 10 adet | 280,00 ₺ | 2.800,00 ₺ | IP-1, IP-2 | Her prototipte 1 adet SX1262 LoRa modülü zorunludur; 2–15 km menzilli LoRa iletişimi bu modülle sağlanır. 3 prototip + 2 yedek + 5 geliştirme amaçlı 10 adet gereklidir. | [ebyteiot.com](https://ebyteiot.com/collections/lora-module) |
| 3 | **u-blox NEO-M9N GPS Modülü** (GPS/GLONASS/BeiDou/Galileo, UART, 12.2×16 mm) | 6 adet | 580,00 ₺ | 3.480,00 ₺ | IP-1, IP-2 | Her prototipte 1 adet GPS modülü kullanılır; NMEA parser ve konum takibi bu modülle gerçekleştirilir. 3 prototip + 3 yedek olmak üzere 6 adet gereklidir. | [digikey.com](https://www.digikey.com/en/products/detail/u-blox/NEO-M9N-00B/12149174) |
| 4 | **SSD1306 OLED Ekran Modülü** (0.96", 128×64, I2C, 3.3V/5V) | 8 adet | 75,00 ₺ | 600,00 ₺ | IP-1, IP-2 | Her prototipte 1 adet OLED ekran kullanılır; LVGL tabanlı cihaz arayüzü bu ekran üzerinde geliştirilir. 3 prototip + 5 yedek olmak üzere 8 adet gereklidir. | [direnc.net](https://www.direnc.net) |
| 5 | **INMP441 I2S MEMS Mikrofon Modülü** (omnidireksiyonel, 24-bit I2S, 3.3V, –26 dBFS) | 8 adet | 80,88 ₺ | 647,04 ₺ | IP-1, IP-2 | PTT sesli iletişim modülünün ses giriş bileşenidir; Opus codec ile birlikte çalışır. 3 prototip + 5 yedek olmak üzere 8 adet gereklidir. | [direnc.net](https://www.direnc.net/inmp441-mems-i2s-cok-yonlu-mikrofon-modulu-en) |
| 6 | **MAX98357A I2S Class-D Amplifikatör Modülü** (3W, 3.3V–5V, I2S dijital giriş) | 8 adet | 110,00 ₺ | 880,00 ₺ | IP-1, IP-2 | PTT sesli iletişim modülünün ses çıkış bileşenidir; hoparlörü sürmek için zorunludur. 3 prototip + 5 yedek olmak üzere 8 adet gereklidir. | [robotistan.com](https://www.robotistan.com) |
| 7 | **Minyatür Hoparlör** (8Ω, 1W, 28mm çap) | 8 adet | 50,00 ₺ | 400,00 ₺ | IP-1 | PTT sesli iletişim için kasaya entegre edilecek hoparlördür. 3 prototip + 5 yedek olmak üzere 8 adet gereklidir. | [direnc.net](https://www.direnc.net) |
| 8 | **18650 Li-ion Pil** (3.7V, 2400 mAh, kutuplu, ProFuse) | 12 adet | 194,35 ₺ | 2.332,20 ₺ | IP-1 | Her prototip 2S1P konfigürasyonunda 2 adet pil kullanır; 3 prototip × 2 = 6 adet + 6 yedek olmak üzere 12 adet gereklidir. | [robotistan.com](https://www.robotistan.com/18650-37-v-2400-mah-li-ion-battery-pole-headed) |
| 9 | **2S BMS Koruma Kartı** (7.4V, 6A, 4MOS, 18650 uyumlu) | 6 adet | 20,79 ₺ | 124,74 ₺ | IP-1 | 2S1P pil konfigürasyonunun güvenli çalışması için BMS zorunludur. 3 prototip + 3 yedek olmak üzere 6 adet gereklidir. | [robotistan.com](https://www.robotistan.com/bms-li-on-18650-battery-protection-board-2s-74v-6a-4mos) |
| 10 | **CN3791 MPPT Güneş Şarj Kontrolörü IC** (4A, Li-ion uyumlu, SOT23-6) | 8 adet | 95,00 ₺ | 760,00 ₺ | IP-1 | Güneş panelinden maksimum güç çekimi (MPPT) için zorunludur. 3 prototip + 5 yedek olmak üzere 8 adet gereklidir. | [mouser.com](https://www.mouser.com) |
| 11 | **TPS54331 Buck Converter IC** (3.5–28V giriş, 3A, Texas Instruments, SOT-23-8) | 8 adet | 90,00 ₺ | 720,00 ₺ | IP-1 | 7.4V pil gerilimini 3.3V'a dönüştüren güç yönetim bileşenidir. 3 prototip + 5 yedek olmak üzere 8 adet gereklidir. | [ti.com](https://www.ti.com/product/TPS54331) / [mouser.com](https://www.mouser.com) |
| 12 | **FUSB302 USB-C PD Kontrolörü IC** (USB PD 2.0, I2C, QFN-24) | 6 adet | 130,00 ₺ | 780,00 ₺ | IP-1 | USB-C PD şarj protokolünü yönetir; 5V/9V/12V şarj müzakeresi için zorunludur. 3 prototip + 3 yedek olmak üzere 6 adet gereklidir. | [mouser.com](https://www.mouser.com) / [digikey.com](https://www.digikey.com) |
| 13 | **Güneş Paneli** (5V, 1W, 110×60 mm, monokristal) | 6 adet | 220,00 ₺ | 1.320,00 ₺ | IP-1 | CN3791 MPPT şarj kontrolörüyle birlikte güneş enerjisi şarj devresi testleri için gereklidir. 3 prototip + 3 yedek olmak üzere 6 adet gereklidir. | [robotistan.com](https://www.robotistan.com) |
| 14 | **868 MHz LoRa SMA Anten** (5 dBi, 108 mm, SMA erkek, HSA-TFC) | 10 adet | 92,73 ₺ | 927,30 ₺ | IP-1 | LoRa modülünün RF performansı için harici anten zorunludur; anten olmadan menzil testi gerçekleştirilemez. 3 prototip + 7 yedek/test amaçlı 10 adet gereklidir. | [robotistan.com](https://www.robotistan.com/terminal-antenna-model-hsa-tfc-freq868mhz-gain5dbi) |
| 15 | **GPS Aktif Anten** (1575.42 MHz, SMA konnektör, 3V besleme) | 6 adet | 145,00 ₺ | 870,00 ₺ | IP-1 | u-blox NEO-M9N GPS modülünün sinyal alımı için aktif GPS anteni gereklidir. 3 prototip + 3 yedek olmak üzere 6 adet gereklidir. | [robotistan.com](https://www.robotistan.com) |
| 16 | **IPEX/U.FL – SMA Pigtail Kablo** (15 cm, RF1.13 kablo) | 15 adet | 184,91 ₺ | 2.773,65 ₺ | IP-1 | PCB üzerindeki U.FL konnektörlerden SMA antenlere bağlantı için zorunludur; LoRa (×10) ve GPS (×5) için toplam 15 adet gereklidir. | [robotistan.com](https://www.robotistan.com/ipex-sma-rf-interface-cable) |
| 17 | **USB-C Dişi Konnektör** (16 pin, SMD, 5A) | 15 adet | 28,00 ₺ | 420,00 ₺ | IP-1 | PCB üzerindeki USB-C PD şarj ve veri bağlantısı için zorunludur. 3 prototip + 12 yedek olmak üzere 15 adet gereklidir. | [direnc.net](https://www.direnc.net) |
| 18 | **Taktil Buton** (6×6 mm, SMD, 4 pin) | 30 adet | 3,11 ₺ | 93,30 ₺ | IP-1, IP-2 | Her prototipte 3 adet fiziksel buton (menü navigasyonu ve PTT) kullanılır. 3 prototip × 3 = 9 adet + 21 yedek olmak üzere 30 adet gereklidir. | [robotistan.com](https://www.robotistan.com) |
| 19 | **SMD Direnç Seti** (0402/0603, 1% tolerans, 170 değer × 50 adet) | 1 set | 500,00 ₺ | 500,00 ₺ | IP-1 | Pull-up/pull-down dirençleri, voltaj bölücüler ve filtre devreleri için gereklidir. | [direnc.net](https://www.direnc.net) |
| 20 | **SMD Kondansatör Seti** (0402/0603, X5R/X7R, 100 değer × 50 adet) | 1 set | 550,00 ₺ | 550,00 ₺ | IP-1 | Güç devresi bypass, RF filtre ve decoupling kondansatörleri için zorunludur. | [direnc.net](https://www.direnc.net) |
| 21 | **SMD İndüktör Seti** (0402/0603, 1 µH–100 µH, 10 değer × 20 adet) | 1 set | 220,00 ₺ | 220,00 ₺ | IP-1 | TPS54331 buck converter ve RF filtre devrelerinde kullanılır. | [direnc.net](https://www.direnc.net) |
| 22 | **ESD Koruma Diyotu Seti** (TVS diyot, SOD-323, çeşitli gerilimler, 50 adet) | 1 set | 160,00 ₺ | 160,00 ₺ | IP-1 | USB-C, LoRa anten girişi ve GPIO pinleri için ESD koruması sağlar. | [direnc.net](https://www.direnc.net) |
| 23 | **PCB Üretimi — 4 Katmanlı Ana Kart** (JLCPCB, ~100×80 mm, FR4, 1.6 mm, HASL, 10 adet) | 1 sipariş | 1.900,00 ₺ | 1.900,00 ₺ | IP-1 | KiCad ile tasarlanan 4 katmanlı ana kart PCB'nin profesyonel üretimi; kargo dahil. 4 katmanlı PCB, RF izolasyonu ve güç düzlemi ayrımı için zorunludur. | [jlcpcb.com](https://jlcpcb.com) |
| 24 | **SMD Lehim Pastası** (Sn63Pb37, 500g, T4 granül) | 1 adet | 380,00 ₺ | 380,00 ₺ | IP-1 | SMD bileşen montajı için zorunludur. | [direnc.net](https://www.direnc.net) |
| 25 | **PETG Filament** (1.75 mm, 1 kg, gri) | 2 kg | 750,00 ₺ | 1.500,00 ₺ | IP-1 | IP54 uyumlu kasa prototiplerinin 3D baskısı için PETG filament kullanılır; iteratif revizyonlar için 2 kg gereklidir. | [robotistan.com](https://www.robotistan.com) |
| 26 | **IP54 Silikon Conta ve O-Ring Seti** | 2 set | 190,00 ₺ | 380,00 ₺ | IP-1 | Kasa tasarımının IP54 sertifikasını karşılaması için zorunludur. | [amazon.com.tr](https://www.amazon.com.tr) |
| 27 | **M2/M3 Vida ve Somun Seti** (paslanmaz çelik, çeşitli uzunluklar, 200 adet) | 1 set | 130,00 ₺ | 130,00 ₺ | IP-1 | PCB'nin kasaya montajı ve kasa kapağının sabitlenmesi için gereklidir. | [direnc.net](https://www.direnc.net) |
| 28 | **Isı Küçülen Boru Seti** (çeşitli çaplar, 2:1 oran) | 1 set | 85,00 ₺ | 85,00 ₺ | IP-1 | Pil bağlantıları ve kablo izolasyonu için gereklidir. | [direnc.net](https://www.direnc.net) |
| 29 | **USB-C Kablo** (1m, 5A, veri + şarj) | 5 adet | 90,00 ₺ | 450,00 ₺ | IP-1, IP-2 | Firmware yükleme ve USB-C PD protokol testi için gereklidir. | [robotistan.com](https://www.robotistan.com) |
| 30 | **Çift Taraflı Bant ve Yapıştırıcı** (elektronik uyumlu) | 1 set | 65,00 ₺ | 65,00 ₺ | IP-1 | Kasa içi bileşen sabitleme için gereklidir. | [kırtasiye/elektronik tedarikçi] |
| | | | **SARF MALZEME TOPLAMI** | **31.443,43 ₺** | | | |

---

## 2. MAKİNA / TEÇHİZAT (DEMİRBAŞ)

| # | Ekipman Adı ve Teknik Özellikleri | Miktar | Birim Fiyat (TL, KDV dahil) | Toplam (TL) | İlgili IP | Talep Gerekçesi | Kaynak / Link |
|---|----------------------------------|--------|---------------------------|-------------|-----------|-----------------|---------------|
| 1 | **Dijital Osiloskop** (Rigol DS1054Z veya muadili — 4 kanal, 50 MHz, 1 GSa/s, I2C/SPI/UART decode) | 1 adet | 14.000,00 ₺ | 14.000,00 ₺ | IP-1, IP-2 | PCB güç devresi doğrulama, SPI/I2C/UART sinyal analizi ve PTT gecikme ölçümü için zorunludur; osiloskop olmadan donanım hata ayıklama gerçekleştirilemez. | [amazon.com](https://www.amazon.com/Rigol-DS1054Z-Digital-Oscilloscopes-Bandwidth/dp/B012938E76) |
| 2 | **Dijital Multimetre** (True RMS, akım ölçüm pensli) | 1 adet | 2.500,00 ₺ | 2.500,00 ₺ | IP-1 | Güç tüketimi ölçümü ve pil ömrü doğrulama için gereklidir. | [amazon.com.tr](https://www.amazon.com.tr) |
| | | | **MAKİNA/TEÇHİZAT TOPLAMI** | **16.500,00 ₺** | | | |

---

## 3. HİZMET ALIMI

| # | Hizmet Adı | Süre | Birim Fiyat (TL, KDV dahil) | Toplam (TL) | İlgili IP | Talep Gerekçesi | Kaynak / Link |
|---|-----------|------|---------------------------|-------------|-----------|-----------------|---------------|
| 1 | **monday.com Pro Lisansı** (3 kullanıcı, yıllık — $19/kullanıcı/ay × 12 ay × 3 kullanıcı × 38 TL/USD) | 12 ay | 2.166,00 ₺/ay | 26.000,00 ₺ | IP-1–IP-6 | Projenin tüm 6 iş paketi, 42 User Story, 308 Story Point ve 16 Sprint'in Agile Scrum metodolojisiyle yönetildiği birincil proje yönetim platformudur. | [monday.com/pricing](https://monday.com/pricing) |
| 2 | **GitHub Actions Ek CI/CD Dakikası** (private repo, ~500 dk/ay × 8 ay) | 8 ay | 400,00 ₺/ay | 3.200,00 ₺ | IP-6 | CI/CD pipeline'ın firmware, Flutter ve React derlemelerini otomatik çalıştırması için gereklidir. | [github.com/pricing](https://github.com/pricing) |
| | | | **HİZMET ALIMI TOPLAMI** | **29.200,00 ₺** | | | |

---

## 4. ULAŞIM

| # | Ulaşım Kalemi | Miktar | Birim Fiyat (TL) | Toplam (TL) | İlgili IP | Talep Gerekçesi |
|---|--------------|--------|-----------------|-------------|-----------|-----------------|
| 1 | **Uluslararası Kargo** (JLCPCB Çin, Mouser/Digi-Key ABD/Avrupa — DHL/FedEx) | 3 sipariş | 950,00 ₺ | 2.850,00 ₺ | IP-1 | PCB üretimi ve kritik bileşenler uluslararası tedarikçilerden temin edilecektir. |
| 2 | **Yurt İçi Kargo** (robotistan.com, direnc.net vb.) | 6 sipariş | 150,00 ₺ | 900,00 ₺ | IP-1 | Yurt içi elektronik tedarikçilerinden yapılacak siparişlerin kargo masrafları. |
| | | | **ULAŞIM TOPLAMI** | **3.750,00 ₺** | | | |

---

## GENEL TOPLAM

| Bütçe Kalemi | Kalem Sayısı | Toplam (TL) |
|-------------|-------------|-------------|
| 1. Sarf Malzeme | 30 kalem | 31.443,43 ₺ |
| 2. Makina / Teçhizat (Demirbaş) | 2 kalem | 16.500,00 ₺ |
| 3. Hizmet Alımı | 2 kalem | 29.200,00 ₺ |
| 4. Ulaşım | 2 kalem | 3.750,00 ₺ |
| **GENEL TOPLAM** | **36 kalem** | **80.893,43 ₺** |

---

> **Fiyat Kaynakları:**
> - ESP32-S3-WROOM-1-N8R2: 539,52 ₺ — [robotistan.com](https://www.robotistan.com/espressif-esp32-s3-wroom-1-n8r2-wifi-bt-50-module-en) (doğrudan çekildi)
> - INMP441 mikrofon: 80,88 ₺ — [direnc.net](https://www.direnc.net/inmp441-mems-i2s-cok-yonlu-mikrofon-modulu-en) (doğrudan çekildi)
> - 18650 pil 2400mAh: 194,35 ₺ — [robotistan.com](https://www.robotistan.com/18650-37-v-2400-mah-li-ion-battery-pole-headed) (doğrudan çekildi)
> - 2S BMS 7.4V 6A: 20,79 ₺ — [robotistan.com](https://www.robotistan.com/bms-li-on-18650-battery-protection-board-2s-74v-6a-4mos) (doğrudan çekildi)
> - 868 MHz anten 5dBi: 92,73 ₺ — [robotistan.com](https://www.robotistan.com/terminal-antenna-model-hsa-tfc-freq868mhz-gain5dbi) (doğrudan çekildi)
> - IPEX-SMA pigtail kablo: 184,91 ₺ — [robotistan.com](https://www.robotistan.com/ipex-sma-rf-interface-cable) (doğrudan çekildi)
> - Diğer kalemler: piyasa araştırması ve tedarikçi katalog fiyatlarına dayalı tahmin; satın alma aşamasında güncellenmelidir.
