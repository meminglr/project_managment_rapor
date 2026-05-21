# 3.3 Araştırma Olanakları Tablosu

> *Bu tabloda yalnızca mevcut (var olan) altyapı ve araçlar listelenmiştir. Proje kapsamında satın alınacak malzemeler bütçe tablosunda ayrıca belirtilmiştir.*

---

## A. Donanım Altyapısı

| Altyapı / Ekipman Türü ve Modeli | Projede Kullanım Amacı |
|----------------------------------|------------------------|
| **Geliştirici Bilgisayarı** — Apple MacBook (macOS, min. 16 GB RAM, 512 GB SSD) | Tüm yazılım geliştirme, derleme, simülasyon ve test faaliyetleri için birincil geliştirme ortamı. **IP-1, IP-2, IP-3, IP-4, IP-5, IP-6** |
| **Dijital Osiloskop** — 2 kanallı, min. 100 MHz bant genişliği | PCB güç devresi doğrulama, SPI/I2C/UART sinyal analizi, PTT gecikme ölçümü ve LoRa interrupt zamanlaması doğrulama. **IP-1, IP-2** |
| **Dijital Multimetre** — True RMS, akım ölçüm özellikli | Güç tüketimi ölçümü, pil ömrü hesaplama, devre kısa devre kontrolü ve voltaj regülatörü doğrulama. **IP-1** |
| **Lehim İstasyonu** — Sıcaklık kontrollü, min. 350°C | SMD bileşen montajı (reflow veya el lehimi), prototip PCB üretimi ve onarım işlemleri. **IP-1** |
| **3D Yazıcı** — FDM tipi (PLA/PETG malzeme desteği) | IP54 uyumlu kasa prototiplerinin üretimi, mekanik tasarım doğrulama ve iteratif kasa revizyonları. **IP-1** |
| **Android Akıllı Telefon** — min. Android 10, BLE 5.0 destekli | Flutter mobil uygulamasının Android platformunda gerçek cihaz testi, BLE bağlantı doğrulama ve PTT gecikme ölçümü. **IP-3** |
| **iOS Akıllı Telefon** — min. iOS 15, BLE 5.0 destekli | Flutter mobil uygulamasının iOS platformunda gerçek cihaz testi, Background App Refresh ve bildirim servisi doğrulama. **IP-3** |

---

## B. Yazılım Geliştirme Araçları

| Altyapı / Ekipman Türü ve Modeli | Projede Kullanım Amacı |
|----------------------------------|------------------------|
| **KiCad 7.x** — Açık kaynak, ücretsiz | PCB şematik tasarımı, 4 katmanlı layout, DRC/ERC kontrolleri, Gerber ve BOM dosyası üretimi. **IP-1** |
| **Autodesk Fusion 360** — Eğitim lisansı (ücretsiz) | IP54 uyumlu kasa 3D CAD modeli, mekanik montaj simülasyonu ve 3D baskı dosyası (STL) üretimi. **IP-1** |
| **PlatformIO IDE** — Açık kaynak, ücretsiz (VS Code eklentisi) | ESP32-S3 firmware geliştirme ortamı, derleme, flash yükleme ve seri port monitörü. **IP-2** |
| **ESP-IDF v5.x** — Açık kaynak, Apache 2.0 lisansı | ESP32-S3 için resmi geliştirme çerçevesi; FreeRTOS, mbedTLS, ESP-MESH, NVS ve OTA API'leri. **IP-2, IP-5** |
| **Meshtastic Firmware Fork** — Açık kaynak, GPL-3.0 lisansı | Mesh ağ protokolü temel altyapısı; commit hash sabitlenmiş fork üzerinde özel geliştirmeler yapılmaktadır. **IP-2** |
| **mbedTLS (ESP-IDF entegre)** — Açık kaynak, Apache 2.0 lisansı | AES-256-GCM şifreleme, Curve25519 ECDH anahtar değişimi, HKDF, HMAC-SHA256 implementasyonu. **IP-5** |
| **LVGL v8.x** — Açık kaynak, MIT lisansı | SSD1306 OLED ekran için gömülü grafik arayüz kütüphanesi; cihaz UI widget'ları ve menü navigasyonu. **IP-2** |
| **Opus Codec** — Açık kaynak, BSD lisansı | PTT sesli iletişim için düşük gecikmeli ses sıkıştırma/açma (8 kbps, ≤ 500 ms gecikme hedefi). **IP-2** |
| **Unity Test Framework** — Açık kaynak, MIT lisansı | Firmware bileşenleri için C dili birim test çerçevesi; mock SPI, mock ADC, mock I2S nesneleriyle izole test. **IP-2, IP-6** |
| **Flutter 3.x / Dart** — Açık kaynak, BSD lisansı | Android ve iOS için çapraz platform mobil uygulama geliştirme ortamı. **IP-3** |
| **Flutter Paketleri** — Açık kaynak (pub.dev): flutter_blue_plus, flutter_map, sqflite, flutter_secure_storage, mobile_scanner, qr_flutter, flutter_local_notifications, flutter intl | Mobil uygulamanın BLE bağlantı, harita, veritabanı, güvenli depolama, QR kod, bildirim ve lokalizasyon modülleri. **IP-3** |
| **Flutter DevTools** — Açık kaynak, BSD lisansı | Mobil uygulama performans profilleme, bellek analizi ve harita render performansı ölçümü. **IP-3** |
| **React 18 + Vite** — Açık kaynak, MIT lisansı | Web yönetim arayüzü geliştirme ortamı; hızlı derleme ve HMR (Hot Module Replacement) desteği. **IP-4** |
| **D3.js / Cytoscape.js** — Açık kaynak, BSD/MIT lisansı | Gerçek zamanlı ağ topoloji grafiği görselleştirme; düğüm-kenar ilişkileri ve bağlantı kalitesi renk kodlaması. **IP-4** |
| **Leaflet.js + OpenStreetMap** — Açık kaynak, BSD lisansı / CC BY-SA | Web arayüzünde düğüm GPS konumlarının harita üzerinde görüntülenmesi. **IP-4** |
| **Chart.js / Recharts** — Açık kaynak, MIT lisansı | Telemetri zaman serisi grafikleri (pil, RSSI, SNR, sensör verileri) ve CSV export. **IP-4** |
| **Workbox** — Açık kaynak, MIT lisansı (Google) | PWA Service Worker implementasyonu; çevrimdışı cache stratejisi ve dashboard offline desteği. **IP-4** |
| **Jest + React Testing Library** — Açık kaynak, MIT lisansı | Web arayüzü bileşenleri için birim ve entegrasyon testleri. **IP-4, IP-6** |
| **Visual Studio Code** — Ücretsiz, MIT lisansı | Tüm yazılım geliştirme faaliyetleri için birincil kod editörü; PlatformIO, Flutter ve React eklentileriyle. **IP-2, IP-3, IP-4, IP-5** |
| **Git + GitHub** — Ücretsiz (public/private repo) | Sürüm kontrolü, branch yönetimi, Pull Request süreci ve v1.0.0 sürüm etiketleme. **IP-2, IP-3, IP-4, IP-5, IP-6** |

---

## C. Test ve Kalite Güvence Araçları

| Altyapı / Ekipman Türü ve Modeli | Projede Kullanım Amacı |
|----------------------------------|------------------------|
| **GitHub Actions** — Ücretsiz (public repo) / aylık 2000 dakika (private repo) | CI/CD pipeline otomasyonu; firmware derleme, Flutter/React derleme, birim test, entegrasyon test ve kod kapsamı raporu aşamaları. **IP-6** |
| **Docker Desktop** — Ücretsiz (kişisel kullanım) | 3 düğümlü mesh simülasyon ortamı kurulumu; entegrasyon test konteynerleri ve izole test ortamları. **IP-6** |
| **gcov / lcov** — Açık kaynak, GPL lisansı | Firmware C kodu için satır ve dal kapsamı ölçümü; hedef ≥ %80 kod kapsamı. **IP-6** |
| **OWASP ZAP (Zed Attack Proxy) 2.x** — Açık kaynak, Apache 2.0 lisansı | Web yönetim arayüzü ve API uç noktaları otomatik güvenlik taraması; kritik/yüksek bulgu tespiti. **IP-5, IP-6** |
| **MobSF (Mobile Security Framework)** — Açık kaynak, GPL-3.0 lisansı | Flutter mobil uygulaması statik güvenlik analizi; izin kontrolü, şifreleme kullanımı ve güvenlik açığı tespiti. **IP-5, IP-6** |
| **NIST CAVP Test Vektörleri** — Kamuya açık, ücretsiz | AES-256-GCM implementasyonunun standart uyumluluğunun doğrulanması; resmi NIST test vektör dosyaları. **IP-5** |
| **Lighthouse (Chrome DevTools entegre)** — Açık kaynak, Apache 2.0 lisansı | PWA uyumluluk skoru, performans, erişilebilirlik ve SEO metrikleri değerlendirmesi; hedef ≥ 90 puan. **IP-4, IP-6** |
| **Meshtastic Simülatörü** — Açık kaynak, GPL-3.0 lisansı | 50 düğümlü mesh ağı simülasyonu; flood ve structured routing performans karşılaştırması. **IP-2, IP-6** |
| **Python 3.x** — Açık kaynak, PSF lisansı | Yük testi scriptleri, rastgele ağ topolojisi üreteci (property-based test), HIL test otomasyon scriptleri ve veri analizi. **IP-6** |
| **MkDocs / Docusaurus** — Açık kaynak, MIT lisansı | Türkçe/İngilizce kullanıcı kılavuzu ve OpenAPI 3.0 dokümantasyonu için statik site üretimi. **IP-6** |

---

## D. Proje Yönetimi Araçları

| Altyapı / Ekipman Türü ve Modeli | Projede Kullanım Amacı |
|----------------------------------|------------------------|
| **monday.com** — SaaS, Pro lisansı | Agile Scrum proje yönetimi; Product Backlog yönetimi, Sprint planlama, User Story ve Subtask takibi, Gantt çizelgesi, iş paketi ilerleme izleme ve Sprint Review raporlama. Projenin tüm 6 iş paketi (IP-1 – IP-6), 42 User Story ve 308 Story Point bu platform üzerinde yönetilmektedir. **IP-1, IP-2, IP-3, IP-4, IP-5, IP-6** |
| **GitHub Projects** — Ücretsiz | Kod deposuyla entegre Sprint board; Pull Request ve Issue'ların User Story'lerle ilişkilendirilmesi, kod inceleme (code review) süreci yönetimi. **IP-2, IP-3, IP-4, IP-5, IP-6** |
| **Slack / Discord** — Ücretsiz | Daily Scrum iletişimi, Sprint engel bildirimleri ve GitHub Actions CI/CD bildirim entegrasyonu. **IP-1, IP-2, IP-3, IP-4, IP-5, IP-6** |
