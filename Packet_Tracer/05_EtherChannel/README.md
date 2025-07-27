# 🔗 EtherChannel Nedir?

**EtherChannel**, birden fazla fiziksel Ethernet portunu tek bir mantıksal bağlantı (port-channel) gibi birleştiren bir teknolojidir.  
Switch'ler arasında bant genişliğini artırmak ve bağlantı yedekliliği sağlamak için kullanılır.

---

## 🎯 EtherChannel Avantajları

- ⚡ **Artan Bant Genişliği**: 2, 4, 8 gibi port birleştirilerek daha yüksek hız sağlanır (örneğin 4x1G = 4 Gbps).
- 🔄 **Yedeklilik**: Fiziksel bağlantılardan biri koparsa trafik kalan bağlantılardan devam eder.
- 🚫 **Loop Engelleme**: STP tüm portları tek bir bağlantı gibi görür, loop oluşmaz.
- 🔧 **Kolay Yönetim**: Birden çok port, tek bir port-channel arayüzü üzerinden yönetilir.

---

## 🔁 Otomatik Anlaşma Protokolleri

| Protokol | Açılımı | Açıklama |
|----------|---------|----------|
| **LACP** | Link Aggregation Control Protocol | IEEE 802.3ad standardı, vendor bağımsız |
| **PAgP** | Port Aggregation Protocol | Cisco’ya özel, sadece Cisco cihazlarda çalışır |

**Statik EtherChannel** ise hiçbir protokol kullanılmadan manuel olarak yapılandırılır.

---

## ⚙️ EtherChannel Yapılandırma (Cisco)

### LACP ile (önerilen – otomatik)

```
interface range f0/1 - 2
channel-group 1 mode active
```

### Port-channel Arayüz Ayarları

```
interface port-channel1
switchport mode trunk
switchport trunk allowed 1,2,10 
```

vlan 10 
name IT 
vlan 20 
name HR 
vlan 30 
name ARGE
 
int fa 0/3
switchport mode access 
switchport acc vlan 10 
int fa 0/4
switchport mode access 
switchport acc vlan 20
int fa 0/5
switchport mode access 
switchport acc vlan 30