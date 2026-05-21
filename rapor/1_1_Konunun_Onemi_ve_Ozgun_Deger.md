# 1.1 Konunun Önemi, Araştırma Önerisinin Özgün Değeri ve Araştırma Sorusu / Hipotezi

---

## 1.1.1 Konunun Kapsamı ve Sınırları

Bu araştırma, altyapıya bağımlı olmaksızın çalışabilen, taşınabilir ve çevrimdışı bir taktik iletişim sisteminin tasarımını, geliştirilmesini ve doğrulanmasını kapsamaktadır. Sistem; LoRa (Long Range) radyo teknolojisi üzerinde çalışan çok atlamalı (multi-hop) mesh ağı, Wi-Fi Mesh (ESP-MESH) protokolü, uçtan uca AES-256-GCM şifreleme, ECDH anahtar değişimi, gerçek zamanlı GPS konum takibi, Push-to-Talk (PTT) sesli iletişim, Flutter tabanlı çapraz platform mobil uygulama ve React tabanlı web yönetim arayüzünden oluşan bütünleşik bir mimari üzerine inşa edilmiştir.

Araştırmanın kapsamı; donanım tasarımı (ESP32-S3 + SX1262 LoRa + u-blox NEO-M9N GPS), gömülü yazılım (FreeRTOS tabanlı firmware), uygulama katmanı yazılımları ve güvenlik altyapısını birlikte ele almaktadır. Araştırma, ticari ölçekli üretim optimizasyonunu, uydu iletişim entegrasyonunu ve lisanslı frekans bantlarında çalışmayı kapsam dışında tutmaktadır. Hedef kullanım senaryoları; afet ve acil durum müdahalesi, kentsel altyapı kesintileri, uzak arazi operasyonları ve kritik altyapı güvenliğinin sağlanamadığı ortamlardır.

---

## 1.1.2 Literatürdeki Mevcut Çalışmalar ve Eleştirel Değerlendirme

Altyapıdan bağımsız kablosuz iletişim sistemleri üzerine yürütülen akademik çalışmalar, son on yılda belirgin biçimde artmıştır. Bu alandaki temel çalışmalar birkaç ana eksen etrafında kümelenmektedir.

**LoRa/LoRaWAN Tabanlı Afet İletişimi:** Centelles ve ark. (2019), deprem sonrası koordinasyon için LoRa tabanlı bir iletişim sistemi önermiş; ancak bu çalışma yalnızca tek atlamalı (single-hop) metin iletimini ele almış, ses iletişimi ve güvenlik katmanını kapsam dışında bırakmıştır [[Centelles et al., 2019, MDPI Proceedings, doi:10.3390/proceedings2019031073](https://www.mdpi.com/2504-3900/31/1/73)]. Benzer biçimde, Springer bünyesinde yayımlanan düşük maliyetli acil durum iletişim sistemleri üzerine yapılan çalışmalar, LoRa modüllerinin afet bölgelerinde kullanılabilirliğini göstermiş; ancak bu sistemlerin büyük çoğunluğu şifreleme mekanizması içermemekte ya da yalnızca LoRaWAN altyapısına bağımlı kalmaktadır [[Springer, 2024, doi:10.1007/978-981-97-8336-6_21](https://link.springer.com/chapter/10.1007/978-981-97-8336-6_21)].

**Meshtastic ve Altyapısız Mesh Ağlar:** Meshtastic protokolü, düşük güçlü LoRa donanımı üzerinde altyapısız mesh iletişimi sağlayan açık kaynaklı bir çerçeve olarak öne çıkmaktadır. Akademik literatürde Meshtastic'in IoT uygulamalarıyla entegrasyonunu inceleyen çalışmalar mevcuttur [[Researchgate, 2022](https://www.researchgate.net/publication/357994440_Meshtastic_Infrastructure-less_Networks_for_Reliable_Data_Transmission_to_Augment_Internet_of_Things_Applications)]; bununla birlikte bu çalışmalar, protokolün güvenlik açıklarını —özellikle varsayılan şifreleme yapılandırmasının yetersizliğini ve replay saldırısı risklerini— yeterince ele almamaktadır. 2024 tarihli teknik analizde de Meshtastic'in flood routing mekanizmasının büyük ağlarda ölçeklenebilirlik sorunları yarattığı ve yapılandırılmış yönlendirme (structured routing) desteğinin sınırlı kaldığı vurgulanmaktadır [[Critical Analysis of the Meshtastic Protocol, 2024](https://disk91.com/2024/technology/lora/critical-analysis-of-the-meshtastic-protocol/)].

**Güvenlik ve Şifreleme:** IoT cihazlarında uçtan uca şifreleme üzerine yapılan çalışmalar, AES-256 ve ECDH protokollerinin gömülü sistemlerde uygulanabilirliğini doğrulamıştır [[MDPI Computers, 2025](https://www.mdpi.com/2073-431X/15/5/308)]. Ancak bu çalışmaların büyük bölümü, şifreleme modülünü bağımsız bir bileşen olarak ele almakta; mesh ağ protokolü, güç yönetimi ve ses iletişimiyle bütünleşik bir sistem mimarisi sunmamaktadır. OWASP IoT Top 10 kılavuzu, IoT sistemlerindeki en kritik güvenlik açıklarını tanımlamış olsa da bu kılavuzun LoRa mesh sistemlerine özgü uygulamasını doğrulayan deneysel çalışmalar oldukça sınırlıdır [[OWASP IoT Top 10](https://owasp.org/www-project-internet-of-things/)].

**Sesli İletişim ve PTT:** Gömülü sistemlerde gerçek zamanlı sesli iletişim üzerine yapılan çalışmalar, genellikle Wi-Fi veya hücresel ağ altyapısına bağımlı çözümler sunmaktadır. Opus codec'in düşük bant genişliğinde (8 kbps) çevrimdışı mesh ağı üzerinden çalıştırılması ve PTT gecikmesinin 500 ms altında tutulması, literatürde yeterince araştırılmamış bir teknik problemdir.

**Tespit Edilen Temel Eksiklikler:**

1. Mevcut çalışmaların büyük çoğunluğu, LoRa iletişimi, güvenlik, ses ve konum takibini **ayrı bileşenler** olarak ele almakta; bu bileşenlerin tek bir taşınabilir cihazda bütünleşik biçimde çalışmasını sağlayan sistem düzeyinde bir mimari sunmamaktadır.
2. Meshtastic tabanlı sistemlerde **ECDH anahtar değişimi + AES-256-GCM + HMAC-SHA256** üçlüsünün birlikte uygulandığı ve OWASP IoT Top 10 uyumluluğunun deneysel olarak doğrulandığı bir çalışma bulunmamaktadır.
3. Flood routing ile Dijkstra tabanlı structured routing arasında **dinamik geçiş mekanizması** içeren ve 50+ düğüm ölçeğinde doğrulanmış bir mesh protokol implementasyonu literatürde yer almamaktadır.
4. Çevrimdışı mesh ağı üzerinden **OTA (Over-the-Air) firmware güncellemesi** ile **SHA-256 doğrulamalı geri dönüş mekanizmasının** birlikte çalıştığı bir sistem tasarımı akademik düzeyde belgelenmemiştir.
5. Söz konusu sistemlerin **Hardware-in-the-Loop (HIL) test ortamında** otomatik doğrulanması ve CI/CD pipeline'a entegrasyonu, gömülü sistem araştırmalarında henüz yaygınlaşmamış bir yaklaşımdır.

---

## 1.1.3 Projenin Özgün Katkısı ve Yenilik Boyutu

Bu araştırma, yukarıda tespit edilen eksiklikleri gidermek amacıyla aşağıdaki özgün katkıları sunmaktadır:

**Kavramsal Özgünlük:** Proje, "çevrimdışı iletişim" kavramını yalnızca metin iletimi düzeyinde değil; sesli iletişim (PTT), konum paylaşımı, telemetri ve güvenli kanal yönetimini kapsayan **çok modlu, bütünleşik bir iletişim ekosistemi** olarak yeniden tanımlamaktadır. Bu yaklaşım, mevcut literatürdeki parçalı çözüm anlayışından metodolojik olarak ayrışmaktadır.

**Teknolojik Özgünlük:** Tek bir ESP32-S3 mikrodenetleyici üzerinde LoRa (SX1262, 2–15 km menzil), Wi-Fi Mesh (ESP-MESH), GPS (u-blox NEO-M9N), ses (Opus codec, I2S), OLED arayüz (LVGL) ve güç yönetimi (MPPT + BMS) bileşenlerinin **eş zamanlı ve kesintisiz** çalıştırılması, donanım-yazılım entegrasyonu açısından özgün bir teknik katkı oluşturmaktadır.

**Güvenlik Mimarisi Özgünlüğü:** AES-256-GCM şifreleme, ECDH (Curve25519) anahtar değişimi, HKDF ile kanal anahtarı türetimi, HMAC-SHA256 mesaj bütünlüğü ve replay saldırısı önleme mekanizmalarının **tek bir gömülü sistemde katmanlı biçimde** uygulanması ve OWASP IoT Top 10 kılavuzuna uygunluğunun deneysel olarak doğrulanması, güvenlik araştırmaları açısından somut bir metodolojik katkı sunmaktadır.

**Metodolojik Özgünlük:** Projenin doğrulama sürecinde kullanılan **property-based test** yaklaşımı (rastgele ağ topolojilerinde %99,9 mesaj iletim oranı hedefi), **HIL (Hardware-in-the-Loop) test otomasyonu** ve **CI/CD pipeline entegrasyonu** (30 dakika hedefi), gömülü sistem araştırmalarında henüz standart hale gelmemiş ileri düzey kalite güvence yöntemlerini temsil etmektedir.

**Pratik Özgünlük:** Sistemin 500 g altında, IP54 sertifikalı, güneş paneli destekli ve –20°C ile +60°C arasında çalışabilir olması; hem akademik hem de operasyonel kullanım senaryolarında doğrulanabilir performans ölçütleri sunmaktadır.

---

## 1.1.4 Araştırma Sorusu

> **Altyapıdan tamamen bağımsız, taşınabilir bir IoT düğümü üzerinde; LoRa ve Wi-Fi Mesh protokollerini, AES-256-GCM uçtan uca şifrelemeyi, gerçek zamanlı GPS konum takibini ve PTT sesli iletişimi bütünleşik biçimde çalıştıran, OWASP IoT Top 10 uyumlu ve 50+ düğüm ölçeğinde doğrulanmış bir çevrimdışı iletişim sistemi tasarlamak ve gerçekleştirmek mümkün müdür?**

---

## 1.1.5 Hipotez

**H₁ (Ana Hipotez):** ESP32-S3 tabanlı, FreeRTOS üzerinde çalışan ve Meshtastic protokolünden türetilmiş bir mesh firmware mimarisi; AES-256-GCM şifreleme, ECDH anahtar değişimi, Opus codec PTT ses iletimi ve u-blox NEO-M9N GPS entegrasyonunu tek bir donanım platformunda eş zamanlı olarak destekleyebilir ve bu sistem, 50 düğümlü bir ağda %99,9 mesaj iletim oranını, 500 ms altında PTT gecikmesini ve 2 km'nin üzerinde LoRa menzilini aynı anda karşılayabilir.

**H₀ (Null Hipotez):** Söz konusu bileşenlerin tek bir kısıtlı donanım platformunda eş zamanlı çalıştırılması, işlemci ve bellek kısıtları nedeniyle belirtilen performans eşiklerinin en az birinin karşılanamamasına yol açar.

---

## Önerilen Literatür Atıfları

> *Not: Aşağıdaki atıflar yer tutucu niteliğindedir. Gerçek DOI ve tam künye bilgileri araştırmacı tarafından doğrulanmalı ve güncellenmelidir.*

1. **[Centelles et al., 2019]** — Centelles, R., Freitag, F., Meseguer, R., Navarro, L., Ochoa, S. F., & Santos, R. M. (2019). A LoRa-Based Communication System for Coordinated Response in an Earthquake Aftermath. *MDPI Proceedings, 31*(1), 73.
   🔗 https://www.mdpi.com/2504-3900/31/1/73

2. **[Researchgate, 2022]** — Meshtastic Infrastructure-less Networks for Reliable Data Transmission to Augment Internet of Things Applications. *ResearchGate*, 2022.
   🔗 https://www.researchgate.net/publication/357994440_Meshtastic_Infrastructure-less_Networks_for_Reliable_Data_Transmission_to_Augment_Internet_of_Things_Applications

3. **[disk91.com, 2024]** — Critical Analysis of the Meshtastic Protocol: Scalability and Security Limitations in Large-Scale Mesh Deployments. *(Teknik analiz, Ağustos 2024 — Akademik kaynak ile desteklenmesi önerilir.)*
   🔗 https://disk91.com/2024/technology/lora/critical-analysis-of-the-meshtastic-protocol/

4. **[MDPI Computers, 2025]** — Performance Evaluation of Lightweight Cryptographic Algorithms for End-to-End Secure IoT Data Transmission over 5G Standalone. *MDPI Computers, 15*(5), 308.
   🔗 https://www.mdpi.com/2073-431X/15/5/308

5. **[Springer, 2024]** — Low Cost Emergency Communication System for Disaster Affected Areas. *Springer*, 2024.
   🔗 https://link.springer.com/chapter/10.1007/978-981-97-8336-6_21

6. **[OWASP IoT Top 10]** — OWASP Internet of Things Top 10 Security Vulnerabilities. *OWASP Foundation.*
   🔗 https://owasp.org/www-project-internet-of-things/

---

*İçerik, TÜBİTAK 2209-A başvuru formatına uygun akademik üslupta hazırlanmıştır. Literatür atıfları yer tutucu niteliğinde olup araştırmacı tarafından güncel ve erişilebilir kaynaklarla desteklenmelidir.*
