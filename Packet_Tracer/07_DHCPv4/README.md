# 📡 DHCPv4 Nedir?

## 📘 Tanım

**DHCPv4 (Dynamic Host Configuration Protocol for IPv4)**, IPv4 ağlarında istemcilere otomatik olarak IP adresi, ağ geçidi, DNS sunucusu ve diğer ağ yapılandırma bilgilerini atayan bir protokoldür.  
Bu protokol, **RFC 2131** ile tanımlanmıştır.

---

## 🎯 Amacı

- Manuel IP adresi atamasını ortadan kaldırmak
- Ağ yöneticilerinin iş yükünü azaltmak
- IP adreslerinin verimli, hatasız ve merkezi şekilde yönetilmesini sağlamak
- Ağ üzerinde IP çakışmalarını önlemek

---

## 🌐 Nerelerde Kullanılır?

DHCPv4, aşağıdaki ortamlarda yaygın olarak kullanılır:

- Kurumsal LAN ve WLAN ağları
- Ev ağları
- İnternet servis sağlayıcıları (ISP)
- Wi-Fi hotspot alanları
- DHCP Relay kullanılarak farklı subnetlerdeki istemcilerde

---

## 🔍 Temel Kavramlar

| Kavram              | Açıklama                                                                 |
|---------------------|--------------------------------------------------------------------------|
| **DHCP Sunucusu**   | IP ve yapılandırma bilgilerini dağıtan merkezi cihaz                     |
| **DHCP İstemcisi**  | IP adresi talebinde bulunan cihaz (PC, yazıcı, telefon, vb.)             |
| **Kiralama (Lease)**| Bir istemciye verilen IP adresinin geçerlilik süresi                    |
| **DHCP Discover**   | İstemcinin yayın (broadcast) ile IP arayışı başlattığı ilk mesaj         |
| **DHCP Offer**      | Sunucunun istemciye IP adresi ve yapılandırma önerdiği mesaj             |
| **DHCP Request**    | İstemcinin bir teklif üzerine talepte bulunduğu mesaj                    |
| **DHCP Acknowledge**| Sunucunun istemciye IP’yi tahsis ettiğini onayladığı mesaj               |
| **DHCP NAK**        | Geçersiz isteklerde sunucunun red cevabı                                |
| **DHCP Decline**    | İstemcinin önerilen IP'nin kullanılmakta olduğunu bildirmesi             |

---

## 🧠 DHCPv4 Nasıl Çalışır? (DORA Süreci)

1. **D**iscover → İstemci ağda sunucu arar.  
2. **O**ffer → Sunucu IP önerir.  
3. **R**equest → İstemci, önerilen IP’yi talep eder.  
4. **A**ck → Sunucu, IP'yi kiralar ve onaylar.

> Bu işleme **DORA süreci** denir.

---

## ⚙️ DHCPv4 Özellikleri

- 🔁 **Otomatik IP Atama**  
- 🧭 **Opsiyonel Ayarlar (DNS, ağ geçidi, subnet maskesi vs.)**  
- 📅 **Kiralama Süresi Yönetimi**  
- 🌍 **DHCP Relay Agent Desteği (`ip helper-address`)**  
- 🛡️ **MAC Adresine Göre Statik IP Rezervasyonu (Reservation)**  
- 🔄 **Kiralama Yenileme Mekanizması**

---

## ❗ Ek Bilgiler

- **DHCP Snooping**: Switch’lerde sahte DHCP sunucularını engellemek için kullanılan bir güvenlik önlemidir.
- **DHCPv6**: IPv6 ağlarında kullanılan benzer bir protokoldür.
- **BOOTP ve DHCP Farkı**: BOOTP sabit yapılandırmalıyken, DHCP dinamik olarak çalışır ve daha esnektir.

---

## 🧪 Örnek Topoloji


- PC1 → DHCP istemcisi  
- Router → DHCP sunucusu  
- Switch → VLAN 10 yapılandırması yapılabilir  

---

## 🔧 Örnek: IP Aralığını Rezerve Et (Hariç Tut)

**Önce rezerve edilmek istenen IP aralığı hariç tutulur.**

Aşağıdaki örnekte, 192.168.10.1 ila 192.168.10.10 arasındaki IP’ler rezervasyon veya manuel atama için ayrılmıştır:
```
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.10
```

```
ip dhcp excluded-address 192.168.10.1 192.168.10.10

```

## 📌 Sonuç

Cisco IOS'ta **IP aralığı için rezervasyon işlemi**, doğrudan değil ama `ip dhcp excluded-address` komutuyla **dolaylı olarak** yapılır.  
Bu şekilde belirli IP adresleri DHCP havuzunun dışında tutulur ve genellikle sunucular, yazıcılar veya statik IP gerektiren cihazlar için ayrılır.

---

## 🧰 Cisco IOS Üzerinde DHCPv4 Konfigürasyonu

```
Router(config)# ip dhcp pool IT
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 8.8.8.8
Router(dhcp-config)# lease 7    				!Bu komut paket tracer üzerinde çalışmaz! 
```
```
Router(config)# interface g0/0.10
Router(config-if)# ip address 192.168.10.1 255.255.255.0
Router(config-if)# no shutdown
```

```
ip dhcp pool IT
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
lease 7    				 			!istemcilere verilen IP adreslerinin **ne kadar süreyle geçerli olacağını** belirtir.
```
```
interface g0/0.10
ip address 192.168.10.1 255.255.255.0
no shutdown
```
---
