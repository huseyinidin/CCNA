\# DHCP Snooping ve VLAN Konfigürasyonu



\## Switch Konfigürasyonları



```
vlan 10
name IT 

vlan 20 
name HR

vlan 30 
name ARGE

vlan 40 
name SERVER 

vlan 50 
name SALES
```



```
ip dhcp snooping vlan 10,20        # VLAN 10 ve VLAN 20 için DHCP snooping aktif edilir
ip dhcp snooping                  # DHCP snooping global olarak aktif edilir
```



```
spanning-tree mode pvst            # PVST+ (Per VLAN Spanning Tree) modu aktif edilir
spanning-tree extend system-id     # Switch ID genişletilir, VLAN bazlı STP ID kullanılır
```



\### VLAN 10 Portu



```
interface FastEthernet0/1
switchport access vlan 10        # Port VLAN 10'a atanır
ip dhcp snooping limit rate 10   # DHCP mesajları için maksimum hız 10 msg/sn
switchport mode access            # Port access moduna ayarlanır
```



\### VLAN 20 Portu



```
interface FastEthernet0/3
switchport access vlan 20        
ip dhcp snooping limit rate 10   

switchport mode access            
```



\### VLAN 30 Portu



```
interface FastEthernet0/3
switchport access vlan 30        
ip dhcp snooping limit rate 10   
switchport mode access            
```



\### VLAN 50 Portu



```
interface FastEthernet0/22
switchport access vlan 50          
switchport mode access            
```

\### VLAN 40 Portu - \*\*Trusted DHCP\*\*



```
interface FastEthernet0/24
switchport access vlan 40
ip dhcp snooping trust           # Bu porttan gelen DHCP mesajları güvenilir kabul edilir
switchport mode access

```



\### GigabitEthernet Trunk Portu



``` 
interface GigabitEthernet0/1
ip dhcp snooping trust           # Trunk portta DHCP mesajları güvenilir kabul edilir
switchport mode trunk             # Trunk modu aktif edilir
switchport nonegotiate            # DTP (Dynamic Trunking Protocol) kapatılır

```

---



\## Router - ROAS Konfigürasyonu 



```

interface GigabitEthernet0/0

&nbsp;no ip address

&nbsp;duplex auto

&nbsp;speed auto

```



\### Router Subinterface Konfigürasyonları



```

interface GigabitEthernet0/0.10      		# Router üzerinde VLAN 10 için oluşturulan subinterface

&nbsp;encapsulation dot1Q 10             		# 802.1Q trunk tag ile VLAN 10 trafiğini tanımlar

&nbsp;ip address 192.168.10.1 255.255.255.0  	# Subinterface'e IP adresi atanır (gateway olarak kullanılacak)

&nbsp;ip helper-address 192.168.40.10   		# DHCP taleplerini 192.168.40.10 IP adresine yönlendirir (DHCP relay)

```



```

interface GigabitEthernet0/0.20

&nbsp;encapsulation dot1Q 20

&nbsp;ip address 192.168.20.1 255.255.255.0

&nbsp;ip helper-address 192.168.40.10

```



```

interface GigabitEthernet0/0.30

&nbsp;encapsulation dot1Q 30

&nbsp;ip address 192.168.30.1 255.255.255.0

&nbsp;ip helper-address 192.168.40.10

```



```

interface GigabitEthernet0/0.40

&nbsp;encapsulation dot1Q 40

&nbsp;ip address 192.168.40.1 255.255.255.0

&nbsp;ip helper-address 192.168.40.10

```



```

interface GigabitEthernet0/0.50

&nbsp;encapsulation dot1Q 50

&nbsp;ip address 192.168.50.1 255.255.255.0

&nbsp;ip helper-address 192.168.40.10

```

---

