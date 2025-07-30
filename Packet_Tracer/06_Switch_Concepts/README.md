# 🖧 Switching Concepts 

## 📘 Tanım

**Switching**, bir ağda veri trafiğini yönlendirme işlemidir. Özellikle **LAN (Local Area Network)** ortamlarında kullanılan **switch** cihazları, veri paketlerini hedef cihaza en verimli şekilde iletmek için kullanılır.

Switching, **OSI modelinin Layer 2 (Data Link Layer)** katmanında çalışır ve **MAC adreslerini** kullanarak veri iletimini sağlar. Daha gelişmiş bazı switch'ler **Layer 3 (Network Layer)**'da da yönlendirme (routing) yapabilir.

---

## 🔍 Özellikleri

- **MAC Adres Tabanlı Çalışma**: Her port, bağlı cihazların MAC adresini öğrenir ve bu bilgileri MAC adres tablosuna kaydeder.
- **Full-Duplex İletim**: Aynı anda veri gönderip alma kapasitesine sahiptir, çakışmaları (collision) önler.
- **Collision Domain Ayrımı**: Her switch portu ayrı bir collision domain oluşturur.
- **Broadcast Domain**: Varsayılan olarak tüm switch portları aynı broadcast domain’dedir. VLAN kullanılarak ayrılabilir.
- **MAC Address Table**: Hangi MAC adresinin hangi porta bağlı olduğunu gösteren tablo tutulur.
- **Learning, Filtering, Forwarding**: Çerçeveleri öğrenir, gerektiğinde filtreler ve hedefe iletir.
- **Loop Önleme**: STP (Spanning Tree Protocol) gibi protokollerle ağ döngüleri engellenir.

---

## ⚙️ Switching Türleri

### 1. Store-and-Forward Switching
- Frame tamamen alınır.
- CRC (Cyclic Redundancy Check) ile hata kontrolü yapılır.
- Güvenlidir ama gecikme olabilir.

### 2. Cut-Through Switching
- Sadece hedef MAC adresi okunduktan sonra frame hemen iletilir.
- Hızlıdır ama hata kontrolü yapılmaz.

### 3. Fragment-Free Switching
- İlk 64 byte okunduktan sonra frame iletilir.
- Hız ve güvenilirlik arasında dengelidir.

---

## 🧠 MAC Address Table İşleyişi

1. **Learning**: Kaynak MAC adresi öğrenilir ve ilgili porta kaydedilir.
2. **Forwarding**: Hedef MAC adresi tabloya bakılarak uygun porta yönlendirilir.
3. **Flooding**: Hedef MAC adresi bilinmiyorsa tüm portlara gönderilir.
4. **Aging**: Belirli bir süre aktif olmayan adresler tablodan silinir.

---

## 🛡️ Anahtarlamanın Avantajları

- ✅ Yüksek hızda veri iletimi sağlar.
- ✅ Çakışmaları azaltır, verimliliği artırır.
- ✅ LAN performansını iyileştirir.
- ✅ Mikro-segmentasyon ile daha az trafik çakışması yaşanır.
- ✅ VLAN desteği ile mantıksal ağ bölünmesi yapılabilir.
- ✅ Güvenlik politikaları (Port Security, ACL vb.) uygulanabilir.

---

## 📌 Ek Bilgi

- Layer 2 switch'ler yönlendirme yapmaz, MAC adresleri ile çalışır.
- Layer 3 switch'ler IP tabanlı yönlendirme de yapabilir.
- VLAN konfigürasyonu ile switch üzerinde sanal ağlar oluşturulabilir.
