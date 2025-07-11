# 🔀 Spanning Tree Protocol (STP) 

## ⚙️ STP'nin İşleyişi (Temel İşlemleri)

STP, ağdaki döngüleri engellemek için aşağıdaki temel adımları uygular:

### 1. 👑 Root Bridge Seçimi  
- Tüm switch'ler kendi Bridge ID’si ile yarışır  
- En düşük Bridge ID’ye sahip switch "Root Bridge" olur

### 2. 📶 Port Rolü Atamaları  
- **Root Port (RP):** Root Bridge’e en kısa yoldan giden port  
- **Designated Port (DP):** Her segmentte en iyi yola sahip port  
- **Blocked Port:** Yedek yollar, döngü engellemek için pasif kalır

### 3. 🔄 BPDU (Bridge Protocol Data Unit) Değişimi  
- Switch'ler sürekli BPDU mesajları göndererek STP bilgilerini paylaşır

### 4. 🧼 Topoloji Değişikliği Tespiti  
- Yeni cihaz eklendiğinde, kablo çıkarıldığında veya Root değiştiğinde  
  → STP yeni hesaplama yapar

### 🔢 Varsayılan Priority Değeri

- **Varsayılan Priority**: `32768`
- Değerler yalnızca **4096'nın katları** olacak şekilde değiştirilebilir:
  - Geçerli değerler: `0`, `4096`, `8192`, `12288`, ..., `61440`

> ❗ `0` en yüksek önceliktir (Root Bridge olma şansı en fazla olan değerdir).

---

## STP Show Spanning-Tree Komutu

### STP Port Rolleri ve Durumlarının Açıklamaları

| Kısaltma | Açılımı    | Anlamı                                                                                      |
|----------|------------|--------------------------------------------------------------------------------------------|
| **Root** | Root Port  | Bu port, switch’in Root Port’u yani Root Bridge’e en kısa yol sağlayan portudur.           |
| **Desg** | Designated | Her ağ segmentinde veri iletiminden sorumlu port. O segmentte en iyi yol olarak seçilmiştir.|
| **FWD**  | Forwarding | Port aktif, veri trafiği gönderir ve alır. Port forwarding (iletim) durumundadır.          |
| **Altn** | Alternate  | Alternatif port — Root port olmayan, Root Bridge'e alternatif yol sağlayan port.            |
| **BLK**  | Blocking   | Bu port trafiğe kapalı (bloklanmış), sadece BPDU paketleri dinler, veri iletmez.           |


### 🔁 STP Durumları ve Süreleri

| Port Durumu     | Açıklama                                                | Varsayılan Süre |
|------------------|-----------------------------------------------------------|------------------|
| **Blocking**     | Sadece BPDU dinlenir, veri iletilmez, MAC öğrenilmez     | 20 saniye (ilk açılışta) |
| **Listening**    | BPDU'lar analiz edilir, MAC öğrenilmez                   | 15 saniye        |
| **Learning**     | MAC adresleri öğrenilir, veri trafiği hala iletilmez     | 15 saniye        |
| **Forwarding**   | Veri trafiği başlar, MAC adresleri öğrenilir             | Kalıcı           |
| **Disabled**     | Port kapalı ya da manuel olarak devre dışı               | Kalıcı           |

---

### 📌 Önemli Notlar

- **Listening + Learning** toplamda **30 saniyelik gecikme** oluşturur.
- Bu gecikmeler, **STP zamanlayıcıları** olan `Forward Delay` değeri ile belirlenir (varsayılan: 15 saniye).
- **Blocking** durumu kalıcı olabilir; STP portu loop riski varsa bu modda kalır.
- **Disabled** durumu port fiziksel olarak kapatıldığında ya da yöneticiler tarafından manuel olarak devre dışı bırakıldığında görülür.

---

### ⚡ RSTP (Rapid STP) ile Süreler

- RSTP, klasik STP’ye göre çok daha hızlıdır.
- Bu süreler RSTP’de **milisaniyeler ile ölçülür** ve genellikle birkaç saniyeye kadar düşer.
- RSTP ile ağ toparlanma süresi ciddi oranda azalır.

---


# 🌐 Spanning Tree Protocol (STP) – 20 Maddede Temel Bilgi ve Komutlar

## 🧠 1. STP Nedir?

**STP (Spanning Tree Protocol)**, anahtarlamalı ağlarda **loop (döngü)** oluşmasını önleyen bir protokoldür.  
Ağda aynı paketin tekrar tekrar dolanmasını engellemek için bazı bağlantıları geçici olarak devre dışı bırakır.

---

## 🧩 2. Döngü (Loop) Nedir?

Birden fazla switch birbirine bağlıysa, aynı veri paketi sürekli dönüp durabilir.  
Bu sonsuz trafiğe **broadcast storm** denir ve ağı felç eder.

---

## 📌 3. STP Ne Yapar?

STP, ağdaki döngüleri algılar ve bu döngüleri **geçici olarak bağlantıları engelleyerek (blocking)** önler.

---

## 🧱 4. STP Nasıl Çalışır?

STP, önce ağı tarar ve en uygun switch’i **Root Bridge** olarak belirler.  
Daha sonra bağlantıların en kısa yolu hesaplanarak bazıları kapatılır.

---

## 🏛️ 5. Root Bridge Nedir?

Ağın merkezi olarak görev yapan **ana switch**’tir.  
Tüm STP hesaplamaları Root Bridge’e göre yapılır.

---

## 🪙 6. Root Bridge Nasıl Seçilir?

STP, her switch'e ait **Bridge ID**'ye bakar:  
Bridge ID = `priority + MAC address`  
En düşük değerli switch, Root Bridge olur.

---

## 🔧 7. Bridge Priority Değeri Nasıl Değiştirilir?

```
Switch(config)# spanning-tree vlan 1 priority 0
```
---

## 🌉 8. STP Port Türleri

| Port Türü       | Görev                                                 |
|------------------|--------------------------------------------------------|
| **Root Port**        | Root Bridge'e giden en kısa yolu sağlayan port         |
| **Designated Port**  | Her segmentte veri iletimine açık port                |
| **Blocked Port**     | Loop'u önlemek için geçici olarak kapatılmış port     |

---

## 🔍 9. STP Port Rolleri Nasıl Görülür?

```
Switch# show spanning-tree
```

Bu komut, switch üzerindeki tüm portların STP durumlarını ve rollerini listeler.

---

## ⏱️ 10. STP Zamanlayıcıları

| Zamanlayıcı     | Açıklama                               | Varsayılan Değer |
|------------------|------------------------------------------|-------------------|
| **Hello Time**    | BPDU gönderim sıklığı                   | 2 saniye          |
| **Forward Delay** | Listening ve Learning süreleri          | 15 saniye         |
| **Max Age**       | BPDU geçersizlik (timeout) süresi       | 20 saniye         |

---

## 🚦 11. STP Durumları (Port States)

STP çalışırken her port aşağıdaki beş durumdan birinde bulunabilir:

- **Blocking** – BPDU’ları dinler ama veri iletimi yapmaz.  
- **Listening** – MAC adresi öğrenilmez, sadece BPDU’lar analiz edilir.  
- **Learning** – MAC adresleri öğrenilir, ancak hala veri trafiği iletilmez.  
- **Forwarding** – Veri trafiği gönderilir ve alınır, port aktif durumdadır.  
- **Disabled** – Port kapalıdır veya manuel olarak devre dışı bırakılmıştır.

---

## 📡 12. BPDU Nedir?

**BPDU (Bridge Protocol Data Unit)**, STP bilgisini switch’lerin birbiriyle paylaşmak için kullandığı veri birimidir.

Switch’ler BPDU göndererek ağın topolojisini öğrenir ve döngü (loop) oluşumunu kontrol eder.

---

## ⚡ 13. STP Aktif mi? Nasıl Kontrol Edilir?

STP'nin çalışıp çalışmadığını kontrol etmek için aşağıdaki komut kullanılır:

```
Switch# show spanning-tree vlan 1
```
---

## 🧪 14. RSTP (Rapid STP) Nasıl Aktif Edilir?

**RSTP (Rapid Spanning Tree Protocol)**, klasik STP'ye göre çok daha hızlı çalışır ve ağda bir bağlantı değişikliği (topoloji değişimi) olduğunda çok daha kısa sürede toparlanma sağlar.

Cisco cihazlarda RSTP'yi etkinleştirmek için şu komut kullanılır:

```
Switch(config)# spanning-tree mode rapid-pvst
```
RSTP ile aşağıdaki avantajlar sağlanır:

- Port durumları daha hızlı değişir (blocking yerine discarding durumu gelir)

- Toparlama süresi 50 saniyeye kadar değil, birkaç saniyeye iner.

---

## 🧰 15. PortFast – Uç Cihazlar İçin

**PortFast**, uç cihazlara (örneğin bilgisayar, yazıcı, IP telefon gibi) bağlı switch portlarının  
STP bekleme sürelerini (Listening ve Learning) atlayarak **doğrudan Forwarding moduna** geçmesini sağlar.

### 🎯 Avantajı Nedir?

- Bilgisayarlar ve diğer uç cihazlar çok daha hızlı ağa bağlanabilir.
- DHCP istemcileri IP adresini daha çabuk alır.
- STP geçiş süresi ortadan kalkar (normalde 30-50 saniye).

### ⚙️ PortFast Nasıl Aktif Edilir?

Bireysel bir port için:

```
Switch(config-if)# spanning-tree portfast
```
⚠️ Dikkat Edilmesi Gerekenler
   🔒 PortFast yalnızca uç cihazlara (end devices) bağlı portlarda kullanılmalıdır.
   Eğer PortFast aktif bir porta başka bir switch bağlanırsa, loop oluşabilir!

**Aşağıdaki komutla tüm access portlar için global olarak PortFast açılabilir:**

```
Switch(config)# spanning-tree portfast default
```
---

## 🔐 16. BPDU Guard – Güvenlik Amaçlı

**BPDU Guard**, PortFast özelliği açık olan portlara **BPDU (Bridge Protocol Data Unit)** gelmesi durumunda,  
portu otomatik olarak **err-disabled (hatalı durumda kapalı)** konuma getirir.  
Bu özellik, **loop oluşumunu engellemek** ve ağı korumak amacıyla kullanılır.

### 🎯 Neden Kullanılır?

- Uç cihazlara bağlı portlara yanlışlıkla bir switch bağlanırsa loop oluşabilir.
- BPDU Guard, bu durumu fark edip portu kapatarak ağı korur.
- Özellikle **kullanıcı hataları** veya **yanlış bağlantılar** için ideal bir güvenlik önlemidir.

### ⚙️ BPDU Guard Nasıl Aktif Edilir?

**PortFast açık bir arayüzde BPDU Guard’ı aktifleştirmek için:**

```
Switch(config-if)# spanning-tree bpduguard enable
```
⚠️ Dikkat Edilmesi Gerekenler
   🔐 BPDU Guard genellikle PortFast ile birlikte kullanılır.
   Bu sayede uç cihaz portlarının switch bağlantısı gibi davranmasının önüne geçilir.
---

## 📁 17. STP Modları Nelerdir?

Cisco cihazlarda STP için 3 farklı mod bulunmaktadır:

| Komut                                 | Açıklama                                  |
|-------------------------------------|-------------------------------------------|
| `spanning-tree mode pvst`            | Her VLAN için ayrı STP örneği (PVST)      |
| `spanning-tree mode rapid-pvst`      | Hızlı STP (RSTP tabanlı, Rapid PVST)      |
| `spanning-tree mode mst`             | Çoklu VLAN’lar için ortak STP örneği (MST) |

### Örnek Komutlar:

```
Switch(config)# spanning-tree mode pvst
Switch(config)# spanning-tree mode rapid-pvst
Switch(config)# spanning-tree mode mst
```
---

## 🎯 18. Root Bridge Hangisi? Nasıl Anlaşılır?

Root Bridge’i tespit etmek için aşağıdaki komut kullanılır:

```
Switch# show spanning-tree
```
---

## 🧮 19. Root Port Nasıl Seçilir?

Switch üzerinde Root Bridge’e giden en düşük **Path Cost** değerine sahip port, **Root Port** olarak seçilir.

Bu port, Root Bridge’e veri iletimi için en uygun yolun bulunduğu porttur.

---

**Path Cost Hesaplama Örneği:**

| Bağlantı Hızı | Path Cost (Varsayılan) |
|---------------|-----------------------|
| 10 Mbps       | 100                   |
| 100 Mbps      | 19                    |
| 1 Gbps        | 4                     |
| 10 Gbps       | 2                     |

> Not: Daha düşük Path Cost, daha kısa ve daha hızlı bağlantı anlamına gelir.

---

🛑 20. Loop Önlenmiş mi? Kontrol Et

Ağda loop oluşup oluşmadığını kontrol etmek için aşağıdaki komut kullanılır:
  
```
Switch# show spanning-tree
```

Eğer herhangi bir port “Blocking” durumundaysa,
STP düzgün çalışıyor ve döngüyü önlüyor demektir.

Loop oluştuğunda, STP bu portları geçici olarak kapatarak ağın stabil kalmasını sağlar.


