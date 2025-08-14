# 🌐 DHCP Snooping

**DHCP Snooping**, bir switch üzerinde **sadece güvenilir portlardan DHCP mesajlarına izin veren güvenlik mekanizmasıdır**.
Amaç: **Sahte DHCP sunucularının ağa IP dağıtmasını engellemek.**

---

## ⚡ 1. Tanım

**DHCP Snooping**, switch’in DHCP paketlerini **güvenilir (trusted) ve güvenilmeyen (untrusted) portlar** olarak ayırmasını sağlar.

- **Trusted Port:** Gerçek DHCP sunucusunun bağlı olduğu port
- **Untrusted Port:** Client portları veya şüpheli portlar

---

## 🎯 2. Amaç

* **Sahte DHCP sunucularını engellemek**
* IP çakışmalarını ve **MITM saldırılarını önlemek**
* Ağ güvenliğini **artırmak**

---

## 🔧 3. Çalışma Mantığı

1. DHCP Snooping aktif edilir ve VLAN bazında çalıştırılır.
2. Portlar **trusted/untrusted** olarak belirlenir.
3. Client’lar sadece **trusted DHCP sunucularından** IP alabilir.
4. Switch **binding table** oluşturur: MAC–IP–VLAN eşleşmelerini kaydeder.
5. DAI ve diğer güvenlik mekanizmaları bu tabloyu kullanabilir.

---

## 🧠 4. Avantajları

* DHCP tabanlı **saldırılara karşı koruma sağlar**
* Ağda **IP bütünlüğünü** garanti eder
* **Binding table**, ARP Inspection ve IP Source Guard gibi özellikler için temel oluşturur

---

## 🌟 5. Kullanım Alanları

* Kurumsal ağlarda **LAN güvenliği**
* Misafir ağlarda **IP kontrolü**
* Şubelerde **DHCP güvenliği**

---

