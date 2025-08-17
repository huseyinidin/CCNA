---

## 1️⃣ Gereksiz Trunk Portlarını Kapatın

```
 vlan 10 
 name IT 

 interface range fa0/1 - 3
  switchport mode access
  switcport access vlan 10

 interface range fa0/4 - 24
  shutdown
  switchport mode access
  switchport access vlan 999
```

💡 **İpucu: VLAN 999 gibi kullanılmayan bir VLAN oluşturmak, saldırganın bu portları kullanarak ağınıza sızmasını zorlaştırır.**

---