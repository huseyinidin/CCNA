# 🔑 **Access Control Nedir?** 

**Access Control** (Erişim Kontrolü), sistemlerin, ağların ve fiziksel kaynakların yalnızca yetkilendirilmiş kullanıcılar tarafından erişilmesini sağlayan bir güvenlik mekanizmasıdır. Bu, bilgilerin ve kaynakların korunmasına yardımcı olur, kötü amaçlı erişimi engeller ve yalnızca doğru kişilere doğru izinleri verir. Erişim kontrolü, güvenlik politikalarının ve erişim yönetiminin temel unsurlarından biridir.

## 🧑‍💻 **Access Control Türleri** 

Erişim kontrolü, çeşitli yöntemler ve stratejilerle uygulanabilir. Bu yöntemler genellikle kullanıcılara erişim yetkisi verirken, organizasyonların güvenliğini sağlamaya yönelik farklı yaklaşımlar sunar. En yaygın erişim kontrol türleri şunlardır:

### 1. 🔐 **Zorunlu Erişim Kontrolü (MAC - Mandatory Access Control)**

Zorunlu Erişim Kontrolü, kullanıcıların belirli kaynaklara erişim izinlerini, yalnızca güvenlik politikaları ve sistem yöneticileri tarafından belirlenen kurallara göre verir. Bu yöntem, genellikle hükümet ve askeri sistemlerde kullanılır. 
- **Özellikler**: 
  - Sıkı politikalar ve güvenlik gereksinimleri.
  - Erişim, kullanıcı seviyesinin ötesine geçer.
  
### 2. 🔑 **Discretionary Access Control (DAC) - İsteğe Bağlı Erişim Kontrolü**

İsteğe Bağlı Erişim Kontrolü, kullanıcıların sahip olduğu kaynaklara erişim izni verme konusunda daha fazla esneklik sağlar. Kullanıcılar, kendi verilerine kimlerin erişebileceğine karar verebilir.
- **Özellikler**: 
  - Kullanıcılar kendi kaynaklarına erişimi kontrol eder.
  - Genellikle ev kullanıcıları ve küçük işletmelerde yaygındır.

### 3. 🛡️ **Rol Tabanlı Erişim Kontrolü (RBAC - Role-Based Access Control)**

Rol Tabanlı Erişim Kontrolü, kullanıcıların belirli rollere göre erişim izinlerine sahip olmalarını sağlar. Her rol, belirli bir dizi erişim yetkisiyle ilişkilidir. Örneğin, bir "admin" rolü, "kullanıcı" rolünden daha fazla erişim yetkisine sahiptir.
- **Özellikler**: 
  - Roller üzerinden erişim kontrolü yapılır.
  - Kurumsal yapılar için ideal bir sistemdir.

### 4. 📊 **Atribute Tabanlı Erişim Kontrolü (ABAC - Attribute-Based Access Control)**

Atribute Tabanlı Erişim Kontrolü, erişim iznini sadece kullanıcının rolüne göre değil, aynı zamanda diğer özelliklerine (örneğin, coğrafi konum, cihaz türü) göre de belirler. Bu yaklaşım, daha esnek ve dinamik bir erişim yönetimi sağlar.
- **Özellikler**: 
  - Erişim, birçok faktöre dayanır.
  - Daha karmaşık ve ayrıntılı politikalar içerir.

## ⚙️ **Erişim Kontrolü Politikaları** 

Erişim kontrolü uygulamak için bazı belirli politikalara ihtiyaç vardır. Bu politikalar, kullanıcıların ve cihazların hangi kaynaklara erişebileceğini, hangi durumlarda erişebileceğini ve erişim izinlerinin nasıl denetleneceğini belirler. İşte bazı temel erişim kontrol politikaları:

### 1. 🚪 **Least Privilege (En Az Ayrıcalık)**

En Az Ayrıcalık prensibi, kullanıcıların sadece işlerini yapabilmeleri için gerekli olan minimum erişim seviyelerine sahip olmalarını sağlar. Bu, güvenlik risklerini azaltır.
- **Özellikler**:
  - Kullanıcılara yalnızca ihtiyaç duydukları erişim sağlanır.
  - Sistem üzerindeki gereksiz erişim izinleri ortadan kaldırılır.

### 2. 🔄 **Need to Know (İhtiyaç Duyulan Bilgi)**

Bu politika, kullanıcıların yalnızca görevlerini yerine getirebilmeleri için gerekli olan verilere erişebileceğini belirtir. Gereksiz bilgilere erişim engellenir.
- **Özellikler**:
  - Veriler yalnızca gerekli olduğunda paylaşılır.
  - Bilgi paylaşımı sınırlandırılır.

### 3. 🕵️‍♂️ **Audit Trails (Denetim İzleri)**

Erişim kontrolü, kullanıcı etkinliklerini izleyerek denetim izleri oluşturur. Bu, erişim izinlerinin ve kullanıcı etkinliklerinin izlenmesini sağlar. Denetim izleri, güvenlik ihlallerinin tespit edilmesine yardımcı olabilir.
- **Özellikler**:
  - Kullanıcı etkinlikleri kaydedilir.
  - Şüpheli etkinlikler tespit edilebilir.

### 4. 🛑 **Time-Based Access Control (Zaman Bazlı Erişim Kontrolü)**

Zaman Bazlı Erişim Kontrolü, kullanıcıların yalnızca belirli bir zaman diliminde erişim izni almasını sağlar. Örneğin, bir çalışan yalnızca çalışma saatlerinde belirli verilere erişebilir.
- **Özellikler**:
  - Erişim, belirli zaman dilimlerine göre kısıtlanır.
  - Çalışanlar dışındaki kişilerin erişimi engellenebilir.

## 💡 **Access Control'un Faydaları** 

Erişim kontrolü, organizasyonların güvenliğini artırırken aynı zamanda verimliliği de artırır. İşte erişim kontrolünün sağladığı bazı faydalar:

- 🔒 **Veri Güvenliği**: Hassas veriler yalnızca yetkili kişiler tarafından erişilebilir. Bu, veri sızıntılarını ve hırsızlıklarını önler.
- 🛡️ **Yasal Uyumluluk**: Birçok sektör, belirli erişim kontrollerine uyulmasını zorunlu kılar (örneğin, GDPR, HIPAA). Erişim kontrolü, bu uyumluluğu sağlamak için gereklidir.
- ⚖️ **Risk Azaltma**: Erişim hakları sınırlanarak, potansiyel kötü niyetli aktiviteler engellenir.
- 📈 **Verimli Erişim Yönetimi**: Kullanıcıların ve grupların erişimi yönetmek kolaylaşır, gereksiz erişimler ortadan kaldırılır.
- 👥 **Rol Tabanlı Yönetim**: Kullanıcıların hangi kaynaklara erişebileceği, net bir şekilde belirlenir ve yönetilir.
