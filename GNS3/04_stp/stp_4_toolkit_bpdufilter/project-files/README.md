# 🔌 GNS3 Üzerinde STP – `spanning-tree bpdufilter enable` İncelemesi

## 🎯 Amaç

`spanning-tree bpdufilter enable` komutunun amacı, belirli portlardan BPDU (Bridge Protocol Data Unit) gönderimini ve alınmasını engellemektir. 

Bu komut, özellikle uç cihazlara (host/PC gibi) bağlı portlarda kullanılır ve bu portlarda STP (Spanning Tree Protocol) işlemine katılımı devre dışı bırakır. Böylece port, doğrudan forwarding (iletime) geçer.

> ⚠️ **Uyarı:** Bu komut dikkatli kullanılmazsa ağda Layer 2 döngü (loop) oluşmasına neden olabilir. Çünkü STP devre dışı kaldığında switch’ler arasında BPDU alışverişi engellenir ve döngüleri engelleyen yapı ortadan kalkar.

## 📌 Kullanım Senaryosu

GNS3 üzerinde yapılan bir testte, bir switch’in Ethernet 0/2 portuna önce bir PC (host) bağlanmış, ardından aynı porta başka bir switch bağlanarak `spanning-tree bpdufilter enable` komutu ile davranış gözlemlenmiştir. Bu test, Wireshark ile kayıt altına alınarak BPDU paketlerinin gönderilip gönderilmediği analiz edilmiştir.

### 1️⃣ PC Bağlıyken:
- BPDU gönderimi/alımı yapılmaz.
- Port doğrudan forwarding durumuna geçer.
- STP süresi beklenmeden bağlantı aktif olur.

### 2️⃣ Switch Bağlandığında:
- Eğer diğer switch BPDU gönderirse, bu port bunları almaz ve kendi BPDU’sunu da göndermez.
- Bu durumda ağda STP çalışmaz ve döngü riski oluşur.

## 🧠 Özet

- ✅ **Avantajı:** Uç cihazlara hızlı bağlantı sağlanır, STP geçiş süresi ortadan kalkar.
- ❌ **Dezavantajı:** Yanlış konfigürasyonda ciddi loop riski taşır.
- 🔒 **Güvenli Kullanım:** Sadece uç cihazlara bağlı portlarda kullanılmalı, başka bir switch’in bağlanması engellenmelidir.

---

📚 Daha güvenli bir alternatif olarak `spanning-tree portfast` komutu da değerlendirilebilir. Bu komut STP'yi tamamen devre dışı bırakmaz; BPDU gönderimi devam eder, sadece STP bekleme süresi atlanır.