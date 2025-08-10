# 🔓 **MAC Address Table Attack** 

**MAC Address Table Attack** (MAC adresi tablosu saldırısı), genellikle ağda kullanılan **switch'lerin** zayıflıklarından faydalanan bir tür saldırıdır. Switch'ler, ağdaki cihazları birbirinden ayırt etmek için **MAC adreslerini** kullanır ve her cihazın MAC adresini bir **MAC adresi tablosunda** saklar. Saldırgan, bu tabloyu manipüle ederek switch'i kandırabilir ve ağda yetkisiz erişim sağlayabilir.

## ⚠️ **MAC Address Table Attack Nedir?** 

Switch'ler, veri paketlerini iletmek için MAC adresi tablosunu kullanır. Bu tablodaki her giriş, bir MAC adresinin belirli bir port ile ilişkilendirildiği bilgiyi içerir. MAC Address Table Attack (veya **MAC Flooding**), bu tablonun aşırı yüklenmesini sağlamak amacıyla çok sayıda sahte MAC adresi gönderilmesiyle gerçekleşir. Bu saldırı, switch'in MAC adresi tablosunu doldurarak switch'in tüm portlara broadcast (yayın) yapmasına neden olur.

Bu durumda, switch'in normalde yapması gereken **port yönlendirmeleri** yerine, her paket her porta gönderilir. Bu da, ağı tıkayabilir ve saldırganın ağdaki trafiği izlemesine olanak tanır.

## ⚡ **MAC Address Table Attack Türleri** 

### 1. 🌀 **MAC Flooding**

**MAC Flooding** saldırısında, saldırgan ağdaki switch'e çok sayıda rastgele MAC adresi gönderir. Switch, bu MAC adreslerini kendi adres tablosuna kaydeder. Sonunda, switch'in adres tablosu dolmuş olur ve yeni MAC adresleri için yer kalmaz. Bu durumda, switch, adres tablosu yerine **broadcast** ile her paketi her porta gönderir.

- **Riskler**:
  - **Ağ Tıkanıklığı**: Switch'in broadcast trafiği nedeniyle ağda bant genişliği sorunları oluşabilir.
  - **Veri Erişimi**: Saldırgan, switch'in port yönlendirmelerini tıkayarak tüm trafiği dinleyebilir.

### 2. 🕵️‍♂️ **Man-in-the-Middle (MITM) Saldırıları**
MAC flooding, **Man-in-the-Middle** (MITM) saldırılarına zemin hazırlayabilir. Saldırgan, ağ trafiğini izlemek için kendisini geçerli bir cihaz olarak tanıtabilir. Switch, MAC adreslerini doğru eşleştiremediğinden, paketler saldırgana yönlendirilir.

- **Riskler**:
  - **Veri Sızıntıları**: Saldırgan, ağ üzerinden geçen hassas verileri (şifreler, finansal bilgiler) yakalayabilir.
  - **Veri Manipülasyonu**: Saldırgan, ağdaki verileri değiştirebilir veya sahte veri gönderebilir.

### 3. 🛑 **MAC Spoofing ile İlgili Sorunlar**

Saldırganlar, **MAC Spoofing** kullanarak bir cihazın MAC adresini taklit edebilirler. Bu, bir cihazın ağda kimliğini gizlemesini sağlar ve saldırganın ağdaki verileri izlemesine olanak tanır.

- **Riskler**:
  - **İzinsiz Erişim**: Saldırgan, doğru MAC adresini taklit ederek ağda yetkisiz cihazlara erişebilir.
  - **Ağ Karışıklığı**: Gerçek cihazlar doğru portları bulmakta zorlanabilir.

## 🛡️ **MAC Address Table Attack'tan Korunma Yöntemleri** 

### 1. 🧳 **Port Security Kullanmak**
Switch’lerde **port security** özelliği aktif hale getirilerek, her port için yalnızca belirli bir veya sınırlı sayıda MAC adresine izin verilebilir. Bu, ağdaki her cihazın doğru port üzerinden bağlanmasını sağlar ve sahte MAC adreslerinin ağda görünmesini engeller.

- **Özellikler**:
  - Sadece belirli MAC adreslerinin kabul edilmesi.
  - Fazla sayıda MAC adresi eklendiğinde saldırgan tespit edilir.

### 2. 🔄 **Static MAC Address Assignment**

Switch’ler üzerinde **statik MAC adresleri** atayarak, cihazların yalnızca belirli MAC adresleri ile bağlantı kurmalarını sağlayabilirsiniz. Bu yöntem, **MAC Address Table Flooding** saldırılarını engellemeye yardımcı olur çünkü saldırganın sahte MAC adresi göndermesi mümkün olmaz.

- **Özellikler**:
  - MAC adresleri elle atanır ve değiştirilemez.
  - Dinamik MAC adresleri kullanılmaz, sadece belirli adreslere izin verilir.

### 3. 🔒 **VLAN İzolasyonu Kullanmak**

Ağdaki farklı cihazları izole etmek için **VLAN** (Virtual Local Area Network) kullanmak, bir VLAN'daki cihazların diğer VLAN'larla doğrudan iletişim kurmalarını engeller. Bu, **MAC flooding** saldırısının yalnızca tek bir VLAN ile sınırlı kalmasına neden olur.

- **Özellikler**:
  - Ağ trafiği, farklı VLAN'lara izole edilerek yayılmanın önüne geçilir.
  - VLAN'lar arası erişim kısıtlanır.

### 4. ⚙️ **Switch Configuration'ını Güçlendirmek**

Switch'lerin **configurations** (yapılandırmalarını) gözden geçirerek güvenliği artırmak mümkündür. **BPDU Guard**, **Root Guard** gibi özelliklerle ağdaki yanlış yapılandırmalar ve yetkisiz erişimler engellenebilir.

- **Özellikler**:
  - BPDU (Bridge Protocol Data Unit) Guard, geçerli olmayan BPDU'ları engeller.
  - Root Guard, ağdaki kök bridge'i değiştirecek saldırılara karşı korur.

### 5. 🚪 **Layer 3 Switch'ler ve Router Kullanmak**

Layer 2 switch'lerinin yerine **Layer 3 switch** veya yönlendirici kullanarak, ağda daha güçlü erişim kontrolü sağlanabilir. Bu, ağın daha iyi yönlendirilmesini ve izlenmesini sağlar, böylece Layer 2 saldırılarının etkisi azaltılır.

- **Özellikler**:
  - Layer 3 switch’ler, paketleri Layer 3'e göre yönlendirir ve daha fazla güvenlik sunar.
  - Yönlendiriciler, ağdaki izinsiz erişimi daha etkin şekilde engeller.