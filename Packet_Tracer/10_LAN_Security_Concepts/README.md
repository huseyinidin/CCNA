# 🔐 LAN Security Concepts

Yerel Ağ (LAN - Local Area Network) güvenliği, bir kuruluşun iç ağını dış tehditlere ve iç risklere karşı koruma sürecidir. LAN, genellikle bir ev, ofis veya kurum içindeki cihazların birbirine bağlandığı bir ağdır. Bu belge, LAN güvenliğinin temel kavramlarını ve uygulamalarını kapsamlı bir şekilde açıklamaktadır.

## 📚 İçindekiler

- [LAN Nedir?](#lan-nedir)
- [LAN Güvenliği Neden Önemlidir?](#lan-güvenliği-neden-önemlidir)
- [Temel LAN Güvenlik Tehditleri](#temel-lan-güvenlik-tehditleri)
- [LAN Güvenliğini Sağlama Yöntemleri](#lan-güvenliğini-sağlama-yöntemleri)
- [Güvenlik Politikaları ve İzleme](#güvenlik-politikaları-ve-izleme)
- [En İyi Uygulamalar (Best Practices)](#en-iyi-uygulamalar-best-practices)

---

## 🖧 LAN Nedir?

LAN (Local Area Network), sınırlı bir alandaki bilgisayarlar, yazıcılar, sunucular ve diğer cihazların birbirine bağlandığı bir ağ türüdür. Genellikle Ethernet veya Wi-Fi teknolojisi kullanılır.

---

## ❗ LAN Güvenliği Neden Önemlidir?

- Yetkisiz erişimi önlemek
- Hassas verileri korumak
- Zararlı yazılım yayılımını engellemek
- Ağ içi saldırıları (ör. Man-in-the-Middle, ARP Spoofing) tespit etmek
- Uyum (compliance) gerekliliklerini sağlamak

---

## 🛡️ Temel LAN Güvenlik Tehditleri

| Tehdit Türü           | Açıklama                                                                 |
|------------------------|--------------------------------------------------------------------------|
| **ARP Spoofing**       | Saldırgan, ağda kendisini başka bir cihaz gibi göstererek trafik yakalar. |
| **MAC Flooding**       | Switch'e sahte MAC adresleri gönderilerek MAC tablosu doldurulur.         |
| **Man-in-the-Middle**  | İki cihaz arasındaki iletişime gizlice müdahale edilir.                   |
| **Yetkisiz Erişim**    | Güvenlik açıkları kullanılarak ağa izinsiz giriş sağlanır.                 |
| **Virüs/Solucanlar**   | Ağ üzerinden yayılan zararlı yazılımlar sistemlere zarar verebilir.        |

---

## 🔧 LAN Güvenliğini Sağlama Yöntemleri

### 1. 🔐 **Ağ Erişim Kontrolü (NAC)**

- Cihazların ağa erişmeden önce kimlik doğrulaması yapılır.
- 802.1X protokolü kullanılabilir.

### 2. 🛠️ **VLAN (Virtual LAN) Kullanımı**

- Ağ trafiğini izole ederek segmentlere ayırmak.
- Misafir kullanıcılar ile iç ağ kullanıcılarını ayırmak.

### 3. 🚫 **Port Security (Anahtar Seviyesinde Güvenlik)**

- Switch portlarına belirli MAC adresleri atamak.
- Belirlenmeyen cihazların bağlantısını engellemek.

### 4. 🔍 **IDS/IPS (Saldırı Tespit ve Önleme Sistemleri)**

- Ağ trafiğini analiz eder ve şüpheli etkinlikleri bildirir.
- Anormallikler tespit edilirse önlem alır.

### 5. 🔄 **Ağ Donanım Güncellemeleri**

- Switch, router ve firewall firmware’leri güncel tutulmalı.
- Güvenlik açıkları hızlıca kapatılmalı.

### 6. 🌐 **Güvenlik Duvarları (Firewalls)**

- İç ve dış ağlar arasında trafik kontrolü sağlar.
- Kurallar belirlenerek sadece izinli trafiğe geçiş izni verilir.

---

## 🧾 Güvenlik Politikaları ve İzleme

- **Kullanıcı Rolleri ve Yetkilendirme:** Kim neye erişebilir netleştirilmeli.
- **Loglama ve İzleme:** Ağ aktiviteleri düzenli olarak kaydedilmeli.
- **Düzenli Denetimler:** Zayıf noktaların tespiti için periyodik testler yapılmalı (örneğin penetration testing).

---

## ✅ En İyi Uygulamalar (Best Practices)

- **Güçlü parolalar ve MFA (çok faktörlü kimlik doğrulama) kullanımı**
- **Kablosuz ağlar için WPA3 veya en güncel şifreleme yöntemlerinin tercih edilmesi**
- **Ağ cihazlarının fiziksel güvenliği**
- **Düzenli yedekleme (backup) politikalarının uygulanması**
- **Çalışanlar için siber güvenlik farkındalık eğitimleri**

---

## 📌 Sonuç

LAN güvenliği, kurumların veri güvenliği, süreklilik ve yasal yükümlülükleri açısından hayati öneme sahiptir. Güçlü bir LAN güvenliği stratejisi, sadece teknoloji değil aynı zamanda politika, eğitim ve izleme bileşenlerini de içermelidir.

> Unutmayın: **Güvenli bir ağ, sadece saldırılara karşı korunan değil, aynı zamanda sürekli izlenen ve güncellenen bir ağdır.**

---

## 📚 **Konu Özetlerine buradan ulaşabilirsiniz** 

- [*Endpoint Security:*](https://github.com/huseyinidin/CCNA/tree/main/Packet_Tracer/10_LAN_Security_Concepts/EndpointSecurity.md)
- [*Access Control:*](https://github.com/huseyinidin/CCNA/tree/main/Packet_Tracer/10_LAN_Security_Concepts/AccessControl.md)
- [*Layer 2 Security Threats:*](https://github.com/huseyinidin/CCNA/tree/main/Packet_Tracer/10_LAN_Security_Concepts/Layer2SecurityThreats.md)
- [*Mac Address Table Attack:*](https://github.com/huseyinidin/CCNA/tree/main/Packet_Tracer/10_LAN_Security_Concepts/MacAddressTableAttack.md)
- [*Lan Attacks:*](https://github.com/huseyinidin/CCNA/tree/main/Packet_Tracer/10_LAN_Security_Concepts/LanAttacks.md)