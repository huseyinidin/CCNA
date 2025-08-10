# FHRP Concepts (First Hop Redundancy Protocols)

## Ağ Laboratuvarı Çalışması

Bu laboratuvar çalışmasında, bir kurumsal ağ yapısını simüle edecek şekilde birden fazla konfigürasyon tek bir topoloji üzerinde bir araya getirilmiştir. Çalışma kapsamında;

- **VLAN** yapılandırmaları ile ağ segmentasyonu sağlandı.  
- **STP (Spanning Tree Protocol)** kullanılarak yedekli bağlantılarda döngülerin önüne geçildi.  
- **EtherChannel** konfigürasyonu ile bağlantı kapasitesi artırıldı.  
- **IPv6 SLAAC** ve **DHCPv6** yöntemleriyle istemcilere otomatik IPv6 adres dağıtımı yapıldı.  
- **ROAS (Router-on-a-Stick)** kullanılarak VLAN’lar arası yönlendirme gerçekleştirildi.  
- **IPv6 Routing** komutları ile ağlar arası iletişim sağlandı.  
- VLAN’lar arası **trunk bağlantıları** yapılandırıldı.  
- Son kullanıcı portları **access mode** olarak atanıp ilgili VLAN’lara bağlandı.  
- **FHRP (First Hop Redundancy Protocol)** konfigürasyonu yapılarak **Router0** ve **Router1** arasında aktif/standby mantığında geçiş desteği sağlandı, böylece ağda ilk yönlendirici seviyesinde yüksek erişilebilirlik garanti altına alındı.  

Bu çalışma, farklı ağ teknolojilerini entegre ederek gerçekçi ve ölçeklenebilir bir topoloji oluşturmayı hedeflemektedir.


### 2911 Router0 Yapılandırma Komutları

```
ipv6 unicast-routing
```
```
ipv6 dhcp pool DNS
 dns-server 2001:DB8:8000:40::2
 domain-name domain.local 
```
```
interface GigabitEthernet0/1.10
 encapsulation dot1Q 10
 no ip address
 ipv6 address 2001:DB8:8000:20::2/64
 ipv6 nd other-config-flag
 ipv6 enable
 ipv6 dhcp server DNS
 standby version 2
 standby 10 ipv6 autoconfig 
 standby 10 priority 110
 standby 10 preempt
```
```
interface GigabitEthernet0/1.20
 encapsulation dot1Q 20
 no ip address
 ipv6 address 2001:DB8:8000:20::2/64
 ipv6 nd other-config-flag
 ipv6 enable
 ipv6 dhcp server DNS
 standby version 2
 standby 20 ipv6 autoconfig 
 standby 20 priority 110
 standby 20 preempt
```
``` 
interface GigabitEthernet0/1.30
 encapsulation dot1Q 30
 no ip address
 ipv6 address 2001:DB8:8000:30::2/64
 ipv6 nd other-config-flag
 ipv6 enable
 ipv6 dhcp server dns1
 standby version 2
 standby 30 ipv6 autoconfig 
 standby 30 priority 110
 standby 30 preempt
```
---

### 2911 Router1 Yapılandırma Komutları 

```
ipv6 unicast-routing
```
```
ipv6 dhcp pool DNS
 dns-server 2001:DB8:8000:40::2
 domain-name domain.local 
```
```
interface GigabitEthernet0/2.10
 encapsulation dot1Q 10
 no ip address
 ipv6 address 2001:DB8:8000:10::3/64
 ipv6 enable
 ipv6 dhcp server DNS
 standby version 2
 standby 10 ipv6 autoconfig 
 standby 20 priority 100 
 standby 10 preempt
```
```
interface GigabitEthernet0/2.20
 encapsulation dot1Q 20
 no ip address
 ipv6 address 2001:DB8:8000:20::3/64
 ipv6 enable
 ipv6 dhcp server DNS
 standby version 2
 standby 20 ipv6 autoconfig
 standby 20 priority 100 
 standby 20 preempt
```
```
interface GigabitEthernet0/2.30
 encapsulation dot1Q 30
 no ip address
 ipv6 address 2001:DB8:8000:30::3/64
 ipv6 enable
 ipv6 dhcp server DNS
 standby version 2
 standby 30 ipv6 autoconfig 
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

