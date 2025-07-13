# 🌐 Spanning-Tree Mode’ları

Cisco switch’lerde STP’nin **3 temel modu** bulunur.  
Her biri ağın ölçeğine, VLAN yapısına ve hız gereksinimine göre tercih edilir.

## 🟢 PVST+ (Per VLAN Spanning Tree Plus)

### 🔍 **Açılımı**

- **IEEE 802.1D** standardını temel alır.
- Her VLAN için ayrı bir STP instance (örneği) çalıştırır.


### ⚡ **Avantajları**

- VLAN bazlı yük dengeleme (load balancing) yapılabilir.
- Böylece farklı VLAN’lar farklı root switch’ler üzerinden trafik akışı sağlar.

### ⚙️ **Kullanım Komutu**

```
Switch(config)# spanning-tree mode pvst
```
---

## 🔵 Rapid PVST+ (Rapid Per VLAN Spanning Tree Plus)

---

### 🔍 **Açılımı**

- **PVST+**’nin hızlı sürümüdür.  
- **IEEE 802.1w (RSTP)** standardına dayanır.  
- Her VLAN için ayrı bir STP instance çalıştırır (tıpkı PVST+ gibi).

### ⚡ **Avantajları**

- **Çok hızlı port durum değişimi**:  
  `blocking → forwarding` gibi geçişler milisaniyeler içinde gerçekleşir.
- **Loop önleme daha hızlıdır**, ağın toparlanma süresi kısalır.
- STP convergence süresi saniyeler değil, **milisaniyelerdedir**.


### ⚙️ **Kullanım Komutu**

```
Switch(config)# spanning-tree mode rapid-pvst
```

---

## 🟣 MST (Multiple Spanning Tree)


### 🔍 **Açılımı**

- **MST (Multiple Spanning Tree)**, birden fazla VLAN’ı tek bir **STP instance** içinde gruplayarak yönetir.  
- **IEEE 802.1s** standardına dayanır.


### ⚡ **Avantajları**

- Aynı davranışı gösterecek VLAN’lar **tek bir instance** altında gruplanır.  
- **Büyük ağlarda CPU ve bellek kullanımı ciddi ölçüde azalır**.  
- **Topoloji değişimlerinin** sadece ilgili instance’ı etkilemesi sağlanır.  


### ⚙️ **Kullanım Komutu**

```
Switch(config)# spanning-tree mode mst
```
