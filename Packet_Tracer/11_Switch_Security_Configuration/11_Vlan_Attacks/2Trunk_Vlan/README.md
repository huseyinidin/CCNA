---

## 2️⃣ Trunk Portlarını Sıkılaştırma ve DTP Devre Dışı Bırakma

Trunk bağlantılarını sadece gerekli cihazlar arasında yapılandırın ve DTP’yi devre dışı bırakın.

```
 interface fa0/1
  switchport mode trunk
  switchport nonegotiate
  switchport trunk allowed vlan 10,20,30
```

⚠️ **Uyarı: Tüm portların trunk olmasına gerek yoktur, sadece switch-switch veya switch-router bağlantılarında kullanın.**

---
