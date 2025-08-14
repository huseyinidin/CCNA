---------------------------
1. PORT SECURITY
---------------------------

## FastEthernet0/1 Port Security Konfigürasyonu

```
interface FastEthernet0/1
 switchport mode access                  		# Portu access moduna alır (tek VLAN için)
 switchport access vlan 10               		# Portu VLAN 10’a atar
 switchport port-security                		# Port security özelliğini aktif eder
 switchport port-security maximum 2     		# Portta en fazla 2 MAC adresine izin verir
 switchport port-security mac-address sticky  		# Statik olarak öğrenilen MAC adreslerini kaydeder
 switchport port-security mac-address 0000.1111.2222  	# Belirli bir MAC adresine izin verir
 switchport port-security violation shutdown     	# İhlalde portu kapatır (varsayılan mod)

```
---

** Portu access moda al **
switchport mode access                # Portu access moduna geçir (Port Security sadece access portlarda çalışır)

** VLAN ataması yap **
switchport access vlan 10              # Portu VLAN 10'a atar

** Port Security özelliğini aktif et **
switchport port-security               # Port Security özelliğini aktif eder

** Maksimum cihaz sayısını belirle **
switchport port-security maximum 2     # Porttan en fazla 2 farklı MAC adresi geçebilir

** Sticky öğrenme yöntemi **
switchport port-security mac-address sticky    # Bağlanan cihazların MAC adreslerini öğrenip konfigürasyona yazar

** Manuel MAC adresi ekleme (opsiyonel) **
switchport port-security mac-address 0000.1111.2222   # Sadece bu MAC adresine izin verir

** Violation mode belirleme **
switchport port-security violation shutdown    # İhlalde portu kapatır (varsayılan mod)
```
---

```
Durumu görmek için
show port-security                            # Genel Port Security tablosunu gösterir
show port-security interface f0/1             # Belirli portun durumunu gösterir

Err-disabled olmuş portu yeniden aktif etme

interface fastEthernet0/1
shutdown                                     # Portu kapat
no shutdown                                  # Portu tekrar aç
```