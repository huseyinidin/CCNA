# 🛡️ BPDU Guard Nedir?

**BPDU Guard**, bir porttan **BPDU (Bridge Protocol Data Unit)** mesajı gelirse, bu portu **hatalı (err-disabled)** duruma alır.  
Genellikle **PortFast** yapılandırılmış erişim portlarında kullanılır.

---

## 🎯 **Amacı**
- Son kullanıcı portlarına (örneğin PC, printer vb.) **switch** takılmasını önlemek.
- STP topolojisinin kazara veya kötü niyetli olarak bozulmasını engellemek.
- **Loop oluşumunu ve sahte root bridge saldırılarını engellemek.**

---

## ⚙️ **Komut ile Yapılandırma**

### 🔹 **Arayüz bazlı yapılandırma:**
```
Switch(config)# interface fastethernet 0/1
Switch(config-if)# spanning-tree portfast
Switch(config-if)# spanning-tree bpduguard enable
```

```
interface fastethernet 0/3
spanning-tree portfast
spanning-tree bpduguard enable
```
---

### 🔹 **Global Yapılandırma (Tüm Erişim Portları İçin Otomatik Etkinleştirme)**

Aşağıdaki komutlar sayesinde tüm erişim (access) portlarında **PortFast** ve **BPDU Guard** otomatik olarak etkinleştirilir:

```
Switch(config)# spanning-tree portfast default
Switch(config)# spanning-tree bpduguard default
```
```
spanning-tree portfast default
spanning-tree bpduguard default
```
---

## 🚨 BPDU Guard Nasıl Çalışır?

BPDU Guard etkinleştirilmiş bir port üzerinden **BPDU (Bridge Protocol Data Unit)** mesajı algılanırsa, **aşağıdaki güvenlik mekanizması** devreye girer:

---

### 🔒 Ne Olur?

- 🔴 Port, **err-disabled (hatalı)** duruma geçer  
- 🚫 **Trafik taşıyamaz**, ağ erişimi kesilir  
- 🛡️ **Ağ döngüsü (loop)** oluşumu ve  
  🎭 **Sahte switch/root bridge saldırıları** engellenir  
- ⚙️ Port manuel veya otomatik olarak yeniden etkinleştirilene kadar **pasif kalır**

---

### 🧠 Neden Önemlidir?

- **Son kullanıcı portlarına switch bağlanmasını önler**
- **STP topolojisinin bozulmasını engeller**
- Ağ güvenliği ve kararlılığı açısından kritik bir savunma katmanıdır
- 💡 **Tavsiyem:** BPDU Guard, `spanning-tree portfast` ile birlikte **özellikle son kullanıcı portlarında mutlaka etkinleştirilmelidir.**

---

## 🔄 Portu Tekrar Aktif Etme (Manuel Yöntem)

BPDU Guard nedeniyle **err-disabled (hatalı)** duruma geçen bir port, elle yeniden aktif hale getirilebilir.


### 🛠️ Komutlar:

```
Switch(config)# interface fastethernet 0/1
Switch(config-if)# shutdown
Switch(config-if)# no shutdown
