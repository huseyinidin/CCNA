# 🌐 Inter-VLAN Routing Nedir?

**Inter-VLAN Routing**, farklı VLAN’lar arasında cihazların birbiriyle iletişim kurmasını sağlayan işlemdir.  
Çünkü varsayılan olarak **VLAN’lar birbirleriyle iletişim kuramaz.**

---

## 🎯 Amaç

- VLAN 10’daki bir cihazın VLAN 20’deki bir cihaza veri gönderebilmesi için bir **katman 3 yönlendirme (routing)** gerekir.
- Bu işlem bir **Router** ya da **Layer 3 Switch** ile yapılır.

---

## 🔄 Inter-VLAN Routing Türleri

### 1. 🌐 **Geleneksel Inter-VLAN Routing**
- Her VLAN için router üzerinde fiziksel port kullanılır.
- Eski yöntemdir, çok port gerektirir, verimsizdir.

---

## 🛠 Gerekli Yapılandırma Bileşenleri

- VLAN tanımları
- Trunk bağlantılar
- Router veya L3 switch yapılandırması
- Her VLAN’a ait IP adresleri
- Cihazlara doğru **default gateway** verilmesi

---

## ✅ Örnek Senaryo

| VLAN | Ağ               | IP Aralığı          | Default Gateway      |
|------|------------------|---------------------|----------------------|
| 10   | IT               | 192.168.10.0/24     | 192.168.10.1         |
| 20   | HR               | 192.168.20.0/24     | 192.168.20.1         |

> VLAN 10'daki PC → Gateway (10.1) → Routing → VLAN 20'deki PC ile haberleşebilir.

---

## 📌 Notlar

- Layer 2 switch’ler Inter-VLAN Routing yapamaz.
- Layer 3 switch ya da router gerekir.
- Her VLAN’ın bir **SVI ya da alt arayüzü** ve IP adresi olmalıdır.

### 🛠 Inter-Vlan Routing Switch Yapılandırması

```
Switch(config)#vlan 10 
Switch(config-vlan)#name IT 
Switch(config-vlan)#exit
Switch(config-)#vlan 20 
Switch(config-vlan)#name HR 
Switch(config-vlan)#exit 
Switch(config)#
Switch(config)#interface range fastEthernet 0/1-2
Switch(config-if-range)#switchport mode access 
Switch(config-if-range)#switchport access vlan 10

Switch(config)#interface range fastEthernet 0/3-4
Switch(config-if-range)#switchport mode access 
Switch(config-if-range)#switchport access vlan 20 
Switch(config-if-range)#
```

```
vlan 10 
name IT 
exit
vlan 20 
name HR 
exit 
interface range fastEthernet 0/1-2
switchport mode access 
switchport access vlan 10

interface range fastEthernet 0/3-4
switchport mode access 
switchport access vlan 20 
```


### 🛠 Inter-Vlan Routing Router Yapılandırması

```
Router>enable 
Router#configure terminal 
Router(config)#hostname R1 
R1(config)#interface gigabitethernet 0/1
R1(config-if)#ip address 192.168.10.1 255.255.255.0 
R1(config-if)#no shutdown

R1(config-if)#interface gigabitethernet 0/2
R1(config-if)#ip address 192.168.20.1 255.255.255.0
R1(config-if)#no shutdown 
```

```
enable 
configure terminal 
hostname R1 
interface gigabitethernet 0/1
ip address 192.168.10.1 255.255.255.0 
no shutdown

interface gigabitethernet 0/2
ip address 192.168.20.1 255.255.255.0
no shutdown 
```
---

### 2. 🧱 **Router-on-a-Stick (ROAS) Inter-VLAN Routing**

- Bir router üzerinde **her VLAN için sub-interface (alt arayüz)** oluşturulur.
- Her sub-interface'e ilgili VLAN'a ait IP verilir.
- Switch ile router arasında **trunk port** konfigürasyonu yapılır.

### 🛠 Inter-Vlan Routing **Switch** Yapılandırması

```
Switch>enable
Switch#configure terminal 
Switch(config)#hostname SW1
SW1(config)#vlan 10
SW1(config-vlan)#name IT
SW1(config-vlan)#exit
SW1(config)#vlan 20
SW1(config-vlan)#name HR
SW1(config-vlan)#
SW1(config-vlan)#exit 
SW1(config)#interface fastethernet 0/1
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 10 
SW1(config-if)#exit
SW1(config)#interface fastethernet 0/2
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 20
SW1(config-if)#interface gigabitethernet 0/1
SW1(config-if)#switchport mode trunk
SW1(config-if)#switchport nonegotiate

```

```
enable
configure terminal 
hostname SW1
vlan 10
name IT
exit
vlan 20
name HR
exit 
interface fastethernet 0/1
switchport mode access
switchport access vlan 10 
exit
interface fastethernet 0/2
switchport mode access
switchport access vlan 20
exit
interface gigabitethernet 0/1
switchport mode trunk
switchport nonegotiate
```
### 🛠 Inter-Vlan Routing **Router** Yapılandırması

```
Router>enable 
Router#configure terminal 
Router(config)#hostname R1 
R1(config)#interface gigabitethernet 0/1
R1(config-if)#no shutdown 
R1(config-if)#exit

R1(config)#interface gigabitethernet 0/1.10 
R1(config-subif)#encapsulation dot1Q 10 
R1(config-subif)#ip address 192.168.10.1 255.255.255.0 
R1(config-subif)#exit 

R1(config)#interface gigabitethernet 0/1.20 

R1(config-subif)#encapsulation dot1Q 20
R1(config-subif)#ip address 192.168.20.1 255.255.255.0 
R1(config-subif)#
```

```
enable 
configure terminal 
hostname R1 
interface gigabitethernet 0/1
no shutdown 
```

```
interface g0/1.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
```

```
interface g0/1.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
```
---

### 3. 🔁 **Layer 3 Switch ile Inter-VLAN Routing**

- L3 Switch, VLAN’lar arasında yönlendirme yapabilir.
- Her VLAN için bir **SVI (Switch Virtual Interface)** tanımlanır.
- `ip routing` komutu aktif edilerek yönlendirme yapılır.


### 🛠 Inter-Vlan Routing **MLSW** Yapılandırması

```
Switch>enable
Switch#configure terminal 
Switch(config)#hostname SW1
SW1(config)#vlan 10
SW1(config-vlan)#name IT
SW1(config-vlan)#exit
SW1(config)#vlan 20
SW1(config-vlan)#name HR
SW1(config-vlan)#exit 
SW1(config)#interface fastethernet 0/1
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 10 
SW1(config-if)#exit
SW1(config)#interface fastethernet 0/2
SW1(config-if)#switchport mode access
SW1(config-if)#switchport access vlan 20
SW1(config-if)#exit
SW1(config-if)#interface gigabitethernet 0/1      !Gigabit Ethernet ya da Fast Ethernet Portlarına dikkat edin! 
SW1(config-if)#switchport mode trunk
SW1(config-if)#switchport nonegotiate
```

```
enable
configure terminal 
hostname SW1
vlan 10
name IT
exit
vlan 20
name HR
exit 
interface fastethernet 0/1
switchport mode access
switchport access vlan 10 
exit
interface fastethernet 0/2
switchport mode access
switchport access vlan 20
exit
interface gigabitethernet 0/1    
switchport mode trunk
switchport nonegotiate
```
`ip routing`
`MLSW`

```
Switch>enable 
Switch#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#**hostname MLSW**
MLSW(config)#vlan 10
MLSW(config-vlan)#name IT
MLSW(config-vlan)#exit
MLSW(config)#vlan 20
MLSW(config-vlan)#name HR
MLSW(config-vlan)#exit
MLSW(config)#interface range gigabitethernet 1/0/1-2
MLSW(config-if-range)#switchport mode trunk 
MLSW(config-if-range)#switchport nonegotiate
MLSW(config-if-range)#exit
MLSW(config)#ip routing
MLSW(config)#interface vlan 10 
MLSW(config-if)#ip address 192.168.10.1 255.255.255.0
MLSW(config-if)#exit 
MLSW(config)#interface vlan 20
MLSW(config-if)#ip address 192.168.20.1 255.255.255.0
MLSW(config-if)#exit 
```

```
enable 
configure terminal 
**hostname MLSW**
vlan 10
name IT
exit
vlan 20
name HR
exit
interface range gigabitethernet 1/0/1-2
switchport mode trunk 
switchport nonegotiate
exit
ip routing
interface vlan 10 
ip address 192.168.10.1 255.255.255.0
exit 
interface vlan 20
ip address 192.168.20.1 255.255.255.0
exit 
```