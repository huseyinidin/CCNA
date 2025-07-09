# CCNA – Komut Modları Özeti

Cisco switch ve router'larda kullanılan temel komut modlarının kısa açıklamaları aşağıda verilmiştir.

| Mod İsmi                    | Simge             | Açıklama                                                                |
|-----------------------------|-------------------|-------------------------------------------------------------------------|
| **User EXEC Mode**          | `>`               | Temel izleme komutlarının çalıştığı giriş seviyesi modudur.             |
| **Privileged EXEC Mode**    | `#`               | Tüm sistem ve denetim komutlarına erişim sağlar.                        |
| **Global Config Mode**      | `(config)#`       | Cihaz genel ayarlarının yapıldığı moddur.                               |
| **Interface Config Mode**   | `(config-if)#`    | Belirli bir arayüz (port) yapılandırılır.                               |
| **Line Config Mode**        | `(config-line)#`  | Konsol, Telnet veya SSH hatları yapılandırılır.                         |
| **VLAN Config Mode**        | `(config-vlan)#`  | Switch'te VLAN'ların tanımlandığı ve isimlendirildiği moddur.           |
| **Router Config Mode**      | `(config-router)#`| Routing protokollerinin yapılandırıldığı moddur.                        |

## 💡 Ek Bilgi

- `enable` komutu → User mode'dan Privileged mode'a geçiş yapar.  
- `configure terminal` → Global config moduna geçiş sağlar.  
- `exit` → Bir üst moda döner.  
- `end` veya `CTRL+Z` → Direkt Privileged moda döner.

---

# 1. User EXEC Mode (Kullanıcı Yürütme Modu)

- **Giriş simgesi:** `>`

- **Örnek:** `Switch>` veya `Router>`

- **Erişim:** Cihaza ilk bağlandığınızda `Konsol`, `SSH`, `Telnet` komutları

- **Yapabilecekleriniz:** Temel izleme komutları `ping`, `traceroute`, `show`, `logout`

- **Kısıtlama:** Yapılandırma değişiklikleri yapılamaz.

- **Komuta geçiş:**

```
> enable
```

---

# 2. Privileged EXEC Mode (Yetkili Yürütme Modu)

- **Giriş simgesi:** `#`

- **Örnek:** Switch# veya Router#

- **Amaç:** Daha gelişmiş `show`, `debug`, `copy`, `reload`, `erase` komutları

- **Not:** Cihaz yapılandırmasına geçiş buradan yapılır.

- **Komuta geçiş:**
```
# configure terminal
```

---

# 3. Global Configuration Mode (Genel Yapılandırma Modu)

- **Giriş simgesi:** `(config)#`

- **Örnek:** `Switch(config)#` veya `Router(config)#`

- **Amaç:** Cihaz genel ayarlarını yapmak `hostname`, `password`, `routing`, `VLAN`, `interface` vs.

- **Komuta geçiş:**

```
interface FastEthernet0/1

line console 0

router ospf 1
```

---

# 4. Interface Configuration Mode

- **Giriş simgesi:** `(config-if)#`

- **Örnek:** Switch(config-if)#

- **Amaç:** Belirli bir arayüzü yapılandırmak (IP adresi, VLAN, shutdown/no shutdown vs.)

- **Komuta geçiş:**

```
(config)# interface FastEthernet0/1
```

----

# 5. Line Configuration Mode

- **Giriş simgesi:** `(config-line)#`

- **Örnek:** `Router(config-line)#`

- **Amaç:** `Konsol`, `Telnet`, `SSH` erişim hatlarını yapılandırmak

- **Komuta geçiş:**

```
(config)# line console 0

(config)# line vty 0 4
```

---

# 6. VLAN Configuration Mode (Sadece switch’lerde)

- **Giriş simgesi:** `(config-vlan)#`

- **Örnek:** `Switch(config-vlan)#`

- **Amaç:**: `VLAN ID`, `isim` tanımı

- **Komuta geçiş:**

```
(config)# vlan 10
```

---

# 7. Router Configuration Mode (Sadece router’larda veya L3 switch’lerde)

- **Giriş simgesi:** `(config-router)#`

- **Örnek:** `Router(config-router)#`

- **Amaç:** Routing protokollerini `OSPF`, `RIP`, `EIGRP` vs. yapılandırmak

- **Komuta geçiş:**

```
(config)# router ospf 1
```
---