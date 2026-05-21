# 1.2 Amaç ve Hedefler

---

## Proje Amacı

Bu projenin amacı; doğal afet, kentsel altyapı kesintisi ve uzak arazi operasyonları gibi hücresel ve internet altyapısının işlevsiz kaldığı koşullarda, LoRa ve Wi-Fi Mesh teknolojilerini, AES-256-GCM uçtan uca şifrelemeyi, gerçek zamanlı GPS konum takibini ve PTT sesli iletişimi tek bir taşınabilir IoT düğümünde bütünleşik biçimde çalıştıran; OWASP IoT Top 10 uyumlu, 50+ düğüm ölçeğinde doğrulanmış ve açık kaynaklı bir çevrimdışı iletişim sistemini tasarlamak, geliştirmek ve doğrulamaktır.

---

## Hedefler

Aşağıdaki hedefler SMART kriterlerine (Özgün, Ölçülebilir, Ulaşılabilir, İlgili, Zamana Bağlı) göre tanımlanmış olup her biri ilgili iş paketi (EP) ve Sprint çıktısıyla doğrudan ilişkilendirilmiştir.

---

### H-1 — Donanım Prototipinin Üretilmesi ve Doğrulanması
**İlgili İş Paketi:** EP-001 (Donanım Tasarımı ve Üretimi)
**Sprint Bağlantısı:** Sprint 1–3 | **Süre:** 05 Ocak – 13 Şubat 2026

ESP32-S3, SX1262 LoRa, u-blox NEO-M9N GPS, SSD1306 OLED, mikrofon/hoparlör ve USB-C PD devrelerini barındıran 4 katmanlı ana kart PCB tasarımı tamamlanacak; 18650 Li-ion pil, güneş paneli MPPT ve USB-C PD şarjı destekleyen güç yönetim devresi entegre edilecek; IP54 sertifikalı, 500 g altında ve –20°C ile +60°C arasında çalışabilir kasa tasarlanacak; en az 3 adet çalışan prototip üretilecek ve donanım gereksinimlerinin tamamı doğrulanacaktır.

> **Sprint 1 sonunda** PCB ana kart şematik ve layout dosyaları (Gerber + BOM) teslim edilecektir.
> **Sprint 2 sonunda** IP54 uyumlu 3D baskı kasa prototipi teslim edilecektir.
> **Sprint 3 sonunda** en az 3 adet çalışan donanım prototipi; LoRa menzil testi, GPS konum testi, IP54 toz/su testi, 1 m düşme testi ve pil ömrü ölçümü sonuçlarıyla birlikte teslim edilecektir.

**Başarı Ölçütü:** 3 prototipte LoRa menzili ≥ 2 km (açık alan), pil ömrü ≥ 72 saat (düşük güç modunda), IP54 testini geçme.

---

### H-2 — Temel Firmware Altyapısının ve Sürücü Katmanlarının Geliştirilmesi
**İlgili İş Paketi:** EP-002 (Firmware Geliştirme) — US-005, US-006, US-007, US-008, US-009
**Sprint Bağlantısı:** Sprint 2–6 | **Süre:** 19 Ocak – 27 Mart 2026

Meshtastic fork üzerinde FreeRTOS tabanlı modüler firmware altyapısı kurulacak; SX1262 LoRa sürücüsü (2–15 km menzil), ESP-MESH Wi-Fi Mesh modülü (≥ 8 kbps ses bant genişliği), u-blox NEO-M9N GPS sürücüsü (NMEA parser) ve pil seviyesine göre otomatik güç modu geçişleri (%20 ve %5 eşikleri) geliştirilecektir.

> **Sprint 2 sonunda** FreeRTOS görev iskeletleri, NVS yapılandırma modülü ve Unity test çerçevesi entegrasyonu teslim edilecektir.
> **Sprint 3 sonunda** LoRa sürücüsü gerçek donanımda menzil testiyle doğrulanmış olarak teslim edilecektir.
> **Sprint 4 sonunda** 3 düğümlü Wi-Fi Mesh ağı entegrasyon testi tamamlanmış olacaktır.
> **Sprint 5 sonunda** GPS soğuk/sıcak başlatma testi gerçek donanımda geçilmiş olacaktır.
> **Sprint 6 sonunda** güç modu geçiş testi gerçek donanımda doğrulanmış olacaktır.

**Başarı Ölçütü:** LoRa menzili ≥ 2 km, Wi-Fi Mesh bant genişliği ≥ 8 kbps, GPS soğuk başlatma ≤ 60 s, pil ömrü simülasyonu ≥ 72 saat.

---

### H-3 — Gelişmiş Firmware Modüllerinin Tamamlanması
**İlgili İş Paketi:** EP-002 (Firmware Geliştirme) — US-010, US-011, US-040, US-041, US-042
**Sprint Bağlantısı:** Sprint 7–9 | **Süre:** 30 Mart – 05 Mayıs 2026

SHA-256 doğrulamalı ve otomatik geri dönüşlü OTA firmware güncelleme mekanizması; 50–100+ düğüm destekli, flood ve Dijkstra tabanlı structured routing modları arasında dinamik geçiş yapabilen mesh ağ protokolü; LVGL tabanlı OLED cihaz arayüzü; Opus codec ile PTT sesli iletişim modülü (≤ 500 ms gecikme) ve telemetri firmware modülü geliştirilecektir.

> **Sprint 7 sonunda** OTA mekanizması gerçek donanımda test edilmiş, LVGL cihaz arayüzü ve Opus PTT ses modülü teslim edilecektir.
> **Sprint 8 sonunda** 50 düğümlü ağ simülasyonu ve yük testi tamamlanmış mesh protokolü teslim edilecektir.
> **Sprint 9 sonunda** telemetri modülü JSON dışa aktarma round-trip testiyle birlikte teslim edilecektir.

**Başarı Ölçütü:** OTA başarı oranı ≥ %99, PTT gecikmesi ≤ 500 ms, mesh protokolü 50 düğümde mesaj iletim oranı ≥ %99,9.

---

### H-4 — Güvenlik Altyapısının Kurulması ve OWASP Uyumluluğunun Doğrulanması
**İlgili İş Paketi:** EP-005 (Güvenlik ve Şifreleme) — US-025, US-026, US-027, US-028, US-029, US-030
**Sprint Bağlantısı:** Sprint 4–11 | **Süre:** 16 Şubat – 05 Haziran 2026

mbedTLS tabanlı AES-256-GCM şifreleme modülü (NIST CAVP test vektörleriyle doğrulanmış), Curve25519 ECDH anahtar değişimi ve HKDF kanal anahtarı türetimi, brute-force korumalı kimlik doğrulama sistemi, ESP32 eFuse tabanlı güvenli anahtar depolama ve HMAC korumalı güvenlik denetim kaydı geliştirilecek; sistemin OWASP IoT Top 10 uyumluluğu deneysel olarak doğrulanacaktır.

> **Sprint 4 sonunda** AES-256-GCM modülü NIST CAVP testleriyle doğrulanmış olarak teslim edilecektir.
> **Sprint 5 sonunda** ECDH anahtar değişimi ve JOIN protokol akışı teslim edilecektir.
> **Sprint 6 sonunda** kimlik doğrulama ve brute-force koruma modülü teslim edilecektir.
> **Sprint 8 sonunda** güvenli depolama (eFuse NVS) modülü teslim edilecektir.
> **Sprint 11 sonunda** OWASP IoT Top 10 uyumluluk raporu ve OWASP ZAP tarama sonuçları teslim edilecektir.

**Başarı Ölçütü:** NIST CAVP test vektörlerinin tamamında başarı, OWASP IoT Top 10 maddelerinin tamamında uyumluluk, ESP32-S3 donanım hızlandırıcısıyla şifreleme gecikmesi ≤ 10 ms/mesaj.

---

### H-5 — Flutter Mobil Uygulamasının Geliştirilmesi
**İlgili İş Paketi:** EP-003 (Mobil Uygulama) — US-012 ile US-018
**Sprint Bağlantısı:** Sprint 5–13 | **Süre:** 02 Mart – 03 Temmuz 2026

BLE/Wi-Fi üzerinden otomatik düğüm keşfi ve bağlantı yönetimi, mesh ağı üzerinden metin mesajlaşma (500 karakter, SQLite depolama), çevrimdışı harita destekli GPS konum görüntüleme (≤ 30 s güncelleme), şifreli kanal yönetimi (QR kod ile anahtar paylaşımı), PTT sesli iletişim arayüzü, arka plan bildirim servisi ve Türkçe/İngilizce lokalizasyon desteği geliştirilecektir.

> **Sprint 5 sonunda** BLE/Wi-Fi bağlantı modülü mock testleriyle teslim edilecektir.
> **Sprint 8 sonunda** harita ve konum görüntüleme modülü 50+ marker performans testiyle teslim edilecektir.
> **Sprint 9 sonunda** mesajlaşma ekranı ve kanal yönetimi WCAG 2.1 AA erişilebilirlik kontrolüyle teslim edilecektir.
> **Sprint 10 sonunda** PTT arayüzü ≤ 500 ms gecikme testiyle teslim edilecektir.
> **Sprint 13 sonunda** Türkçe/İngilizce lokalizasyon tüm ekranlarda doğrulanmış olarak teslim edilecektir.

**Başarı Ölçütü:** BLE tarama süresi ≤ 5 s, harita güncelleme ≤ 30 s, PTT gecikmesi ≤ 500 ms, dil değişikliği ≤ 500 ms, WCAG 2.1 AA uyumluluğu.

---

### H-6 — React Tabanlı Web Yönetim Arayüzünün Geliştirilmesi
**İlgili İş Paketi:** EP-004 (Web Yönetim Arayüzü) — US-019 ile US-024
**Sprint Bağlantısı:** Sprint 9–11 | **Süre:** 27 Nisan – 07 Haziran 2026

WebSocket tabanlı gerçek zamanlı ağ topoloji grafiği (D3.js/Cytoscape.js), düğüm yapılandırma ve yönetim arayüzü, OTA firmware güncelleme UI (ilerleme çubuğu + geri alma), telemetri zaman serisi grafikleri (Chart.js/Recharts, CSV export), kullanıcı ve kanal yönetimi (RBAC) ve PWA desteği (Workbox Service Worker, çevrimdışı cache) geliştirilecektir.

> **Sprint 9 sonunda** React + Vite proje altyapısı, dashboard ve topoloji grafiği PWA cache desteğiyle teslim edilecektir.
> **Sprint 10 sonunda** düğüm yönetimi ve telemetri grafikleri gerçek zamanlı güncelleme (≤ 10 s) testiyle teslim edilecektir.
> **Sprint 11 sonunda** OTA UI, kullanıcı/kanal yönetimi ve Lighthouse PWA denetimi tamamlanmış olarak teslim edilecektir.

**Başarı Ölçütü:** Topoloji grafiği ≤ 2 s yükleme, telemetri güncelleme ≤ 10 s, Lighthouse PWA skoru ≥ 90, çevrimdışı dashboard erişimi.

---

### H-7 — Kapsamlı Test, Kalite Güvence ve CI/CD Altyapısının Kurulması
**İlgili İş Paketi:** EP-006 (Test, Kalite Güvence ve Dağıtım) — US-031 ile US-039
**Sprint Bağlantısı:** Sprint 9–16 | **Süre:** 27 Nisan – 14 Ağustos 2026

Firmware (Unity), mobil (Flutter test) ve web (Jest + React Testing Library) bileşenleri için birim test altyapısı; 3 düğümlü Docker/VM simülasyon ortamında entegrasyon testleri; rastgele ağ topolojilerinde property-based testler (%99,9 mesaj iletim oranı); GitHub Actions tabanlı CI/CD pipeline (30 dakika hedefi); 3x ESP32-S3 donanımıyla HIL test otomasyonu; 50 düğümlü yük testi (≥ 100 msg/s); OWASP ZAP güvenlik taraması ve kapsamlı Türkçe/İngilizce dokümantasyon hazırlanacaktır.

> **Sprint 9 sonunda** birim test altyapısı ve kod kapsamı araçları (gcov/lcov) teslim edilecektir.
> **Sprint 10 sonunda** entegrasyon test ortamı ve CI/CD pipeline entegrasyonu teslim edilecektir.
> **Sprint 12 sonunda** property-based testler ve GitHub Actions CI/CD pipeline (≤ 30 dk) teslim edilecektir.
> **Sprint 13 sonunda** HIL test ortamı CI/CD entegrasyonuyla teslim edilecektir.
> **Sprint 14 sonunda** 50 düğümlü yük testi raporu ve OWASP ZAP güvenlik tarama raporu teslim edilecektir.
> **Sprint 15 sonunda** OpenAPI 3.0 dokümantasyonu, kullanıcı kılavuzu (TR/EN) ve MkDocs/Docusaurus statik site teslim edilecektir.
> **Sprint 16 sonunda** tüm bileşenlerin son entegrasyon testi tamamlanmış, v1.0.0 sürüm etiketi ve release notları yayımlanmış olacaktır.

**Başarı Ölçütü:** Kod kapsamı ≥ %80 (firmware), CI/CD pipeline süresi ≤ 30 dk, yük testinde ≥ 100 msg/s, güvenlik taramasında kritik/yüksek bulgu sayısı = 0.

---

## Hedef–İş Paketi–Sprint Özet Tablosu

| Hedef | İş Paketi | Sprint Aralığı | Bitiş Tarihi | Temel Ölçüt |
|-------|-----------|---------------|-------------|-------------|
| H-1: Donanım Prototipi | EP-001 | Sprint 1–3 | 13 Şub 2026 | 3 prototip, LoRa ≥ 2 km, IP54 |
| H-2: Temel Firmware | EP-002 (US-005–009) | Sprint 2–6 | 27 Mar 2026 | GPS ≤ 60 s, Wi-Fi ≥ 8 kbps |
| H-3: Gelişmiş Firmware | EP-002 (US-010–042) | Sprint 7–9 | 05 May 2026 | PTT ≤ 500 ms, mesh ≥ %99,9 |
| H-4: Güvenlik | EP-005 | Sprint 4–11 | 05 Haz 2026 | NIST CAVP, OWASP Top 10 |
| H-5: Mobil Uygulama | EP-003 | Sprint 5–13 | 03 Tem 2026 | WCAG 2.1 AA, PTT ≤ 500 ms |
| H-6: Web Arayüzü | EP-004 | Sprint 9–11 | 07 Haz 2026 | PWA ≥ 90, güncelleme ≤ 10 s |
| H-7: Test ve Dağıtım | EP-006 | Sprint 9–16 | 14 Ağu 2026 | CI/CD ≤ 30 dk, v1.0.0 release |
