# CCNA – Cisco Switch – Line Console 0 Temel Yapılandırma Komutları


Cisco switch'lerde konsol erişimini yapılandırmak için kullanılan `line console 0` komutlarının kısa bir özetini içerir.

---

## 🎯 Amaç

`line console 0` yapılandırması ile:
- Konsol bağlantısına parola koyulur
- Giriş yapılması için `login` komutu etkinleştirilir
- Oturum süresi ve özellikleri belirlenir

---

## ⚙️ Temel Yapılandırma Komutları

```
Switch> enable
Switch# configure terminal
Switch(config)# line console 0
Switch(config-line)# password cisco
Switch(config-line)# login
Switch(config-line)# exit
```
### NOT: 

- Bulunduğunuz mod içerisinde kullanılan komutları yapıştırarak farklı cihazlar arasında hızlı işlemler yapabilirsin.

```
enable
configure terminal
line console 0
password cisco
login
exit
```