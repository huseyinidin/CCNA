# 🌐 EtherChannel Nedir? | CCNA Seviyesi Açıklama

## 📌 Tanım

**EtherChannel**, birden fazla fiziksel Ethernet bağlantısını bir araya getirerek tek bir mantıksal bağlantı (logical link) gibi çalışmasını sağlayan bir teknolojidir. Bu sayede bağlantı hızı artar, yedeklilik (redundancy) sağlanır ve STP (Spanning Tree Protocol) gereksiz portları kapatmaz.

---

## 🎯 EtherChannel’in Amaçları

- 🔄 **Yedeklilik (Redundancy):** Fiziksel linklerden biri koparsa trafik diğerlerinden devam eder.
- 🚀 **Bant Genişliği Artışı:** Örneğin, 4x1 Gbps bağlantı = 4 Gbps efektif bant genişliği sağlar.
- 🧠 **STP Optimizasyonu:** STP tüm linkleri kapatmaz, çünkü EtherChannel tek bir port gibi görünür.
- ⚙️ **Yönetim Kolaylığı:** Çoklu fiziksel bağlantı yerine tek bir mantıksal yapı yönetilir.

---

## ⚙️ EtherChannel Türleri

| Tür | Açıklama |
|-----|----------|
| **PAgP (Cisco’a özel)** | Cisco'ya ait protokol. `auto` ve `desirable` modları vardır. |
| **LACP (802.3ad)** | Standart protokol. `active` ve `passive` modları vardır. |
| **Static (Manual)** | Hiçbir protokol kullanılmaz, elle konfigüre edilir. |

---

## 🔧 Temel Konfigürasyon Örneği (LACP)


SW3(config)# interface range e0/0 - 2
SW3(config-if-range)# switchport trunk encapsulation dot1q
SW3(config-if-range)# switchport mode trunk
SW3(config-if-range)# channel-group 1 mode active

SW3(config)# interface port-channel 1
SW3(config-if-range)# switchport trunk encapsulation dot1q
SW3(config-if)# switchport mode trunk


interface range e0/0 - 2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 1 mode active

interface Port-channel 1
 switchport trunk encapsulation dot1q
 switchport mode trunk

```


```
SW1(config)# interface range e0/0 - 2
SW1(config-if-range)# switchport trunk encapsulation dot1q
SW1(config-if-range)# switchport mode trunk
SW1(config-if-range)# channel-group 1 mode active

SW1(config)# interface port-channel 1
SW1(config-if-range)# switchport trunk encapsulation dot1q
SW1(config-if)# switchport mode trunk


interface range e0/0 - 2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 1 mode active

interface Port-channel 1
 switchport trunk encapsulation dot1q
 switchport mode trunk

```
---

```
SW1(config)# interface range e2/1 - 3
SW1(config-if-range)# switchport trunk encapsulation dot1q
SW1(config-if-range)# switchport mode trunk
SW1(config-if-range)# channel-group 2 mode active

SW1(config)# interface port-channel 2
SW1(config-if-range)# switchport trunk encapsulation dot1q
SW1(config-if)# switchport mode trunk


interface range e2/1 - 3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 2 mode active

interface Port-channel 2
 switchport trunk encapsulation dot1q
 switchport mode trunk

```

```
SW2(config)# interface range e2/1 - 3
SW2(config-if-range)# switchport trunk encapsulation dot1q
SW2(config-if-range)# switchport mode trunk
SW2(config-if-range)# channel-group 2 mode active

SW2(config)# interface port-channel 2
SW2(config-if-range)# switchport trunk encapsulation dot1q
SW2(config-if)# switchport mode trunk


interface range e2/1 - 3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 2 mode active

interface Port-channel 2
 switchport trunk encapsulation dot1q
 switchport mode trunk

```
---

```
SW3(config)# interface range e1/0 - 2
SW3(config-if-range)# switchport trunk encapsulation dot1q
SW3(config-if-range)# switchport mode trunk
SW3(config-if-range)# channel-group 3 mode active

SW3(config)# interface port-channel 3
SW3(config-if-range)# switchport trunk encapsulation dot1q
SW3(config-if)# switchport mode trunk


interface range  e1/0 - 2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 3 mode active

interface Port-channel 3
 switchport trunk encapsulation dot1q
 switchport mode trunk

```

```
SW2(config)# interface range e1/0 - 2
SW2(config-if-range)# switchport trunk encapsulation dot1q
SW2(config-if-range)# switchport mode trunk
SW2(config-if-range)# channel-group 3 mode active

SW2(config)# interface port-channel 3
SW2(config-if-range)# switchport trunk encapsulation dot1q
SW2(config-if)# switchport mode trunk


interface range e1/0 - 2
 switchport trunk encapsulation dot1q
 switchport mode trunk
 channel-group 3 mode active

interface Port-channel 3
 switchport trunk encapsulation dot1q
 switchport mode trunk
```



