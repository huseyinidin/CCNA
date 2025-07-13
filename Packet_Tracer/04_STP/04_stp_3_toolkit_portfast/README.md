# 🧰 STP Toolkit Nedir?

**STP Toolkit**, Cisco tarafından geliştirilen ve Spanning Tree Protocol’ün (STP) ağlarda daha güvenli, hızlı ve kararlı çalışmasını sağlayan bir dizi özelliktir.

Bu toolkit, özellikle kampüs ağlarında ve büyük ölçekli kurumsal ağlarda **STP'nin eksiklerini telafi etmek**, **loop oluşumlarını önlemek** ve **STP hesaplamalarını hızlandırmak** amacıyla kullanılır.

---

## 🧩 STP Toolkit Bileşenleri

| Özellik               | Açıklama                                                                                   |
|------------------------|---------------------------------------------------------------------------------------------|
| **PortFast**           | Uç cihazlara bağlı portları doğrudan Forwarding moda geçirerek hızlı bağlantı sağlar.      |
| **BPDU Guard**         | PortFast etkin portlara BPDU gelirse, bu portu `err-disabled` durumuna getirir.            |
| **BPDU Filter**        | BPDU trafiğini bastırır. İstenirse hem gönderim hem alımı engeller.                        |
| **Root Guard**         | Yetkisiz switch’lerin Root Bridge olmasını engeller.                                       |
| **Loop Guard**         | Root veya Alternate portların ani forwarding durumuna geçmesini önleyerek loop riskini azaltır. |
| **UDLD (Unidirectional Link Detection)** | Tek yönlü (tek taraflı çalışan) bağlantıları algılar ve devre dışı bırakır.          |
| **EtherChannel Guard** | Yanlış yapılandırılmış EtherChannel bağlantılarını algılar ve portu korumaya alır.         |
| **Bridge Assurance**   | (Nexus switch'lerde) BPDU alışverişi kesilirse portu otomatik olarak bloklar.              |

---

## 🎯 STP Toolkit Ne İşe Yarar?

- 🔐 **Ağ Güvenliğini Artırır:**  
  Rogue (yetkisiz) switch bağlantılarını engeller. Loop oluşumunu önler.

- ⚡ **Hızlı Ağ Erişimi Sağlar:**  
  PortFast ile kullanıcı cihazları beklemeden ağa bağlanır (özellikle DHCP açısından kritik).

- 🔄 **Topoloji Hatalarını Önler:**  
  Hatalı kablolamalar veya ani STP değişimlerine karşı önleyici koruma sağlar.

- 🌐 **Ağ Kararlılığını Artırır:**  
  STP hesaplamaları daha kontrollü ve istikrarlı yapılır.

---

## 🏢 Nerelerde Kullanılır?

- Büyük ölçekli kurumsal LAN (yerel ağ) yapılarında  
- Üniversite, hastane ve kampüs ağlarında  
- Cisco Switch tabanlı erişim katmanlarında (Access Layer)  
- Özellikle uç cihazlara bağlı portların bulunduğu yerlerde

---

# ⚡ STP PortFast Nedir?

**PortFast**, uç cihazlara (PC, yazıcı, IP telefon gibi) bağlı switch portlarının,  
STP'nin normal bekleme sürecini (**Listening → Learning → Forwarding**) atlayarak  
**doğrudan Forwarding moduna** geçmesini sağlar.

Bu sayede cihazlar **ağa çok daha hızlı bağlanır**  
ve **DHCP gibi servislerde gecikme** yaşanmaz.

---

## 🛠 STP Portfast Yapılandırması
```
Switch(config)# interface  fastEthernet 0/1
Switch(config-if)# switchport mode access
Switch(config-if)# spanning-tree portfast
```
```
interface  fastEthernet 0/1
switchport mode access
spanning-tree portfast
```

### ⚠️ **PortFast Uyarısı:**  
- PortFast sadece uç cihazlara (PC, yazıcı vb.) bağlı **access portlarda** kullanılmalıdır.  
- Eğer bu porta bir switch veya hub bağlanırsa **loop riski** oluşur.  
- Ayrıca, PortFast yalnızca **trunk olmayan portlarda** etkili olur.

```
Switch(config)# spanning-tree portfast default     ! Tüm access portlarda PortFast otomatik etkinleşir
Switch(config)# spanning-tree portfast disable     ! Global PortFast özelliğini tamamen devre dışı bırakır

```

```
spanning-tree portfast default 
spanning-tree portfast disable 
```
---

## 🔁 `spanning-tree portfast disable` Ne Yapar?

### 📌 Açıklama

```
Switch(config)# spanning-tree portfast disable
```
Bu komut, switch üzerindeki tüm PortFast özelliğini global olarak devre dışı bırakır.

## 🔁 Sonuç: Ne Olur?

Daha önce **access modda** olup otomatik **PortFast etkin** olan tüm portlardan bu özellik kaldırılır.

### 🎯 Bu nedenle:

- 🕒 **DHCP gecikmeleri** yaşanabilir  
- 💻 **PC'lerin ağa bağlanması 30-50 saniye** gecikebilir  
- 🚫 **Hızlı erişim gereken kullanıcılar** bağlantı sorunları yaşayabilir

## 🧠 Notlar

- `spanning-tree portfast disable` komutu sadece **global (varsayılan)** PortFast davranışını kapatır.  
- Daha önce **manuel olarak yapılandırılmış** `spanning-tree portfast` komutları bu durumdan **etkilenmez** ve çalışmaya devam eder.