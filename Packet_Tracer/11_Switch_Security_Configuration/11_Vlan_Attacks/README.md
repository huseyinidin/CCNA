# VLAN Saldırılarını Azaltma 

## 📌 Giriş
VLAN (Virtual Local Area Network), ağları mantıksal olarak ayırarak güvenlik, yönetilebilirlik ve performans avantajı sağlar. Ancak, yanlış yapılandırılmış VLAN ortamları **VLAN Hopping** gibi saldırılara açık olabilir.  
Bu yazıda VLAN saldırı türlerini ve bunlara karşı alınabilecek önlemleri ele alacağız.

---

## 🔍 VLAN Saldırı Türleri

### 1. Switch Spoofing
- Saldırgan, switch ile trunk bağlantısı kuruyormuş gibi davranır.
- Yanlış yapılandırılmış portlar otomatik trunk moduna geçerse saldırgan diğer VLAN'lara erişebilir.

### 2. Double Tagging
- Saldırgan, paketin içine iki VLAN etiketi ekler.
- İlk etiket, switch tarafından kaldırılır ve paket ikinci VLAN etiketi ile başka VLAN’a yönlendirilir.
- Özellikle **yerel VLAN** saldırılarında etkilidir.

---

## 🛡 VLAN Saldırılarından Korunma Yöntemleri

### 1. Kullanılmayan Portları Devre Dışı Bırakma
Kullanılmayan tüm portlar kapatılmalı ve varsayılan VLAN’dan çıkarılmalıdır.


📌 Sonuç

- VLAN güvenliği, çoğu zaman doğru yapılandırma ile sağlanır.
- Kullanılmayan portları kapatın ve Black Hole VLAN’a taşıyın.
- Native VLAN’ı değiştirin.
- DTP’yi devre dışı bırakın.
- Trunk VLAN listesini kısıtlayın.
- Gerektiğinde VACL ve PVLAN kullanın.
- Port Security ile yetkisiz erişimi engelleyin.

🔒 Unutmayın: Güvenli VLAN yapılandırması, saldırganların ağınızda yatay hareket etmesini büyük ölçüde zorlaştırır.