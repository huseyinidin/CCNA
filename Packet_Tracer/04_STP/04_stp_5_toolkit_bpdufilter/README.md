# 🚫 BPDU Filter Nedir?

**BPDU Filter**, bir switch portunun **BPDU mesajlarını göndermesini veya almasını engelleyen** bir Spanning Tree özelliğidir.
Yani bu özellik aktif edildiğinde, o port artık STP protokol mesajlarını **göndermez** ve **gelen mesajlara da tepki vermez.**

## 🧠 **Ne İşe Yarar?**

- Portun **Spanning Tree protokolünden bağımsız** kalmasını sağlar.
- Genellikle uç cihazların bağlandığı portlarda, test/lab ortamlarında ya da özel topolojilerde kullanılır.
- STP’in çalışmasını **geçici veya kalıcı olarak engellemek** için kullanılır.

## ⚙️ **Kullanım Komutları**

### 🔹 Arayüz (interface) bazlı yapılandırma

```
Switch(config)# interface fastethernet0/1
Switch(config-if)# spanning-tree bpdufilter enable
```

```
interface fastethernet0/1
spanning-tree bpdufilter enable
```
---

## 🔹 Global Yapılandırma (PortFast ile Birlikte)

BPDU Filter’ı tüm erişim portlarında otomatik olarak etkinleştirmek için aşağıdaki komutlar kullanılır:

```
Switch(config)# spanning-tree portfast default		
Switch(config)# spanning-tree bpdufilter default

```

```

spanning-tree portfast default		!Tüm access (erişim) portlarında PortFast özelliğini otomatik olarak etkinleştirir.
spanning-tree bpdufilter default	!Tüm PortFast etkin portlarda BPDU Filter'ı otomatik olarak devreye sokar.
					!Bu portlar BPDU göndermez.
					!Eğer BPDU algılanırsa, PortFast devreden çıkar ve STP normal çalışmaya döner.

```

