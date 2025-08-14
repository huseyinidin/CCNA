---

1\. DHCP Snooping Aktif Etme

---



```

ip dhcp snooping                         # DHCP Snooping genel olarak aktif edilir

ip dhcp snooping vlan 10,20              # Sadece VLAN 10 ve 20’de aktif

```

---

2\. Trusted/Untrusted Port Ayarı

---



```

interface FastEthernet0/1

ip dhcp snooping trust                  # DHCP sunucusunun bağlı olduğu port güvenilir

interface range FastEthernet0/2 - 10

ip dhcp snooping limit rate 10          # Client portları untrusted, hız sınırı 10 paket/s

```

---

3\. Binding Tablosu Görüntüleme

---

```

show ip dhcp snooping                     # DHCP Snooping genel durumu

show ip dhcp snooping binding             # MAC-IP-VLAN eşleşmelerini gösterir

```

---



Açıklamalar:



```

ip dhcp snooping                 -> Switch üzerinde DHCP Snooping aktif eder

ip dhcp snooping vlan <vlan>     -> Belirli VLAN’larda aktif eder

ip dhcp snooping trust           -> Portu trusted yapar, DHCP sunucu bağlanabilir

ip dhcp snooping limit rate <x>  -> Untrusted portlarda saniye başına paket limiti



show ip dhcp snooping             -> Genel durumu kontrol eder

show ip dhcp snooping binding     -> Öğrenilen MAC-IP-VLAN tablolarını gösterir

```

