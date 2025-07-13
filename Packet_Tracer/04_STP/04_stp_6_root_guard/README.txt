# 🛡️ Root Guard Nedir?

**Root Guard**, bir switch portunun üzerinden **Root Bridge olma isteği** (BPDU) algılanırsa, bu portu **geçici olarak devre dışı (root-inconsistent)** duruma getirir.

## 🎯 Amaç

- Spanning Tree Protocol (STP) içinde **istenmeyen root bridge değişikliklerini önlemek**.
- Root Bridge’ın sadece **istenen switch** olmasını sağlamak.
- Özellikle **core (omurga) – access (erişim)** yapılarında Root Bridge istikrarını korur.

---

## 📍 Nerede Kullanılır?

Root Guard genellikle **ağın erişim katmanında (Access Layer)**,  
**Root Bridge olmaması gereken portlarda** kullanılır:

| Kullanım Alanı      | Açıklama                                                                 |
|---------------------|--------------------------------------------------------------------------|
| **Access Switch portları** | Kullanıcı cihazlarının bağlı olduğu portlar — Root Bridge olmamalı           |
| **Dağıtım katmanı (Distribution)** | Root'un sadece belirli switchlerde kalması isteniyorsa tercih edilir |
| **Yedek bağlantılar**     | Geçici olarak bağlantı eklenen yerlerde istenmeyen root seçimlerini engeller |

---

## ⚙️ Yapılandırma Komutu

```
Switch(config)# interface fastethernet0/2
Switch(config-if)# spanning-tree guard root
```

```
interface fastethernet0/2
spanning-tree guard root
```

---

## 🔧 Nasıl Çalışır?

Root Guard yapılandırılmış bir port üzerinden, **daha düşük priority (daha "iyi" BPDU)** algılanırsa şu adımlar gerçekleşir:

---

### 🧬 İşleyiş Sırası:

1. 🚨 **Daha iyi bir Root Bridge adayından BPDU alınır.**
2. 🔐 **Root Guard etkin olan port**, bu BPDUlardan dolayı **"root-inconsistent"** durumuna geçer.
3. 🔁 Port, **trafik taşıyamaz** (STP topolojisi korunur).
4. ✅ Doğru BPDU (mevcut root bridge’ten) tekrar algılandığında:
   - Port, **otomatik olarak forwarding moduna** döner.
   - Trafik yeniden taşınmaya başlar.

### 📌 Önemli Not:

> Root-inconsistent durumu, bir tür **koruma modudur**.  
> STP döngüsünü bozacak Root Bridge değişimini **engeller ama portu kalıcı olarak kapatmaz.**


### 🛑 Ne Zaman Devreye Girer?

- Core/Root Bridge dışında bir switch’in Root olmaya çalıştığı durumda.
- Yani Root Guard yapılandırılmış bir port üzerinden "ben Root olmak istiyorum" anlamına gelen **BPDU** gelirse.

> 🎯 **Amaç:** STP topolojisini bozabilecek istenmeyen Root seçimlerini engelleyerek ağı kararlı tutmak.

---

## ✅ Avantajları

Root Guard, STP güvenliğini artırmak ve topoloji istikrarını sağlamak için önemli avantajlar sunar:


- 🌐 **Root Bridge’in Kontrolünü Sağlar**  
  Ağda yalnızca istenen cihazın Root Bridge olmasına izin verir.  
  İstenmeyen switch’lerin Root olmaya çalışmasını engeller.

- 🔐 **STP Güvenliğini Artırır**  
  Özellikle büyük kampüs, veri merkezi ve kritik altyapılarda  
  Spanning Tree topolojisinin bozulmasını önler.

- 🤖 **Otomatik Kurtarma Özelliği Vardır**  
  Port, uygunsuz BPDU algılandığında "root-inconsistent" duruma geçer,  
  ancak doğru BPDU algılandığında **manuel müdahale gerekmeden otomatik olarak** yeniden aktif hale gelir.

---

> 💡 **Sonuç:** Root Guard, ağ güvenliği ve sürekliliği açısından kritik bir Spanning Tree koruma mekanizmasıdır.