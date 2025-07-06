# Cisco Switch Port Güvenliği (Port Security) Yapılandırması

## 🔐 Nedir

Port Security, Cisco switch’lerde belirli bir porta hangi MAC adreslerinin bağlanabileceğini kontrol altına alarak, yetkisiz cihazların ağa bağlanmasını engelleyen bir güvenlik özelliğidir.

---

## 🎯 Ne Amaçla Kullanılır

- Ağda yalnızca yetkili cihazların çalışmasını sağlamak
- MAC adresi taklit **(spoofing)** saldırılarını önlemek
- Fiziksel ağ bağlantılarını denetlemek

---

## 🛠 Temel Yapılandırma Adımları

### 1️⃣ Switch portunu erişim moduna al
```
SW1(config)# interface FastEthernet0/1
SW1(config-if)# switchport mode access
```

### 2️⃣ Port güvenliğini aktif et
```
SW1(config-if)# switchport port-security
```


### 3️⃣ İzin verilecek maksimum cihaz sayısını sınırla
```
SW1(config-if)# switchport port-security maximum 1
```


### 4️⃣ Güvenilir MAC adresi belirle (statik)
```
SW1(config-if)# switchport port-security mac-address 0011.2233.4455

🔄 Alternatif: MAC adresi otomatik öğrenilsin

SW1(config-if)# switchport port-security mac-address sticky
```

### 5️⃣ Kural ihlali durumunda alınacak aksiyonu belirle
```
SW1(config-if)# switchport port-security violation shutdown
```

Diğer seçenekler:

`protect:` Yalnızca yasaklı adresi engeller, log tutmaz

`restrict:` Yasaklı adresi engeller ve log kaydı oluşturur

`shutdown:` Portu kapatır (en katı seçenek, varsayılan)

---

## ⚙️ Örnek Yapılandırma

```
SW1(config)# interface FastEthernet0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport port-security
SW1(config-if)# switchport port-security maximum 1
SW1(config-if)# switchport port-security mac-address sticky
SW1(config-if)# switchport port-security violation shutdown

```

```
interface FastEthernet0/1
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
```

---

## 🔍 Son Adım: Kontrol Et

```
Switch# show port-security address
```

```
Switch# show port-security interface fastEthernet0/1
```

---

## 💡 Ekstra İpucu: Sticky MAC kullanıyorsan…

Sticky MAC adresini silmeden portu shutdown / no shutdown yaparsan, port açılır ama aynı cihazın bağlanması gerekir.

```
SW1# configure terminal
SW1(config)# interface fastEthernet0/1
SW1(config-if)# shutdown
SW1(config-if)# no shutdown
```

Eğer farklı bir cihaz takacaksan MAC adresini önce sil:

```
SW1(config)# interface f0/1
SW1(config-if)# no switchport port-security mac-address sticky 0001.64A7.7A6B
```
