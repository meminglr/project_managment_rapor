# BÖLÜM 2 — YÖNTEM

---

## 2.1 Araştırma Tasarımı

Bu araştırma, **deneysel yazılım ve donanım geliştirme** paradigmasına dayanan, nicel performans ölçümlerini esas alan **karma tasarımlı (mixed-methods) bir mühendislik araştırması** niteliğindedir. Araştırma; sistem tasarımı, prototip üretimi, yazılım geliştirme ve deneysel doğrulama aşamalarını sıralı değil, iteratif ve paralel biçimde yürüten bir yapıya sahiptir. Bu yaklaşım, karmaşık gömülü sistem projelerinde gereksinim belirsizliğini azaltmak ve erken aşamada teknik riskleri tespit etmek amacıyla Agile Scrum metodolojisiyle bütünleştirilmiştir.

Araştırma tasarımı üç temel katmandan oluşmaktadır:

1. **Sistem Tasarımı ve Donanım Geliştirme Katmanı:** PCB tasarımı, bileşen seçimi, mekanik kasa tasarımı ve prototip üretimini kapsar. Bu katman, deneysel donanım araştırması yöntemlerini izlemektedir.
2. **Yazılım Geliştirme Katmanı:** Gömülü firmware, mobil uygulama ve web arayüzü geliştirmeyi kapsar. Test-Driven Development (TDD) ve Continuous Integration/Continuous Deployment (CI/CD) pratikleriyle desteklenmektedir.
3. **Deneysel Doğrulama Katmanı:** Geliştirilen sistemin performans, güvenlik ve güvenilirlik gereksinimlerini karşılayıp karşılamadığını nicel ölçümlerle doğrular. Bu katmanda birim testleri, entegrasyon testleri, property-based testler, Hardware-in-the-Loop (HIL) testleri ve yük testleri uygulanmaktadır.

---

## 2.2 Bağımlı ve Bağımsız Değişkenler

Araştırmanın deneysel doğrulama boyutunda aşağıdaki değişkenler tanımlanmıştır:

**Bağımsız Değişkenler:**
- Mesh ağındaki düğüm sayısı (3, 10, 50, 100+)
- Yönlendirme modu (flood routing / Dijkstra tabanlı structured routing)
- Şifreleme yükü (şifreleme aktif / pasif)
- Güç modu (tam güç / düşük güç / kritik güç)
- LoRa yayılma faktörü (SF7–SF12) ve bant genişliği yapılandırması

**Bağımlı Değişkenler:**
- Mesaj iletim oranı (Packet Delivery Ratio — PDR, hedef: ≥ %99,9)
- Uçtan uca mesaj gecikmesi (hedef: ≤ 500 ms PTT için)
- LoRa iletişim menzili (hedef: ≥ 2 km açık alanda)
- Şifreleme işlem süresi (hedef: ≤ 10 ms/mesaj, ESP32-S3 donanım hızlandırıcısıyla)
- Pil ömrü (hedef: ≥ 72 saat düşük güç modunda)
- CI/CD pipeline tamamlanma süresi (hedef: ≤ 30 dakika)

**Kontrol Değişkenleri:**
- Donanım platformu (ESP32-S3, sabit)
- Firmware temel sürümü (Meshtastic fork, sabit commit hash)
- Test ortamı sıcaklığı (oda sıcaklığı, aksi belirtilmedikçe)

---

## 2.3 Agile Scrum Metodolojisinin Bilimsel Konumlandırılması

Bu araştırmada proje yönetim çerçevesi olarak **Agile Scrum** metodolojisi benimsenmiştir. Scrum'ın IoT ve gömülü sistem araştırmalarına uygulanabilirliği, Guerrero-Ulloa ve ark. (2023) tarafından MDPI Sensors dergisinde yayımlanan çalışmada kapsamlı biçimde ele alınmış; iteratif geliştirme döngülerinin donanım-yazılım entegrasyon projelerinde gereksinim değişikliklerine adaptasyonu kolaylaştırdığı ve erken hata tespitini desteklediği gösterilmiştir [[Guerrero-Ulloa et al., 2023, MDPI Sensors](https://www.mdpi.com/1424-8220/23/2/790)]. Benzer biçimde, güvenlik açısından kritik sistemlerde Scrum'ın uygulanmasını inceleyen çalışmalar, iteratif test döngülerinin güvenlik gereksinimlerinin sürekli doğrulanmasına olanak tanıdığını ortaya koymaktadır [[Scrum for Safety, ResearchGate, 2022](https://www.researchgate.net/publication/362208529_Scrum_for_safety_an_agile_methodology_for_safety-critical_software_systems)].

Bu araştırmada Scrum metodolojisi aşağıdaki bilimsel işlevleri üstlenmektedir:

### 2.3.1 Product Backlog ve Araştırma Gereksinim Yönetimi

Araştırmanın tüm gereksinimleri, 42 User Story ve 308 Story Point'ten oluşan bir **Product Backlog** olarak yapılandırılmıştır. Her User Story; kabul kriterleri, bağımlılık ilişkileri, öncelik düzeyi (Yüksek/Orta) ve ilgili iş paketiyle etiketlenmiştir. Bu yapı, araştırma gereksinimlerinin izlenebilirliğini (traceability) sağlamakta ve her geliştirme çıktısının hangi araştırma hedefine karşılık geldiğini açıkça ortaya koymaktadır. Backlog refinement toplantıları, teknik bağımlılıkların önceden tespit edilmesine ve kritik yol analizinin güncellenmesine olanak tanımaktadır.

### 2.3.2 Sprint Yapısı ve İteratif Doğrulama

Araştırma, her biri 2 haftalık 16 Sprint'e bölünmüştür (Ocak 2026 – Ağustos 2026). Her Sprint'in sonunda, o Sprint kapsamındaki yazılım veya donanım bileşeni çalışır durumda teslim edilmekte ve önceden tanımlanmış kabul kriterleri çerçevesinde test edilmektedir. Bu yaklaşım, geleneksel şelale (waterfall) modelinin aksine, hataların ve tasarım uyumsuzluklarının proje sonuna birikmesini önlemekte; her iterasyonda elde edilen ölçüm sonuçları bir sonraki Sprint'in planlamasını doğrudan beslemektedir.

### 2.3.3 Sprint Review ve Araştırma Kalitesi

Her Sprint sonunda gerçekleştirilen **Sprint Review** toplantısı, teslim edilen çıktının kabul kriterlerini karşılayıp karşılamadığını değerlendiren bir **ara doğrulama noktası** işlevi görmektedir. Bu süreç, araştırma kalitesini sürekli izleme mekanizması olarak konumlandırılmaktadır. Örneğin Sprint 3 Review'unda LoRa menzil testi sonuçları değerlendirilmiş; Sprint 4 planlaması bu sonuçlara göre şekillendirilmiştir.

### 2.3.4 Sprint Retrospektif ve Metodolojik İyileştirme

**Sprint Retrospektif** toplantıları, yalnızca süreç iyileştirmesi değil, aynı zamanda **metodolojik öz-değerlendirme** aracı olarak kullanılmaktadır. Test stratejilerindeki eksiklikler, ölçüm yöntemlerindeki belirsizlikler ve teknik borç (technical debt) bu toplantılarda tespit edilerek bir sonraki Sprint'e taşınmaktadır.

---

## 2.4 Veri Toplama Araçları ve Analiz Yöntemleri

### 2.4.1 EP-001 — Donanım Tasarımı ve Üretimi

**IP-1 kapsamında** aşağıdaki yöntemler uygulanmıştır:

- **PCB Tasarım Doğrulama:** KiCad EDA yazılımıyla gerçekleştirilen şematik ve layout tasarımı, DRC (Design Rule Check) ve ERC (Electrical Rule Check) kontrolleriyle doğrulanmıştır. Gerber ve BOM dosyaları üretim öncesi son kontrol sürecine tabi tutulmuştur.
- **Termal Analiz:** Güç devresi PCB layout'u, TPS54331 buck converter ve FUSB302 USB-C PD kontrolörü için termal simülasyon ile doğrulanmıştır.
- **Pil Ömrü Simülasyonu:** Güç tüketim hesaplamaları, bileşen datasheet değerleri ve ölçülen akım profilleri kullanılarak gerçekleştirilmiştir.
- **Fiziksel Testler:** IP54 toz/su sıçraması testi (IEC 60529 standardına göre), 1 metre düşme testi (3 farklı yüzey), –20°C/+60°C sıcaklık aralığı testi ve pil ömrü ölçümü (tam güç ve düşük güç modu) uygulanmıştır.

**Kullanılan Araçlar:** KiCad 7.x, Fusion 360 (3D CAD), dijital osiloskop, multimetre, iklim test kabini.

### 2.4.2 EP-002 — Firmware Geliştirme

**IP-2 kapsamında** aşağıdaki yöntemler uygulanmıştır:

- **Test-Driven Development (TDD):** Unity test çerçevesi kullanılarak her firmware modülü için birim testleri, implementasyondan önce yazılmıştır. Mock nesneler (mock SPI, mock ADC, mock I2S) gerçek donanım bağımlılıklarını izole etmek amacıyla kullanılmıştır.
- **Menzil Testi:** İki prototip arasında açık alanda gerçekleştirilen LoRa menzil testi; RSSI (Received Signal Strength Indicator) ve SNR (Signal-to-Noise Ratio) değerleri ölçülerek analiz edilmiştir.
- **Gecikme Ölçümü:** PTT ses iletim gecikmesi, donanım zamanlayıcıları ve loglama modülü kullanılarak milisaniye hassasiyetinde ölçülmüştür.
- **Ağ Simülasyonu:** 50 düğümlü mesh ağı simülasyonu, Meshtastic simülatörü ve özel Python test scriptleri kullanılarak gerçekleştirilmiştir.

**Kullanılan Araçlar ve Kütüphaneler:** PlatformIO, ESP-IDF v5.x, FreeRTOS, Meshtastic firmware fork, mbedTLS, Opus codec, LVGL, Unity test framework, Python (simülasyon scriptleri).

### 2.4.3 EP-003 — Mobil Uygulama

**IP-3 kapsamında** aşağıdaki yöntemler uygulanmıştır:

- **Çapraz Platform Geliştirme:** Flutter framework kullanılarak Android ve iOS platformlarında tek kod tabanından uygulama geliştirilmiştir.
- **Mock Tabanlı Birim Testleri:** BLE ve Wi-Fi bağlantı modülleri, mock servislerle izole edilerek test edilmiştir.
- **Erişilebilirlik Değerlendirmesi:** WCAG 2.1 AA standartlarına uygunluk, Flutter erişilebilirlik araçları ve manuel incelemeyle doğrulanmıştır.
- **Performans Profilleme:** Harita bileşeninin 50+ marker ile render performansı, Flutter DevTools kullanılarak analiz edilmiştir.

**Kullanılan Araçlar ve Kütüphaneler:** Flutter 3.x, Dart, flutter_blue_plus, flutter_map/mapbox_gl, sqflite (SQLite), flutter_secure_storage, mobile_scanner, qr_flutter, flutter_local_notifications, Flutter DevTools.

### 2.4.4 EP-004 — Web Yönetim Arayüzü

**IP-4 kapsamında** aşağıdaki yöntemler uygulanmıştır:

- **Gerçek Zamanlı İletişim Testi:** WebSocket bağlantısı üzerinden topoloji güncelleme gecikmesi, tarayıcı geliştirici araçları ve özel test scriptleriyle ölçülmüştür.
- **PWA Denetimi:** Lighthouse aracıyla PWA uyumluluk skoru, performans, erişilebilirlik ve SEO metrikleri değerlendirilmiştir.

**Kullanılan Araçlar ve Kütüphaneler:** React 18, Vite, D3.js/Cytoscape.js, Leaflet.js + OpenStreetMap, Chart.js/Recharts, Workbox, Jest, React Testing Library, Lighthouse.

### 2.4.5 EP-005 — Güvenlik ve Şifreleme

**IP-5 kapsamında** aşağıdaki yöntemler uygulanmıştır:

- **NIST CAVP Doğrulaması:** AES-256-GCM implementasyonu, NIST Cryptographic Algorithm Validation Program (CAVP) test vektörleriyle doğrulanmıştır. Bu yöntem, şifreleme modülünün standart uyumluluğunu nesnel biçimde kanıtlamaktadır.
- **Güvenlik Taraması:** OWASP ZAP (Zed Attack Proxy) ile web arayüzü ve API uç noktaları otomatik güvenlik taramasına tabi tutulmuştur.
- **Statik Analiz:** Firmware bağımlılıkları CVE (Common Vulnerabilities and Exposures) veritabanına karşı taranmıştır. Mobil uygulama MobSF (Mobile Security Framework) ile statik analize tabi tutulmuştur.
- **OWASP IoT Top 10 Uyumluluk Matrisi:** Her güvenlik maddesi için teknik kontrol ve test senaryoları tanımlanmış; sonuçlar uyumluluk matrisi formatında raporlanmıştır.

**Kullanılan Araçlar:** mbedTLS (Curve25519, AES-256-GCM, HKDF, HMAC-SHA256), OWASP ZAP, MobSF, NIST CAVP test vektörleri, ESP32 eFuse şifreli NVS.

### 2.4.6 EP-006 — Test, Kalite Güvence ve Dağıtım

**IP-6 kapsamında** aşağıdaki yöntemler uygulanmıştır:

- **Property-Based Testing:** Rastgele ağ topolojisi üreteci kullanılarak mesaj iletim oranı, AES-256-GCM round-trip, GPS koordinat round-trip ve yapılandırma serileştirme property testleri gerçekleştirilmiştir. Bu yaklaşım, önceden tanımlanamayan kenar durumlarını (edge cases) sistematik biçimde keşfetmeye olanak tanımaktadır.
- **Hardware-in-the-Loop (HIL) Test Otomasyonu:** 3 adet ESP32-S3 donanımından oluşan HIL test ortamı kurulmuş; güç modu geçişleri, OTA güncelleme, LoRa iletişimi ve GPS modülü test senaryoları otomatik olarak çalıştırılmıştır. HIL testlerinin gömülü sistem doğrulamasındaki önemi, Visteon ve NI tarafından yayımlanan teknik raporlarda kapsamlı biçimde belgelenmiştir [[HIL Testing, ResearchGate](https://www.researchgate.net/publication/228539346_An_Overview_of_Hardware-In-the-Loop_Testing_Systems_at_Visteon)].
- **Yük Testi:** 50 düğümlü ağ simülasyon ortamında paket iletim oranı, uçtan uca gecikme ve mesaj işleme kapasitesi (hedef: ≥ 100 msg/s) ölçülmüştür.
- **Kod Kapsamı Analizi:** gcov ve lcov araçlarıyla firmware kod kapsamı ölçülmüş; hedef ≥ %80 olarak belirlenmiştir.
- **CI/CD Pipeline:** GitHub Actions platformunda firmware derleme, Flutter Android/iOS derleme, React web derleme, birim test, entegrasyon test ve kod kapsamı raporu aşamalarından oluşan otomatik pipeline kurulmuştur. Pipeline tamamlanma süresi hedefi 30 dakika olarak belirlenmiştir.

**Kullanılan Araçlar:** Unity (firmware), Flutter test, Jest + React Testing Library (web), gcov/lcov, GitHub Actions, Docker/VM (simülasyon ortamı), OWASP ZAP, MobSF, MkDocs/Docusaurus.

---

## 2.5 Gantt Çizelgesi ve Zaman Planlaması

Projenin tüm görevleri, Ocak 2026 – Ağustos 2026 tarihleri arasında 16 Sprint'e yayılan günlük bazda bir Gantt çizelgesinde planlanmıştır. Çizelge; görev bağımlılıklarını, paralel yürütülebilecek iş akışlarını ve kritik yolu açıkça göstermektedir. Toplam 308 Story Point, 6 iş paketi ve 42 User Story, Sprint kapasitesine göre dengelenmiş biçimde dağıtılmıştır.

| Sprint Aralığı | Tarih | Temel Çıktı |
|---------------|-------|-------------|
| Sprint 1–3 | Oca–Şub 2026 | Donanım prototipi (EP-001) |
| Sprint 2–6 | Oca–Mar 2026 | Temel firmware + güvenlik temeli (EP-002, EP-005) |
| Sprint 7–9 | Mar–May 2026 | Gelişmiş firmware + mobil uygulama temeli (EP-002, EP-003) |
| Sprint 9–11 | Nis–Haz 2026 | Web arayüzü + test altyapısı (EP-004, EP-006) |
| Sprint 12–13 | Haz–Tem 2026 | CI/CD + HIL + mobil uygulama tamamlama (EP-006, EP-003) |
| Sprint 14–16 | Tem–Ağu 2026 | Yük testi + güvenlik taraması + v1.0.0 release (EP-006) |

---

## 2.6 Ön Çalışma ve Fizibilite

Projenin başlangıç aşamasında gerçekleştirilen fizibilite çalışmaları kapsamında şu bulgular elde edilmiştir:

- **LoRa Menzil Fizibilitesi:** SX1262 modülü ile SF10, BW125 kHz yapılandırmasında açık alanda 2 km'nin üzerinde iletişim menzili elde edilebileceği, Meshtastic topluluğunun saha testleri ve ilgili teknik belgelerle doğrulanmıştır.
- **ESP32-S3 Donanım Kapasitesi:** Dual-core 240 MHz işlemci ve 512 KB SRAM kapasitesinin FreeRTOS üzerinde 7 eş zamanlı görev, AES-256-GCM şifreleme ve Opus codec işlemlerini destekleyebileceği, ESP-IDF performans kılavuzları ve benzer projelerin teknik raporlarıyla desteklenmiştir.
- **Meshtastic Fork Uygunluğu:** Meshtastic'in açık kaynak lisansı (GPL-3.0) ve modüler mimarisi, projenin özel güvenlik ve yönlendirme gereksinimlerine uyarlanmasına elverişli bir temel sunmaktadır.
- **Flutter Çapraz Platform Uygunluğu:** Flutter'ın BLE, Wi-Fi ve yerel bildirim API'lerine erişim sağlayan olgun paket ekosistemi (flutter_blue_plus, flutter_map, flutter_secure_storage), mobil uygulama geliştirme için uygun bir platform olduğunu doğrulamaktadır.

---

## 2.7 Yöntemin Uygunluğunun Gerekçelendirilmesi

Seçilen araştırma yöntemi, projenin çok bileşenli ve çok disiplinli yapısıyla doğrudan örtüşmektedir. Agile Scrum'ın IoT sistemleri geliştirmesindeki etkinliği, Guerrero-Ulloa ve ark. (2023) tarafından ampirik olarak gösterilmiş; iteratif döngülerin donanım-yazılım entegrasyon hatalarını erken aşamada tespit ettiği ve proje başarı oranını artırdığı ortaya konmuştur [[MDPI Sensors, 2023](https://www.mdpi.com/1424-8220/23/2/790)]. TDD yaklaşımının gömülü sistemlerde uygulanması, Agile ve TDD metodolojilerini gömülü yazılım geliştirmeyle ilişkilendiren çalışmalar tarafından desteklenmektedir [[IREJ Journals, 2023](https://www.irejournals.com/paper-details/1705042)]. HIL test otomasyonunun gömülü sistem doğrulamasındaki rolü ise endüstriyel uygulamalar ve akademik çalışmalarla kapsamlı biçimde belgelenmiştir [[ResearchGate, HIL Assessment Methods](https://www.researchgate.net/publication/342114211_Hardware-in-the-Loop_Assessment_Methods)].

Property-based testing yaklaşımı, önceden tanımlanamayan kenar durumlarını sistematik biçimde keşfetmesi ve rastgele girdi üretimi yoluyla test kapsamını genişletmesi nedeniyle, güvenlik açısından kritik iletişim sistemlerinin doğrulanmasında özellikle uygun bir yöntem olarak değerlendirilmektedir. Bu yöntemin şifreleme ve ağ protokolü testlerinde kullanımı, yazılım güvenilirliği araştırmalarında giderek yaygınlaşmaktadır.

---

*İçerik, TÜBİTAK 2209-A başvuru formatına uygun akademik üslupta hazırlanmıştır.*
