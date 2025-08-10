# FHRP Concepts (First Hop Redundancy Protocols)

## Ağ Laboratuvarı Çalışması

Bu laboratuvar çalışmasında, bir kurumsal ağ yapısını simüle edecek şekilde birden fazla konfigürasyon tek bir topoloji üzerinde bir araya getirilmiştir. Çalışma kapsamında;

- **VLAN** yapılandırmaları ile ağ segmentasyonu yapılarak trafiğin düzenli ve güvenli bir şekilde yönetilmesi sağlandı.  
- **STP (Spanning Tree Protocol)** ile yedekli bağlantılarda oluşabilecek döngüler önlendi.  
- **EtherChannel** kullanılarak bağlantı kapasitesi artırıldı ve hat yedekliliği sağlandı.  
- **DHCP Sunucu** üzerinde her VLAN için ayrı **scope**’lar oluşturuldu, böylece istemcilerin IP adresleri ve ek ağ bilgileri otomatik olarak dağıtıldı.  
- **Interface VLAN**’larda **Relay Agent** yapılandırılarak, farklı VLAN’lardaki istemcilerin IP adreslerini merkezi DHCP sunucudan alması sağlandı.  
- **ROAS (Router-on-a-Stick)** konfigürasyonu ile farklı VLAN’lar arasında yönlendirme yapıldı.  
- **Layer 3 Switch** üzerinde **routing** aktif edilerek **interface VLAN**’lar oluşturuldu ve ağlar arası iletişim sağlandı.  
- VLAN’lar arası **trunk bağlantıları** yapılandırıldı.  
- Son kullanıcı portları **access mode** olarak atanarak ilgili VLAN’lara bağlandı.  
- **FHRP (First Hop Redundancy Protocol)** konfigürasyonu ile **Router0** ve **Router1** arasında aktif/standby yapısı kurularak, ağın ilk geçiş noktasında yüksek erişilebilirlik sağlandı.  

Bu çalışma, farklı ağ teknolojilerini entegre ederek gerçekçi ve ölçeklenebilir bir topoloji oluşturmayı hedeflemektedir.

### 2911 Router0 Yapılandırma Komutları

```
interface gigabitEthernet 0/1.10 
  encapsulation dot1Q 10
  ip address 192.168.10.2 255.255.255.0
  standby 10 ip 192.168.10.1
  standby 10 priority 110
  standby 10 preempt
```
```
interface gigabitEthernet 0/1.20 
  encapsulation dot1Q 30
  ip address 192.168.20.2 255.255.255.0
  standby 20 ip 192.168.20.1
  standby 20 priority 110
  standby 20 preempt

```
```
interface gigabitEthernet 0/1.30
  encapsulation dot1Q 30
  ip address 192.168.30.2 255.255.255.0
  standby 30 ip 192.168.30.1
  standby 30 priority 110
  standby 30 preempt
```
---

### 2911 Router1 Yapılandırma Komutları 

```
interface gigabitEthernet 0/2.10
  ip address 192.168.10.3 255.255.255.0
  encapsulation dot1Q 10
  standby 10 ip 192.168.10.1
  standby 10 priority 100
  standby 10 preempt
```
```
interface gigabitEthernet 0/2.20 
  encapsulation dot1Q 20
  ip address 192.168.20.3 255.255.255.0
  standby 20 ip 192.168.20.1
  standby 20 priority 100
  standby 20 preempt

```
```
interface gigabitEthernet 0/2.30 
  encapsulation dot1Q 30
  ip address 192.168.30.3 255.255.255.0
  standby 30 ip 192.168.30.1
  standby 30 priority 100
  standby 30 preempt
```
---

### 3650 Layer 3 Switch Yapılandırma Komutları 

```
spanning-tree mode pvst
spanning-tree vlan 1,20 priority 24576
spanning-tree vlan 10,30 priority 28672
```
```
interface Port-channel1
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface Port-channel3
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface GigabitEthernet1/0/1
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface GigabitEthernet1/0/2
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface GigabitEthernet1/0/3
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
 channel-group 1 mode active
```
```
interface GigabitEthernet1/0/4
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
 channel-group 3 mode active
```
```
interface GigabitEthernet1/0/5
 switchport access vlan 40
 switchport mode access
```
```
interface Vlan10
 mac-address 00d0.58a1.4101
 ip address 192.168.10.5 255.255.255.0
 ip helper-address 192.168.40.10
```
```
interface Vlan20
 mac-address 00d0.58a1.4102
 ip address 192.168.20.5 255.255.255.0
 ip helper-address 192.168.40.10
```
```
interface Vlan30
 mac-address 00d0.58a1.4103
 ip address 192.168.30.5 255.255.255.0
 ip helper-address 192.168.40.10
```
```
interface Vlan40
 mac-address 00d0.58a1.4104
 ip address 192.168.40.5 255.255.255.0
```
---

### 2960 Layer 2 Switch1 Yapılandırma komutları  

```
spanning-tree mode pvst
spanning-tree extend system-id
spanning-tree vlan 10,30 priority 24576
spanning-tree vlan 20 priority 28672
```
```
interface Port-channel1
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface Port-channel2
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
```
```
interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
```
```
interface FastEthernet0/3
 switchport access vlan 30
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
```
```
interface FastEthernet0/23
 switchport trunk allowed vlan 1,10,20,30
 switchport trunk allowed vlan 30
 switchport mode trunk
 switchport nonegotiate
 channel-group 2 mode active
```
```
interface FastEthernet0/24
 switchport trunk allowed vlan 1,10,20,30
 switchport trunk allowed vlan 30
 switchport mode trunk
 switchport nonegotiate
 channel-group 2 mode active
```
```
interface GigabitEthernet0/1
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
 channel-group 1 mode active
```
---

### 2960 Layer 2 Switch2 Yapılandırma komutları 

```
spanning-tree mode pvst
spanning-tree extend system-id
spanning-tree vlan 10,30 priority 20480
spanning-tree vlan 1,20 priority 28672
```
```
interface Port-channel2
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface Port-channel3
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
```
```
interface FastEthernet0/1
 switchport access vlan 10
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
```
```
interface FastEthernet0/2
 switchport access vlan 20
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
```
```
interface FastEthernet0/3
 switchport access vlan 30
 switchport mode access
 spanning-tree portfast
 spanning-tree bpduguard enable
```
```
interface FastEthernet0/23
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
 channel-group 2 mode active
```
```
interface FastEthernet0/24
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
 channel-group 2 mode active
```
```
interface GigabitEthernet0/2
 switchport trunk allowed vlan 1,10,20,30
 switchport mode trunk
 switchport nonegotiate
 channel-group 3 mode active
```
---

