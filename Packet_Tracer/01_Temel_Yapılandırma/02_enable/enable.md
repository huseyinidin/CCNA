# CCNA – Cisco Switch – Enable Temel Yapılandırma Komutları

## 🎯 Amaç
Cisco `switch` ve `router`'larda `enable` komutu, kullanıcıyı **Privileged EXEC Mode**'a (yetkili yönetici modu) geçirir. Bu modda cihaz üzerinde yapılandırma değişiklikleri yapılabilir. **Bu yüzden güvenliğin sağlanması gerekir.**

---

## 🔐 Neden `enable` Şifresi Verilir?

- **Yetkisiz kişilerin** cihaz yapılandırmasını değiştirmesini engellemek için
- Kullanıcıların sadece sınırlı komutlarla çalışmasını sağlamak için
- Özellikle Telnet/SSH bağlantılarında ek güvenlik katmanı oluşturmak için

---

🔐 Ekstra: Şifreyi Gizli Tutmak İçin

enable secret, enable password’dan daha güvenlidir, çünkü şifreyi şifreli olarak saklar.

Aynı anda ikisi tanımlanırsa, enable secret geçerli olur.


| Komut             | Güvenlik Seviyesi | Özellik                                    |
| ----------------- | ----------------- | ------------------------------------------ |
| `enable password` | Düşük             | Şifre açık şekilde konfigürasyonda görünür |
| `enable secret`   | Yüksek            | Şifrelenmiş, daha güvenli                  |

---

## ⚙️ Örnek Yapılandırma

```
Switch> enable
Switch# configure terminal
Switch(config)# enable password cisco
Switch(config)# enable secret ciscogizli
Switch(config)# exit
```

```
enable
configure terminal
enable password cisco
enable secret ciscogizli
exit
```

---