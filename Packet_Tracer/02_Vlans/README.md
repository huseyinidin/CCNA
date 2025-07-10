# 📚 VLANs (Virtual Local Area Networks)

## 🧠 VLAN Nedir?

Bir ağda **VLAN’lar** (_Virtual Local Area Networks_), ağ trafiğini **mantıksal olarak farklı ağlara ayırmak** için kullanılır. Her VLAN, farklı bir yayın domaini oluşturur ve **güvenli, verimli, düzenli** ağlar kurmak için kullanılır.

- Aynı switch üzerindeki portlar, farklı VLAN'lara atanarak **ayrı broadcast domain**’ler oluşturulabilir.
- VLAN sayesinde ağlar **daha güvenli, daha yönetilebilir ve segmentlere ayrılmış** hale gelir.

---

- Aşağıda en sık kullanılan VLAN türleri ve yapılandırma örnekleri açıklanmıştır:

## 📦 VLAN Türleri

| VLAN Türü        | Açıklama |
|------------------|----------|
| **Default VLAN** | Tüm switch portları başlangıçta VLAN 1’e aittir. |
| **Data VLAN**    | Kullanıcı veri trafiğini taşıyan VLAN’lardır. |
| **Voice VLAN**   | IP telefonların ses trafiğini taşır. (QoS desteği gerekir) |
| **Management VLAN** | Switch yönetimi için kullanılan VLAN (genellikle VLAN 1 yerine VLAN 99 tercih edilir). |
| **Native VLAN**  | Trunk bağlantılarda etiketlenmemiş (untagged) trafiğin taşındığı VLAN’dır. |
| **Trunk VLAN**  | Birden fazla VLAN’ın, aynı fiziksel port üzerinden iletilmesini sağlar. |
| **Private VLAN**  | Aynı VLAN içindeki portlar arasında izolasyon sağlar. |
| **Static VLAN**  | Portlar, belirli bir VLAN'a manuel olarak atanır. | 
| **Dynamic VLAN**  | Portlar, kullanıcıların MAC adresi veya kimlik doğrulaması temelinde otomatik olarak VLAN’a atanır. |
| **Black Hole VLAN** | Bilinmeyen veya yetkisiz cihazların izole edildiği VLAN (güvenlik amaçlı). |

---
## 🎯 VLAN Neden Kullanılır?

- **Broadcast domain’leri sınırlandırmak**
- **Ağ güvenliğini artırmak**
- **Ağ trafiğini yönetilebilir kılmak**
- **Bölümler arası izolasyon sağlamak** (Örn: Muhasebe & IT)

---

## 🛠 VLAN Oluşturma ve Port Atama

### 0️⃣ VLAN Oluşturma

```
SW1(config)# vlan 10
SW1(config-vlan)# name IT
```
---

## 1️⃣ Varsayılan VLAN (Default VLAN)

- Cisco anahtarlarda varsayılan VLAN `1`’dir.  
- Tüm portlar başlangıçta bu VLAN’a üyedir.  
- **Yönetim ve ilk konfigürasyon** için kullanılır.

### 🛠 Konfigürasyon:

Varsayılan VLAN sistemde zaten bulunduğundan özel bir yapılandırma gerekmez. Ancak bir portun VLAN 1’e atanması için:

```
SW1(config)# interface fastethernet0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 1
```
```
interface fastethernet0/1
switchport mode access
switchport access vlan 1
```
---

## 2️⃣ Veri VLAN'ı (Data VLAN / User VLAN)

- **Kullanıcı trafiğini** taşır.  
- Genellikle **departmanları ayırmak** için kullanılır (örneğin: IT, HR, Satış).

### 🛠 Örnek: HR VLAN (VLAN 10) Yapılandırması

```
SW1(config)# vlan 10
SW1(config-vlan)# name IT

SW1(config)# interface fastethernet0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10
```
```
vlan 10
name IT

interface fastethernet0/1
switchport mode access
switchport access vlan 10
```

---

## 3️⃣ Ses VLAN'ı (Voice VLAN)

- **VoIP cihazları** için özel VLAN’dır.  
- **QoS (Quality of Service)** sağlar, önceliklidir.  
- Ses ve veri trafiği aynı porta bağlanan cihazlarda ayrıştırılarak iletilir.

### 🛠 VLAN 20 ile Ses VLAN Yapılandırması

```
SW1(config)# vlan 20
SW1(config-vlan)# name VOICE

SW1(config)# interface fastethernet0/1
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 10   ! PC de bağlanacaksa
SW1(config-if)# switchport voice vlan 20
```
```
vlan 20
name VOICE

interface fastethernet0/1
switchport mode access
switchport access vlan 10   ! PC de bağlanacaksa
switchport voice vlan 20
```
---

## 4️⃣ Yönetim VLAN'ı (Management VLAN)

- **SSH, Telnet, SNMP** gibi yönetim trafiği için ayrılmıştır.  
- Genellikle **veri trafiğinden izole edilir**.

### 🛠 VLAN 99 ile Yönetim IP Ayarı

```
SW1(config)# vlan 99
SW1(config-vlan)# name Management

SW1(config)# interface vlan 99
SW1(config-if)# ip address 192.168.99.2 255.255.255.0
SW1(config-if)# no shutdown

SW1(config)# interface fastethernet0/1
SW1(config-if)# switchport access vlan 99
```
```
vlan 99
name Management

interface vlan 99
ip address 192.168.99.2 255.255.255.0
no shutdown

interface fastethernet0/1
switchport access vlan 99
```
---

## 5️⃣ Yerel VLAN (Native VLAN)

- **802.1Q trunking**'de **etiketsiz (untagged)** trafiği taşır.  
- Her trunk port **yalnızca bir native VLAN**’a sahip olabilir.  
- Native VLAN, genellikle **yönetimsel nedenlerle ayrılır** ve güvenlik açısından dikkatle yapılandırılmalıdır.
- Yönetim vlan'ı ile Yerel vlan'ın standart'ı yoktur. İstediğiniz vlan numarasını verebilirsiniz. 

### 🛠 Trunk Port için Native VLAN 98 Ayarı

```
SW1(config)# interface gigabitethernet0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk native vlan 98

SW1(config-if)# switchport trunk encapsulation dot1q    ! Bu komut L3 switch üzerinde çalışır! 
 
```
---


## 6️⃣ Trunk VLAN  

- **Birden fazla VLAN’ın**, **aynı fiziksel port üzerinden** iletilmesini sağlar.  
- Genellikle **Switch-Switch** veya **Switch-Router** bağlantılarında kullanılır.  
- **Trunk port**, belirli VLAN'ların trafiğini taşıyacak şekilde yapılandırılır.

### 🛠 Trunk Port Konfigürasyonu

```
SW1(config)# interface gigabitethernet0/1
SW1(config-if)# switchport mode trunk
SW1(config-if)# switchport trunk allowed vlan 10,20,99
SW1(config-if)# switchport trunk allowed vlan 10,20,99
```
---


## 7️⃣ Özel VLAN (Private VLAN - PVLAN) Aynı VLAN içindeki **portlar arasında izolasyon** sağlar.  


- Aynı VLAN içindeki **portlar arasında izolasyon** sağlar.  
- Özellikle **veri merkezlerinde** yaygın olarak kullanılır.  
- Üç temel mod içerir:
  - **Promiscuous:** Herkesle iletişim kurabilir.
  - **Isolated:** Yalnızca promiscuous port ile iletişim kurabilir.
  - **Community:** Kendi grubu ve promiscuous port ile iletişim kurabilir.

### 🛠 Temel PVLAN Yapılandırması (Catalyst Switch)

```
SW1(config)# vlan 100
SW1(config-vlan)# private-vlan primary

SW1(config)# vlan 101
SW1(config-vlan)# private-vlan isolated

SW1(config)# vlan 102
SW1(config-vlan)# private-vlan community

SW1(config)# vlan 100
SW1(config-vlan)# private-vlan association 101,102

SW1(config)# interface gigabitethernet0/2
SW1(config-if)# switchport mode private-vlan host
SW1(config-if)# switchport private-vlan host-association 100 101

SW1(config)# interface gigabitethernet0/3
SW1(config-if)# switchport mode private-vlan promiscuous
SW1(config-if)# switchport private-vlan mapping 100 101,102
```
---


## 8️⃣ Statik VLAN 

- Portlar, belirli bir VLAN'a **manuel olarak atanır**.
- Bu yöntem sayesinde **daha fazla kontrol** ve **güvenlik** sağlanır.  
- Genellikle küçük ve orta ölçekli ağlarda tercih edilir.

### 🛠 Statik VLAN 30’a Port Atama

```
SW1(config)# vlan 30
SW1(config)# interface fastethernet0/5
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 30
```
---


## 9️⃣ Dinamik VLAN 

- Portlar, kullanıcıların **MAC adresi** veya **kimlik doğrulaması** temelinde otomatik olarak VLAN’a atanır.
- Eski yöntem **VMPS** (VLAN Management Policy Server) ile yapılırken, günümüzde **802.1X + RADIUS** kullanımı yaygındır.  
- Bu yöntem, daha esnek ve merkezi yönetim sağlar.

### 🛠 Temsili 802.1X + Dinamik VLAN Yapılandırması

```
SW1(config)# aaa new-model
SW1(config)# aaa authentication dot1x default group radius
SW1(config)# dot1x system-auth-control

SW1(config)# interface fastethernet0/6
SW1(config-if)# switchport mode access
SW1(config-if)# authentication port-control auto
SW1(config-if)# dot1x pae authenticator
```
---

## 1️⃣0️⃣ Black Hole VLAN 

**Black Hole VLAN**, ağda oluşturulan ve içine gelen tüm trafiğin yok sayıldığı (düşürüldüğü) özel bir VLAN türüdür. Bu VLAN’a yönlendirilen paketler başka cihazlara iletilmez, yani “kara delik” gibi trafiği yutar.

---

### Neden Kullanılır?

- **Güvenlik:** Yetkisiz veya zararlı cihazların ağda etkili olmasını engellemek için.  
- **Ağ Performansı:** Sorunlu cihazlardan veya portlardan gelen istenmeyen trafiği izole etmek için.  
- **Broadcast Storm Koruması:** Yayılabilecek fazla broadcast/multicast trafiğinin önüne geçmek için.

---

### Nasıl Çalışır?

Switch üzerinde bir VLAN (örneğin VLAN 999) Black Hole VLAN olarak atanır.  
Bu VLAN’a atanmış portlardan veya VLAN üzerinden gelen trafik **silinir** ve ağda başka bir yere ulaşmaz.

---

### Örnek 

Bir şirkette bazı portlara yetkisiz cihazlar bağlanıyor ve ağ performansını etkiliyor. Bu portlar, Black Hole VLAN olarak ayarlanan VLAN 999’a atanır. Böylece bu portlardan gelen trafik yok edilir.

---

### 🛠 Black Hole VLAN Yapılandırması

```
SW1(config)# vlan 999
SW1(config-vlan)# name BLACKHOLE

SW1(config)# interface fastethernet0/20
SW1(config-if)# switchport mode access
SW1(config-if)# switchport access vlan 999

```