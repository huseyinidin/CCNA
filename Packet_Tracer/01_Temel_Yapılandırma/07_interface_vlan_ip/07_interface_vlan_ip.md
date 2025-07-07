# 🌐 Interface VLAN ve IP Ayarı (SVI)

## 🧠 Nedir?

Switch'lerde doğrudan fiziksel arayüzlere IP adresi atanamaz. Bunun yerine **Switch Virtual Interface (SVI)** olarak adlandırılan `interface vlan` arayüzüne IP adresi atanarak, switch'e **uzaktan erişim (SSH, Telnet, ping)** gibi işlemler sağlanır.

---

## 🎯 Kullanım Amaçları

- Switch'e **ping atabilmek**
- Switch'i **uzaktan (Telnet / SSH) yönetebilmek**
- **VLAN bazlı yönetim** sağlamak

---

## 🔧 Konfigürasyon Adımları

### 1️⃣ VLAN Arayüzüne IP Adresi Atama

```
SW1> enable
SW1# configure terminal
SW1(config)# interface vlan 1
SW1(config-if)# ip address 192.168.1.2 255.255.255.0
SW1(config-if)# no shutdown
```

```
enable
configure terminal
interface vlan 1
ip address 192.168.1.2 255.255.255.0
no shutdown
```
### 2️⃣ Default Gateway Tanımlama

Switch’in VLAN dışındaki ağlara çıkabilmesi için gereklidir (örneğin uzaktaki bir SSH istemcisi).

```
SW1(config)# ip default-gateway 192.168.1.1
```

Bu komut yalnızca Layer 2 switch’ler içindir.
Layer 3 switch’lerde ip route komutu kullanılır.

---

### 🧪 Durum Kontrol Komutları

```
SW1# show ip interface brief
```

Bu komut ile tüm arayüzlerin IP, durum (up/down) ve VLAN bilgileri özetlenir.

---

### 🔒 Not

Eğer SVI'yi ping ya da SSH ile test etmek istiyorsan, aşağıdaki şartların sağlandığından emin ol:

- Switch’in VLAN arayüzü up durumda olmalı

- VLAN’a ait en az bir port aktif bağlı cihaz içermeli

- Default gateway doğru tanımlanmalı

- Uzak bilgisayarla aynı ağda olmalı veya router ile yönlendirme yapılmalı

