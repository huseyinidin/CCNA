# Cisco Cihazlarda `line vty` Yapılandırması

## 📌 Nedir?

`line vty` (Virtual Teletype Line), Cisco router ve switch’lerde **uzaktan erişim (Telnet/SSH)** bağlantıları için kullanılan sanal hatlardır. Her bir `vty` hattı, eş zamanlı uzaktan bağlantı oturumlarını temsil eder.

---

## 🎯 Ne İşe Yarar?

* Telnet veya SSH ile Cisco cihaza **uzaktan bağlantı** yapılmasını sağlar.
* Şifre koruması, kimlik doğrulama ve zaman aşımı gibi güvenlik ayarları yapılabilir.

---

## 🔢 `line vty 0 4` ve `line vty 0 15` Ne Anlama Gelir?

### ✅ `line vty 0 4` → **5 adet** sanal oturum (0,1,2,3,4)

* Cisco cihazlarda **varsayılan olarak 5 vty hattı** tanımlıdır.
* Bu da aynı anda en fazla 5 kişinin uzaktan (Telnet/SSH) bağlanabileceği anlamına gelir.

### ✅ `line vty 0 15` → **16 adet** sanal oturum (0–15)

* Bazı cihazlarda (özellikle Layer 3 switch’ler, router’lar) **16 hatta kadar** destek vardır.
* Daha fazla eş zamanlı kullanıcıya izin verilmesi isteniyorsa bu aralık kullanılır.

---

## 🛠 Temel Yapılandırma Komutları


```
Switch> enable
Switch# configure terminal
Switch(config)# line vty 0 4
Switch(config-line)# password cisco
Switch(config-line)# login
Switch(config-line)# exit
```

```
configure terminal
line vty 0 4
password cisco
login
exit
```

**Açıklama:**

- `password` cisco → Girişte parola ister.

- `login` → Parola doğrulamasını etkinleştirir.

- Bu yapılandırma hem Telnet hem SSH için ortak kullanılabilir (transport ayarı yapılmazsa).

- `transport input telnet` → Yalnızca `Telnet` bağlantılarına izin verir.

- `transport input ssh` → Yalnızca `SSH` bağlantılarına izin verir.

---

## 🔐 Gelişmiş Kimlik Doğrulama `(Login Local)`

### SSH için line vty 0 4 Yapılandırması

```
Switch> enable
Switch# configure terminal
Switch(config)# line vty 0 4
Switch(config-line)# login local
Switch(config-line)# transport input ssh

Switch(config)# hostname SW1
SW1(config)# ip domain-name ccna.local
SW1(config)# username admin privilege 15 secret cisco
SW1(config)# crypto key generate rsa
SW1(config)# ip ssh version 2

```

```
enable
configure terminal
line vty 0 4
login local
transport input ssh

hostname SW1
ip domain-name ccna.local
username admin privilege 15 secret cisco
crypto key generate rsa
ip ssh version 2

```

---

Switch’e uzaktan (SSH/Telnet) erişim sağlamak için, VLAN arayüzü olarak kullanılan Switch Virtual Interface (SVI)’ye IP adresi atanması gerekir. Bu IP, yönetim için kullanılan sanal bir ağ arayüzüdür.

```
Switch(config)# interface vlan 1
Switch(config-if)# ip address 192.168.1.1 255.255.255.0
Switch(config-if)# no shutdown
Switch(config-if)# exit
```

```
interface vlan 1
ip address 192.168.1.1 255.255.255.0
no shutdown
exit
```