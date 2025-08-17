---

## 3️⃣ Native VLAN’ı Değiştirme

Varsayılan Native VLAN olan VLAN 1’i kullanmak güvenlik riskidir. Farklı bir VLAN kullanarak VLAN Hopping saldırılarını zorlaştırabilirsiniz.

```
Switch(config)# interface Gig 0/1
Switch(config-if)# switchport trunk native vlan 100

```

⚠️ ** Native VLAN olarak atanan VLAN’da aktif cihaz bulunmamasına dikkat edin.**

---

