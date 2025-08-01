# 🌐 SLAAC ve DHCPv6 Kavramları

## 📘 Tanım

**DHCPv6 (Dynamic Host Configuration Protocol for IPv6)**, IPv6 ağlarında istemcilere otomatik olarak IP adresi, DNS sunucusu ve diğer yapılandırma bilgilerini sağlayan bir protokoldür.

IPv6'da adres yapılandırması için üç temel yöntem vardır:

### 📦 Çalışma Modları

1. **SLAAC** (Stateless Address Autoconfiguration)  
2. **Stateful DHCPv6** (Tam adres ve tüm bilgiler DHCPv6 sunucusundan alınır)  
3. **Stateless DHCPv6** (Adres SLAAC ile, ek bilgiler DHCPv6 ile alınır)

---

## 🔧 SLAAC (Stateless Address Autoconfiguration)

### 🔍 1. SLAAC Nedir?

**SLAAC**, IPv6 cihazlarının ağ yönlendiricisinden aldığı yönlendirme ilanları (RA - Router Advertisement) ile kendi IP adreslerini otomatik olarak yapılandırmalarını sağlayan yöntemdir.

### ⚙️ Nasıl Çalışır?

1. Cihaz, ağa bağlandığında bir **Router Solicitation (RS)** mesajı gönderir.
2. Router, **Router Advertisement (RA)** mesajı ile ağ bilgilerini (prefix ve diğer bayraklar) gönderir.
3. Cihaz, RA içindeki **prefix** bilgisini ve kendi MAC adresini kullanarak **EUI-64 formatında** bir IPv6 adresi üretir.
4. Cihaz, bu adresin ağda benzersiz olup olmadığını kontrol etmek için **Duplicate Address Detection (DAD)** yapar.
5. Eğer çakışma yoksa IP adresi kullanıma alınır.

### 🧩 Özellikleri

- DHCP sunucusuna gerek yoktur.
- IP adresi, yönlendiricinin gönderdiği prefix ile cihaz tarafından oluşturulur.
- **Stateless** (durumsuz) olduğu için sunucu istemci bilgisi tutmaz.
- DNS adresleri gibi ek bilgiler RA mesajı içinde ya da DHCPv6 ile alınabilir.

### 🛠️ SLAAC DHCPv6 Konfigürasyonu 

- Router üzerindeki interface'e IPv6 adresi vererek SLAAC'ı otomatik başlatmış olursunuz. RA mesajları otomatik olarak gönderilir.

```
Router(config)# ipv6 unicast-routing
Router(config)# interface g0/0
Router(config-if)# ipv6 address 2001:DB8:10::1/64
Router(config-if)# no shutdown
```

```
ipv6 unicast-routing
interface g0/0
ipv6 address 2001:DB8:10::1/64
no shutdown
```
- Bu yapılandırmadan sonra g0/0 arayüzünde RA mesajları gönderilmeye başlanır. SLAAC aktif hale gelir.

---

## 🖥️ DHCPv6 (Dynamic Host Configuration Protocol for IPv6)

### 🔷 2. Stateful DHCPv6 Nedir?

> **DHCPv6 sunucusu**, istemcilere **IP adresi**, **DNS** ve **diğer bilgileri** tamamen kendisi sağlar.  
> RA mesajında **M (Managed) bayrağı = 1**, **O (Other Config) bayrağı = 1** olur.

### ✅ Özellikleri

- IP adresi tamamen DHCPv6 sunucusu tarafından atanır.
- DNS, domain name gibi ek bilgiler de sunucudan gelir.
- Router sadece yönlendirici olarak davranır, adres atamaz.
- Ağ yöneticisi istemci adreslerini merkezi olarak izleyebilir.

### 🛠️ Stateful DHCPv6 Konfigürasyonu 

```
Router>enable
Router#configure terminal 
```
```
Router(config)#ipv6 unicast-routing
```
```
Router(config)#ipv6 dhcp pool STATEFUL-IT
Router(config-dhcpv6)#address prefix 2001:DB8:8000:1::/64
Router(config-dhcpv6)#dns-server 2001:DB8:8000:1::2
Router(config-dhcpv6)#domain-name cisco.local
Router(config-dhcpv6)#exit 
```
```
Router(config)#interface gigabitEthernet 0/0
Router(config-if)#ipv6 address 2001:DB8:8000:1::1/64
Router(config-if)#ipv6 dhcp server STATEFUL-IT
Router(config-if)#ipv6 nd managed-config-flag
Router(config-if)#ipv6 nd other-config-flag
Router(config-if)#no shutdown   
```

```
enable 
configure terminal 
ipv6 unicast-routing
```

**! DHCPv6 havuzu oluştur**
```
ipv6 dhcp pool STATEFUL-IT
address prefix 2001:DB8:8000:1::/64
dns-server 2001:DB8:8000:1::2
domain-name cisco.local
```

**! Arayüze adres ve DHCPv6 havuzu bağla**
```
interface gigabitEthernet 0/0
ipv6 address 2001:DB8:8000:1::1/64
ipv6 dhcp server STATEFUL-IT
ipv6 nd managed-config-flag
ipv6 nd other-config-flag
no shutdown   
```
---

## 🔶 3. Stateless DHCPv6 Nedir?

> **Stateless DHCPv6**, istemcinin IPv6 adresini **SLAAC** (Stateless Address Autoconfiguration) yöntemiyle oluşturduğu, ancak **DNS sunucusu, domain ismi** gibi diğer yapılandırma bilgilerini **DHCPv6 sunucusundan aldığı** bir yöntemdir.

### 🔧 Teknik Açıklama

- IPv6 adresi: Router Advertisement (RA) mesajı sayesinde istemci tarafından otomatik oluşturulur.
- IP adresi SLAAC ile alınır, **sadece ek bilgiler (DNS, domain)** DHCPv6 sunucusundan alınır.
- RA mesajında:
  - **M (Managed) = 0** ⟶ Adres DHCP'den alınmayacak.
  - **O (Other Config) = 1** ⟶ Diğer bilgiler DHCP'den alınacak.

### ✅ Özellikleri

- Ağ daha az konfigürasyon gerektirir.
- Adres takibi yapılamaz çünkü DHCP sunucusu adres dağıtmaz.
- SLAAC'ın esnekliği ile DHCPv6'nın bazı avantajlarını birleştirir.
- DHCP sunucusu yükü daha azdır.

### 🛠️ Stateless DHCPv6 Konfigürasyonu 

```
Router>enable
Router#configure terminal 
```
```
Router(config)#ipv6 unicast-routing
```
```
Router(config)#ipv6 dhcp pool STATELESS-HR
Router(config-dhcpv6)#dns-server 2001:DB8:8000:2::2
Router(config-dhcpv6)#domain-name hr.local
Router(config-dhcpv6)#exit 
```
```
Router(config)#interface gigabitEthernet 0/0
Router(config-if)#ipv6 address 2001:DB8:8000:2::1/64
Router(config-if)#ipv6 dhcp server STATELESS-HR
Router(config-if)#ipv6 nd other-config-flag
Router(config-if)#no shutdown   
```

```
enable 
configure terminal 
ipv6 unicast-routing
```

**! DHCPv6 havuzu oluştur**
```
ipv6 dhcp pool STATELESS-HR
dns-server 2001:DB8:8000:2::2
domain-name hr.local
```

**! Arayüze IPv6 adresi ver, havuzu bağla ve RA bayraklarını ayarla**
```
interface gigabitEthernet 0/0
ipv6 address 2001:DB8:8000:2::1/64
ipv6 dhcp server STATELESS-HR
ipv6 nd other-config-flag
no shutdown   
```
---

### ⚙️ DHCPv6 İşleyiş Adımları

1. Cihaz RA mesajını alır.
2. RA içindeki bayraklara göre (M veya O bitleri) DHCPv6 istemcisi devreye girer.
3. DHCPv6 sunucusuyla **Solicit → Advertise → Request → Reply** mesajları ile IP veya diğer bilgiler alınır.

---

## 🧾 RA Mesaj Bayrakları

| Bayrak | Anlamı | Açıklama |
|--------|--------|---------|
| **M** (Managed) | 1 ise | IP adresi DHCPv6'dan alınır (Stateful) |
| **O** (Other) | 1 ise | Sadece ek bilgiler DHCPv6'dan alınır (Stateless) |

---

## 🔍 SLAAC ve DHCPv6 Karşılaştırması

| Özellik           | SLAAC                    | DHCPv6                         |
|-------------------|--------------------------|--------------------------------|
| IP Adresi Atama   | Otomatik (RA üzerinden)  | DHCPv6 sunucusundan            |
| Ek Bilgiler (DNS) | RA ile ya da DHCPv6      | DHCPv6                         |
| Sunucu Gerekir mi?| Hayır                    | Evet                           |
| Durum Takibi      | Stateless (Durumsuz)     | Stateful (Durumlu) olabilir    |
| Kullanım Alanı    | Küçük-orta ağlar         | Orta-büyük kurumsal ağlar      |

---

## 📌 Notlar

- SLAAC genellikle basit ağlarda yeterlidir.
- DHCPv6 daha fazla yönetim ve denetim imkânı sunar.
- IPv6, SLAAC ve DHCPv6'yı birlikte kullanacak şekilde esnek tasarlanmıştır.

---

# 🌐 Neighbor Discovery Protocol (NDP) – Sorgu Protokolleri

## 📘 Tanım

**Neighbor Discovery Protocol (NDP)**, IPv6 ağlarında cihazların birbirini keşfetmesi, adres çözümlemesi, yönlendirici keşfi ve otomatik adres yapılandırması gibi görevleri yerine getirmek için kullanılan ICMPv6 tabanlı bir protokoldür.

IPv4’te kullanılan aşağıdaki protokollerin yerini alır:

- ARP (Adres çözümleme)
- ICMP ( yönlendirici keşfi )
- DHCP (bazı durumlarda)
- RARP ve ICMP Redirect

---

## 🔍 NDP Sorgu Protokolleri (5 Ana ICMPv6 Mesaj Türü)

| # | Protokol Adı                 | ICMPv6 Tip No | Açıklama |
|---|-------------------------------|---------------|----------|
| 1 | **Router Solicitation (RS)** | `133`         | Host → Router: Yönlendirici keşfetme isteği gönderir. |
| 2 | **Router Advertisement (RA)**| `134`         | Router → Host: Ağ bilgilerini gönderir (prefix, MTU, bayraklar). |
| 3 | **Neighbor Solicitation (NS)**| `135`        | Host → Host: Hedefin MAC adresini öğrenmek için (ARP yerine). |
| 4 | **Neighbor Advertisement (NA)**| `136`       | Host → Host: MAC adresini bildiren yanıt mesajı. |
| 5 | **Redirect**                 | `137`         | Router → Host: Daha iyi bir rota varsa bildirir. |

---

## 📌 Kısa Açıklamalar

### 1. 🛰️ Router Solicitation (RS) – Tip 133
- Host, ağa yeni bağlandığında yönlendiriciye "Kimsin, bana ağ bilgilerini gönder" anlamında bir mesaj gönderir.
- Bu mesaj sayesinde RA (Router Advertisement) mesajının tetiklenmesi sağlanır.

### 2. 📡 Router Advertisement (RA) – Tip 134
- Router, ağdaki tüm hostlara periyodik olarak veya RS aldığında RA mesajı gönderir.
- Prefix, default gateway, MTU, DHCPv6 kullanılıp kullanılmayacağı gibi bilgiler içerir.

### 3. 🧭 Neighbor Solicitation (NS) – Tip 135
- IPv4’teki ARP işlevini görür.
- Bir IPv6 adresinin MAC adresini öğrenmek veya Duplicate Address Detection (DAD) yapmak için gönderilir.

### 4. 🪪 Neighbor Advertisement (NA) – Tip 136
- NS mesajına verilen yanıttır.
- "Benim MAC adresim bu" diyerek hedef adresin kimliğini doğrular.

### 5. 🛣️ Redirect – Tip 137
- Router, bir host’a daha uygun bir yönlendirici veya yol önerdiğinde gönderilir.
- Yüksek maliyetli rotaları engellemek için kullanılır.

---

## 🧠 Ek Bilgiler

- Tüm bu mesajlar **ICMPv6** üzerinden çalışır.
- IPv6’da **ARP yoktur**, bunun yerine NS ve NA kullanılır.
- SLAAC (Stateless Address Autoconfiguration), RS ve RA mesajlarıyla çalışır.
- RA mesajlarında `M` ve `O` bayrakları, DHCPv6 kullanımını belirler.

---

## 🖥️ NDP Mesaj Akışı Örneği

```
[ Host ]
   |
   |--- RS --->  (Tip 133)
   |<-- RA ---   (Tip 134)
   |
   |--- NS --->  (Tip 135)
   |<-- NA ---   (Tip 136)
   |
   |<-- Redirect (Tip 137, opsiyonel)
```
---

## 🔐 Güvenlik Notu

NDP mesajları, sahte **RA (Router Advertisement)** veya **NA (Neighbor Advertisement)** mesajları gönderilerek kötüye kullanılabilir. Bu durum, özellikle:

- Sahte yönlendirici tanıtımları (Rogue RA)
- MAC adres sahteciliği (Spoofing)
- Trafik yönlendirme veya dinleme (Man-in-the-Middle)

gibi güvenlik tehditlerine neden olabilir.

IPv6 ağlarında bu tür saldırılara karşı aşağıdaki önlemler alınmalıdır:

- ✅ **RA Guard**: Switch seviyesinde sahte RA mesajlarını engeller.
- ✅ **IPv6 ACL (Access Control List)**: Belirli ICMPv6 mesajlarının trafiğini filtreler.
- ✅ **ND Inspection (Neighbor Discovery Inspection)**: Meşru komşu ilişkilerini denetler ve doğrular.


