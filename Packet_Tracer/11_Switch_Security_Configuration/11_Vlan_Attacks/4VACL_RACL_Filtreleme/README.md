---

## 4️⃣ VLAN Bazlı ACL (RACL) Konfigürasyonu Access Control List (RACL) ile Filtreleme

Cisco 2960 Layer 2 switch VACL (VLAN ACL) özelliğini desteklemez. Bunun yerine PACL (Port ACL) kullanılabilir. Yani filtrelemeyi VLAN bazlı değil, port bazlı yapabilirsin.

 ===============================

 1️⃣ Layer 2 Switch (2960) Konfigürasyonu

 ===============================

```

 VLAN’ları oluştur

vlan 10
 name IT
vlan 20
 name HR

 Trunk portu router’a bağla

interface GigabitEthernet 0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20
 no shutdown

 Uç kullanıcı portları

interface fastEthernet0/1
 switchport mode access
 switchport access vlan 10
 no shutdown

interface fastEthernet0/2
 switchport mode access
 switchport access vlan 10
 no shutdown

interface fastEthernet0/3
 switchport mode access
 switchport access vlan 20
 no shutdown
```

 ===============================

 2️⃣ Router (2911) Konfigürasyonu

 ===============================

```

 Alt interface’ler ile VLAN’ları yapılandır

interface gigabitEthernet0/0
 no shutdown

interface gigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 Bu interface VLAN 10 gateway’i

interface gigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
 Bu interface VLAN 20 gateway’i
```

 ===============================

 3️⃣ VLAN Bazlı ACL (RACL) Konfigürasyonu

 ===============================

```

 Extended ACL oluştur, VLAN 10 trafiğini kontrol etmek için

ip access-list extended VLAN10-BLOCK
 deny ip host 192.168.10.51 any   # VLAN 10’daki 192.168.10.51 IP adresinden gelen tüm trafiği engeller
 permit ip any any                  # Diğer tüm trafiğe izin verir
 exit                               # ACL tanımından çıkar
```

 ACL’i VLAN 10 subinterface’ine uygula

```
interface gigabitEthernet0/0.10
 ip access-group VLAN10-BLOCK in    # Giriş yönünde (VLAN 10’dan router’a gelen) trafiğe ACL uygular

```
---

💡 Notlar:

- Bu ACL VLAN 10 alt interface’ine uygulandığı için, VLAN 10 içi ve VLAN 10’dan diğer VLAN’lara giden trafiği kontrol eder.
- Diğer VLAN’lar için de aynı şekilde ayrı ACL’ler oluşturup ilgili subinterface’lere uygulayabilirsin.

---