# 🔁 Loop Guard Nedir? – STP Güvenlik Özelliği

## 🎯 Amaç

`Loop Guard`, Spanning Tree Protocol (STP) için geliştirilen bir **gelişmiş koruma mekanizmasıdır**.  
Amaç, bir portun **hatalı olarak forwarding (iletim) moduna geçip ağda Layer 2 döngü (loop) oluşturmasını önlemektir.**

---

## ⚠️ Sorun Ne?

STP normalde portları rollerine göre `root`, `designated`, `blocked` gibi modlara geçirir.  
Ancak bazı durumlarda **BPDU’lar kesilirse** (örneğin fiziksel bağlantı aktif ama BPDU alınamıyor), STP portu **yanlışlıkla aktif duruma geçirir**.

🔌 Bu durumda:  
- İki switch kendini **"root bridge’e en yakın"** sanır.  
- Portlar forwarding olur.  
- Ağda **loop** oluşur.

---

## 🛡️ Loop Guard Ne Yapar?

Loop Guard aktif olan bir port:
- **Uzun süre BPDU almazsa** portu **"err-disable" yapmaz**, ama **"loop inconsistent"** durumuna geçirir.
- Portu **blocking gibi pasif moda alır.**
- BPDU tekrar gelirse, port **otomatik olarak eski haline döner** (self-healing özelliktedir).

---

## 📌 Hangi Durumlarda Kullanılır?

| Kullanım Durumu | Açıklama |
|------------------|----------|
| STP root ve alternate portlar | BPDU almaya bağımlı portlar |
| Büyük Layer 2 ağlar | Fiziksel bağlantılar stabil ama BPDU kesilirse tehlike büyür |
| BPDU kaybı ihtimali olan senaryolar | L2 hataların yayılmasını engeller |

---

## 🔧 Nasıl Uygulanır?

### Interface Modda:

```
SW3(config)# interface e0/2 
SW3(config-if)# spanning-tree guard loop
```

### Global modda:

```
spanning-tree loopguard default
```