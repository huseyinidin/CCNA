# 🔒 **Layer 2 Security Threats** 

**Layer 2** (Veri Linki Katmanı), OSI modelinde, ağ cihazları arasındaki doğrudan iletişimi sağlayan katmandır. Bu katman, veri iletimi sırasında MAC adreslerini kullanarak cihazlar arasında veri iletir. Ancak, Layer 2, özellikle güvenlik açısından birçok zafiyet barındırır. Saldırganlar, Layer 2'nin zayıf noktalarını kullanarak ağlara izinsiz erişim sağlayabilir, verileri manipüle edebilir veya ağ performansını bozabilirler.

## ⚠️ **Layer 2 Güvenlik Tehditleri** 

### 1. 🕵️‍♂️ **MAC Spoofing**

**MAC Spoofing**, bir cihazın MAC adresini taklit ederek ağda kimlik doğrulama sürecini atlatmak amacıyla yapılan bir saldırıdır. Bir saldırgan, kendini farklı bir cihaz olarak gösterebilir ve yetkilendirilmiş cihazlardan gelen trafiği izlemesi veya manipüle etmesi için ağda geçerli bir MAC adresi kullanabilir.

- **Riskler**:
  - Ağda yetkisiz cihazların görünmesi.
  - Kimlik doğrulama mekanizmalarının yanıltılması.

### 2. 🧲 **ARP Spoofing (ARP Poisoning)**

**ARP Spoofing**, ağdaki cihazların, kendilerini başka bir cihazın IP adresiyle eşleştirerek trafiği izlemelerine veya yönlendirmelerine izin veren bir saldırıdır. ARP (Address Resolution Protocol), IP adreslerini MAC adreslerine eşleştirir. Saldırgan, yanlış ARP yanıtları göndererek, ağdaki cihazların doğru IP-MAC eşleşmelerini kaybetmesine neden olabilir.

- **Riskler**:
  - Gizli verilerin ele geçirilmesi (örneğin, şifreler, kredi kartı bilgileri).
  - Trafik yönlendirme ve veri manipülasyonu.

### 3. 🔄 **VLAN Hopping**

**VLAN Hopping**, saldırganların bir VLAN’dan diğerine geçerek, sınırları aşmalarını sağlayan bir tekniktir. Bu saldırı, genellikle iki teknikle gerçekleştirilir: 
  - **Double Tagging**: Saldırgan, paketlere iki VLAN etiketi ekler ve bu sayede bir VLAN’dan başka bir VLAN’a geçiş yapar.
  - **Switch Spoofing**: Saldırgan, switch'e kendisini başka bir VLAN üyeliği olarak tanıtarak farklı bir VLAN'a erişim sağlar.

- **Riskler**:
  - Güvenli VLAN’lara izinsiz erişim.
  - Verilerin gizliliği ve bütünlüğünün ihlali.

### 4. 💥 **Switch Spoofing**

**Switch Spoofing**, saldırganın ağdaki bir switch'e kendisini başka bir cihaz gibi tanıtarak switch ile bağlantı kurmasını sağlamasıdır. Bu tür saldırılar, VLAN'lar arası geçişi kolaylaştırabilir ve ağ trafiğini izleme veya manipülasyon için fırsat yaratabilir.

- **Riskler**:
  - VLAN’lar arası geçiş ve gizli verilere erişim.
  - Ağda yetkisiz cihazlar ve trafiğin yönlendirilmesi.

### 5. 🚨 **Flooding Attacks (Storm Attacks)**

Layer 2'deki bazı saldırılar, ağdaki tüm cihazların bant genişliğini tüketen **flooding** saldırılarıdır. Bu tür saldırılar, özellikle ağdaki switch’leri hedef alır. Örneğin, **MAC Flooding** saldırısı, bir switch’in MAC adresi tablosunun dolmasına neden olur, bu da switch’in paketleri broadcast yapmasına yol açar.

- **Riskler**:
  - Ağı tıkama (bandwidth hogging).
  - Sistem çöküşü ve hizmetin kesintiye uğraması.

### 6. 📡 **Jamming ve Denial of Service (DoS)**

Layer 2, ayrıca **Jamming** veya **Denial of Service (DoS)** gibi saldırılara karşı savunmasızdır. Bu tür saldırılar, ağ trafiğini bozar ve cihazların iletişimini engeller. Saldırganlar, sinyalleri tıkayarak veya sistemin kapasitesini aşarak cihazların iletişim kurmasını engelleyebilirler.

- **Riskler**:
  - Ağın tıkanması ve hizmetin kesilmesi.
  - Cihazların ağ üzerinden veri iletmesini engelleme.

### 7. 🌐 **Double Tagging**

**Double Tagging**, saldırganların iki VLAN etiketi ekleyerek, bir paketin birden fazla VLAN’a yönlendirilmesini sağladığı bir saldırıdır. Bu yöntemle, bir paket hedef VLAN'a yönlendirilmeden önce, ilk VLAN etiketinden çıkarılabilir ve ikinci VLAN’a yönlendirilebilir.

- **Riskler**:
  - Farklı VLAN’larda veri sızıntıları.
  - Etiketleme hatalarıyla ağda ciddi güvenlik zafiyetleri oluşturulması.

### 8. 🔓 **Port Security Bypass**

Ağdaki **port security** özellikleri, belirli cihazların ağ bağlantı noktalarına bağlanmasını sınırlamak için kullanılır. Ancak saldırganlar, port security kontrolünü aşmak için **MAC address spoofing** veya **physical device attacks** gibi yöntemleri kullanabilir. Bu tür saldırılar, ağdaki cihazların bağlantısını yanlış şekilde yönetebilir.

- **Riskler**:
  - Yetkisiz cihazların ağa bağlanması.
  - Ağ üzerinde izinsiz erişim sağlanması.

## 🔐 **Layer 2 Güvenlik Önlemleri** 

Layer 2 güvenliğini sağlamak için aşağıdaki önlemler alınabilir:

### 1. **VLAN'ları İyi Yönetmek**
VLAN’lar arasındaki geçişleri kontrol altına almak ve sadece gerekli VLAN’lara erişime izin vermek, Layer 2 saldırılarını önlemeye yardımcı olabilir.

### 2. **Port Security Kullanmak**
Switch portlarında port security kullanmak, yalnızca belirli MAC adreslerinin ağ bağlantı noktalarına bağlanmasına izin verir. Bu, yetkisiz cihazların ağınıza bağlanmasını engeller.

### 3. **ARP Monitoring ve Guarding**
ARP spoofing saldırılarına karşı önlem almak için, ARP izleme ve ARP koruması gibi yöntemler kullanılabilir. Bu sayede, yanlış ARP yanıtları engellenebilir.

### 4. **Flooding Saldırılarına Karşı Duyarlılık**
Switch’lerin MAC adresi tablosu kapasitesini aşmalarını engellemek için **MAC filtering** ve **rate-limiting** gibi teknikler kullanılabilir.

### 5. **Layer 3 Geçiş Kullanmak**
Layer 2'deki saldırıları izole etmek için, yönlendiricileri kullanarak Layer 3 geçişi sağlamak iyi bir yöntemdir. Bu, VLAN’lar arasında doğrudan iletişimi sınırlayarak güvenliği artırabilir.
