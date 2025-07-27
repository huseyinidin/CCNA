# VLAN, Per-VLAN(PVST+), EtherChannel ve ROAS Konfigürasyon Komutları

## SW1

### 🔧 SW1 Data Vlan Yapılandırması

** Bütün Switch'lere aynı data vlanlar girilir! ** 

```
vlan 10
name IT 
vlan 20
name HR
vlan 30 
name ARGE
vlan 40 
name MNGM 
```

### 🔧 SW1 Son Kullanıcı Cihazların Yapılandırması

```
interface fastEthernet 0/1
switchport mode access 
switchport access vlan 10 
---
interface fastEthernet 0/2
switchport mode access 
switchport access vlan 20 
---
interface fastEthernet 0/3
switchport mode access 
switchport access vlan 30 
---
interface fastEthernet 0/4
switchport mode access 
switchport access vlan 40 
```

### 🔧 Son Cihaz Interface Range Yapılandırması

**NOT: Ortak yapılabilen konfigürasyonları tek tek portların içine girmek yerine, range komutunu kullanarak tek seferde yapabilirsin.**

```
interface range fastEthernet 0/1-4 
switchport mode access
spanning-tree portfast
spanning-tree bpduguard enable
```

## 🔧 EtherChannel Interface Range Yapılandırması

**🔹 Fiziksel Arayüzlere Yazılması Gerekenler: ** 

### SW1 
```
interface range fastEthernet 0/21-22
switchport mode trunk
switchport nonegotiate
**channel-group 2 mode active**
```

```
interface range fastEthernet 0/23-24
switchport mode trunk
switchport nonegotiate
**channel-group 1 mode active**

```

### SW2 
```
interface range fastEthernet 0/21-22
switchport mode trunk
switchport nonegotiate
**channel-group 3 mode active**
```

```
interface range fastEthernet 0/23-24
switchport mode trunk
switchport nonegotiate
**channel-group 1 mode active*

```

### SW3 
```
interface range fastEthernet 0/21-22
switchport mode trunk
switchport nonegotiate
**channel-group 3 mode active**
```

```
interface range fastEthernet 0/23-24
switchport mode trunk
switchport nonegotiate
**channel-group 2 mode active**

```
---

## 🔧 Port-Channel Arayüz Yapılandırması


**🔹 Port-Channel Arayüzüne Yazılması Gerekenler: **

** Her Switch için verdiğin port-channel grubuna girerek yazılması gereken komutlar!**
```
interface Port-channel 2
switchport mode trunk 
switchport nonegotiate
```

```
interface Port-channel 1
switchport mode trunk 
switchport nonegotiate

```
---

## 🔧 PVST+ Yapılandırması 

### 🔧 SW2 Yapılandırması 

```
spanning-tree vlan 10 root secondary
spanning-tree vlan 20 root primary
spanning-tree vlan 30 root secondary
spanning-tree vlan 40 root primary
```

### 🔧 SW3 Yapılandırması 

```
spanning-tree vlan 1 root primary
spanning-tree vlan 10 root primary
spanning-tree vlan 30 root primary
```
---

## 🔧 ROAS Yapılandırması 

```
interface GigabitEthernet0/0
no shutdown

interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 192.168.30.1 255.255.255.0
 no shutdown

interface GigabitEthernet0/0.40
 encapsulation dot1Q 40
 ip address 192.168.40.1 255.255.255.0
 no shutdown
```
