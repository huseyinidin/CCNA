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

- **Erişim:** Cihaza ilk bağlandığınızda (`Konsol`, `SSH```, `Telnet`)

- **Yapabilecekleriniz:** Temel izleme komutları (`ping`, `traceroute`, `show`, `logout`)

- **Kısıtlama:** Yapılandırma değişiklikleri yapılamaz.

- **Komuta geçiş:**

```
bash

enable
```
---