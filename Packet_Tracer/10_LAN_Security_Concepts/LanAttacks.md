# 🌐 **LAN Attacks** 

**LAN (Local Area Network)**, sınırlı bir coğrafi alanda, genellikle bir bina veya kampüs içinde, cihazların birbirleriyle iletişim kurduğu bir ağdır. LAN, birçok organizasyonun ve evdeki ağların temelini oluşturur. Ancak, LAN ortamı da çeşitli güvenlik tehditlerine açıktır. Bu yazı, LAN saldırı türlerini, bu saldırıların nasıl işlediğini ve bu tehditlerden korunma yollarını detaylandıracaktır.

## ⚡ **LAN Saldırı Türleri** 🛠️

### 1. 🕵️‍♂️ **Man-in-the-Middle (MITM) Saldırısı**

**Man-in-the-Middle (MITM)** saldırısı, bir saldırganın ağ trafiğine gizlice müdahale etmesini sağlar. Saldırgan, iki cihaz arasındaki iletişimi izler veya manipüle eder. LAN üzerinde, bu saldırı genellikle **ARP Spoofing** veya **DNS Spoofing** gibi tekniklerle yapılır.

- **Riskler**:
  - Verilerin çalınması veya değiştirilmesi (şifreler, kişisel bilgiler).
  - İletişim gizliliğinin ihlali.
  
- **Korunma Yöntemleri**:
  - **HTTPS** kullanarak şifreli bağlantılar oluşturmak.
  - **DNSSEC** ile DNS saldırılarını önlemek.

### 2. 🔄 **Denial of Service (DoS) ve Distributed Denial of Service (DDoS)**

**DoS** ve **DDoS** saldırıları, hedef sistemin hizmet dışı kalmasını sağlamak için ağ trafiği aşırı yüklenir. LAN ortamında, bu tür saldırılar, ağ cihazlarını (switch'ler, yönlendiriciler) tıkayarak, iletişimi engelleyebilir ve tüm ağın çalışmasını zorlaştırabilir.

- **Riskler**:
  - Ağın çökmesi ve sistemlerin çalışmaması.
  - Hizmet kesintileri ve iş sürekliliği kaybı.

- **Korunma Yöntemleri**:
  - **Firewall** ve **Intrusion Detection Systems (IDS)** kullanmak.
  - **Rate Limiting** ve **Traffic Filtering** ile ağ trafiğini denetlemek.

### 3. 🧲 **ARP Spoofing / ARP Poisoning**

**ARP Spoofing**, bir saldırganın sahte ARP (Address Resolution Protocol) mesajları göndererek, ağdaki cihazları kandırmasıdır. Bu saldırıda, saldırgan kendisini ağdaki başka bir cihaz gibi gösterir. ARP Spoofing, genellikle **MITM** saldırılarının temelini oluşturur.

- **Riskler**:
  - Ağdaki veri trafiğini izlemek ve manipüle etmek.
  - **Man-in-the-Middle (MITM)** saldırıları gerçekleştirmek.

- **Korunma Yöntemleri**:
  - **ARP Spoofing Protection** kullanmak.
  - **Static ARP Entries** ile sabit ARP kayıtları oluşturmak.

### 4. 💥 **MAC Flooding**

**MAC Flooding**, saldırganın bir switch'e sahte MAC adresleri göndererek, switch'in MAC adresi tablosunu aşırı yüklemesidir. Bu durumda, switch, normalde yönlendireceği paketleri **broadcast** yapar, yani tüm portlara gönderir. Bu, ağın tıkanmasına ve saldırganın verileri dinlemesine yol açabilir.

- **Riskler**:
  - Ağın performansının düşmesi (bant genişliği tıkanıklığı).
  - Ağ trafiğinin saldırgan tarafından izlenmesi.

- **Korunma Yöntemleri**:
  - **Port Security** kullanarak, her port için sınırlı sayıda MAC adresine izin vermek.
  - **Static MAC Address** yapılandırması yapmak.

### 5. 🔐 **Password Sniffing**

Ağda, **password sniffing** saldırısı, şifrelerin ağ üzerinden geçerken izlenmesini amaçlar. Bu, özellikle şifresiz (plain text) iletişimde ve **HTTP** gibi güvenli olmayan protokollerle yapılır. Saldırgan, ağdaki cihazlar arasındaki iletişimi dinleyerek şifreleri ele geçirebilir.

- **Riskler**:
  - Şifrelerin ele geçirilmesi ve sistemlere izinsiz erişim.
  - Gizli bilgilerin ifşası.

- **Korunma Yöntemleri**:
  - **Encryption** (şifreleme) kullanmak, örneğin **HTTPS** ve **SSH**.
  - **VPN** kullanarak, şifreli tüneller üzerinden iletişim sağlamak.

### 6. 🔄 **VLAN Hopping**

**VLAN Hopping**, bir saldırganın ağda, VLAN'lar arasında geçiş yaparak, farklı ağ bölümlerine erişmesini sağlayan bir saldırıdır. Bu tür bir saldırı, genellikle **Double Tagging** veya **Switch Spoofing** teknikleriyle yapılır.

- **Riskler**:
  - Farklı VLAN'lara izinsiz erişim.
  - Güvenli VLAN'lara müdahale ve veri sızıntısı.

- **Korunma Yöntemleri**:
  - **VLAN Access Control Lists (ACLs)** kullanmak.
  - **Port-based VLANs** ve **Private VLANs** yapılandırmak.

### 7. 🕹️ **Eavesdropping (Dinleme)**

**Eavesdropping**, saldırganın, ağ üzerinden geçen verileri dinleyerek gizli bilgilere erişmesidir. Bu tür saldırılar, **packet sniffing** araçları kullanılarak gerçekleştirilir ve genellikle şifrelenmemiş ağlarda daha etkilidir.

- **Riskler**:
  - Gizli verilerin çalınması (şifreler, kredi kartı bilgileri).
  - Ağ trafiğini izleme ve analiz etme.

- **Korunma Yöntemleri**:
  - **Encryption** kullanmak (VPN, SSL/TLS).
  - **HTTPS** ve **SSH** gibi güvenli protokoller kullanmak.

### 8. 🚨 **DNS Spoofing**

**DNS Spoofing**, saldırganın ağdaki cihazların DNS (Domain Name System) sorgularını yanıltarak, yanlış IP adreslerine yönlendirilmesini sağlamasıdır. Bu saldırı, kullanıcıların sahte web sitelerine yönlendirilmesine neden olabilir.

- **Riskler**:
  - **Phishing** saldırıları (kimlik avı).
  - Kullanıcıların zararlı sitelere yönlendirilmesi.

- **Korunma Yöntemleri**:
  - **DNSSEC** kullanmak.
  - **Secure DNS Servers** kullanmak.

## 🛡️ **LAN Saldırılarına Karşı Alınabilecek Önlemler** 

### 1. **Ağ Trafiğini Şifreleme**
Şifrelenmiş iletişim, ağ trafiğini izlemek isteyen saldırganlara karşı etkili bir savunma sağlar. **HTTPS**, **SSH** ve **VPN** gibi güvenli iletişim protokolleri kullanılmalıdır.

### 2. **Ağ Erişim Kontrolü**
Ağdaki cihazların yalnızca yetkili cihazlarla iletişim kurması sağlanmalıdır. **MAC Address Filtering**, **Port Security**, ve **VLAN yapılandırmaları** ile ağdaki cihazlar denetlenebilir.

### 3. **Güvenlik Duvarı ve IDS/IPS Kullanımı**
**Firewall** ve **Intrusion Detection/Prevention Systems (IDS/IPS)**, ağ trafiğini izler ve şüpheli aktiviteleri engeller. Bu araçlar, DDoS saldırıları ve diğer saldırılara karşı koruma sağlar.

### 4. **Düzenli Yazılım Güncellemeleri**
Ağdaki cihazların güvenlik yamalarının düzenli olarak güncellenmesi, bilinen güvenlik açıklarının giderilmesini sağlar. Bu, LAN saldırılarının etkinliğini azaltır.

### 5. **Ağ İzleme ve Denetleme**
Ağ aktivitelerini düzenli olarak izlemek, olası saldırıları tespit etmek için kritik öneme sahiptir. **SNMP** (Simple Network Management Protocol) ve diğer ağ izleme araçları kullanılarak, ağda anormal aktiviteler fark edilebilir.
