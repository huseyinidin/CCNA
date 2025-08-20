# 🔐 ARP Attacks (ARP Saldırılarından Korunma)

## 📌 Giriş

**Address Resolution Protocol (ARP)**, IPv4 ağlarında cihazların IP adreslerini MAC adreslerine çözümlemesini sağlayan temel bir protokoldür.  
Ancak ARP, kimlik doğrulama veya güvenlik mekanizmasına sahip değildir. Bu durum, saldırganların **sahte ARP yanıtları** göndererek **ARP Spoofing/Poisoning** saldırıları yapmasına yol açar.  

Sonuç olarak:

- Trafik saldırganın cihazı üzerinden yönlendirilebilir.
- Orta adam (Man-in-the-Middle, MITM) saldırıları gerçekleşebilir.
- Veri gizliliği ve bütünlüğü tehlikeye girebilir.

---

## ⚠️ ARP Saldırıları Neden Olur?

- **ARP'nin güvenliksiz tasarımı**: ARP mesajlarının doğrulanmaması.  
- **Switch ortamında şeffaflık**: Tüm istemciler ARP yanıtlarını kolayca alabilir.  
- **Ağ segmentinde kontrolsüz cihazlar**: Yetkisiz cihazların ağa dahil olması.  

---

## 🎯 Amaç

ARP saldırılarını azaltmak için kullanılabilecek **ağ güvenlik mekanizmalarını** öğrenmek ve uygulamak.  
Amaç, **ağın bütünlüğünü, gizliliğini ve erişilebilirliğini** korumaktır.  

---

## 🛡️ ARP Saldırılarından Korunma Yöntemleri

### 1. **Dynamic ARP Inspection (DAI)**

DAI, switch üzerinde gelen ARP paketlerini denetler.  
ARP yanıtlarının doğruluğu **DHCP Snooping** veritabanı veya **statik güvenilir girişler** üzerinden kontrol edilir.  
Yanlış ARP girişleri otomatik olarak **drop** edilir.

---

## ✅ Sonuç

ARP protokolü doğası gereği güvenliksizdir ve saldırganlar için önemli bir saldırı yüzeyi oluşturur.
Dynamic ARP Inspection, DHCP Snooping, Port Security ve ağ erişim kontrolleri ile ARP saldırılarının büyük ölçüde önüne geçilebilir.

Bu önlemler:

- Ağın güvenilirliğini artırır
- MITM saldırılarını önler
- Kritik verilerin korunmasını sağlar

---

## ⚙️ Örnek Konfigürasyonlar

```
ip dhcp snooping
ip dhcp snooping vlan 50 
ip arp inspection vlan 50 
```

```
interface fastEthernet 0/24
ip dhcp snooping trust
ip arp inspection trust 
```






