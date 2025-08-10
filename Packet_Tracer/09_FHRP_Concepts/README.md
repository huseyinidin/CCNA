# FHRP Concepts (First Hop Redundancy Protocols)

## 📌 FHRP Nedir?

FHRP (First Hop Redundancy Protocols), bir ağda ilk yönlendirici (gateway) arızalandığında, istemcilerin ağ erişimini kaybetmemesi için kullanılan yedeklilik protokolleridir.

Normalde bir istemci (PC, yazıcı, vb.) yalnızca tek bir varsayılan gateway adresi bilir. Eğer bu gateway cihazı arızalanırsa ağ bağlantısı kesilir. İşte FHRP, bu durumu otonom şekilde engeller, böylece ağ erişimi sorunsuz devam eder.

---

## 🧠 Temel FHRP Protokolleri

1. HSRP (Hot Standby Router Protocol)  
   Cisco tarafından geliştirilmiştir. Aktif ve yedek (standby) yönlendirici vardır.

2. VRRP (Virtual Router Redundancy Protocol)  
   Açık standarttır. Farklı üreticilerin cihazları arasında da çalışabilir.

3. GLBP (Gateway Load Balancing Protocol)  
   Cisco'ya özeldir. Hem yedeklilik hem de yük dengeleme sağlar.

---

## 🛠️ FHRP Nasıl Çalışır

- Ağda birden fazla yönlendirici bulunur.
- Bu yönlendiriciler bir sanal IP (virtual IP) ve MAC adresini paylaşır.
- İstemciler yalnızca bu sanal IP'yi gateway olarak kullanır.
- Aktif yönlendirici arızalanırsa, yedek yönlendirici otomatik olarak devreye girer.
- Kullanıcının herhangi bir ayar yapmasına gerek kalmaz.

---

## 🌟 FHRP Özellikleri

 Özellik                      Açıklama                                                                 
------------------------------------------------------------------------------------------------------
 Yüksek Erişilebilirlik      Gateway cihazı bozulduğunda bağlantı devam eder.                        
 Otomatik Geçiş (Failover)   Aktif cihaz arızalanınca yedek cihaz otomatik olarak devreye girer.    
 Sanal IP Kullanımı          Tüm istemciler tek bir IP ile erişim sağlar.                            
 Donanımsal Yedeklilik       Birden fazla routerswitch ile aktif-yedek yapı kurulabilir.            

---

## ✅ FHRP Kullanmanın Avantajları

- ✔ Ağ kesintilerini önler
- ✔ Yedeklilik sayesinde güvenliği artırır
- ✔ Bakım veya cihaz değişiminde kullanıcı etkilenmez
- ✔ VRRP ile çok üreticili ortamlarda esneklik sağlar
- ✔ GLBP ile trafik yükü birden fazla yönlendiriciye paylaştırılabilir

---

## 🎯 Gerçek Hayatta Kullanım Senaryosu

Bir şirket ağı düşünün  
- Varsayılan gateway IP'si `192.168.1.1`  
- Arkada iki yönlendirici var `Router-A` ve `Router-B`  
- Router-A çalışmayı durdurduğunda, Router-B otomatik olarak devreye girer.  
Kullanıcılar hiçbir kesinti yaşamadan internete çıkmaya devam eder.

---
> **Not:** Bu laboratuvar senaryosunda kullanılan tüm konfigürasyon komutlarına erişmek için  
> **`FHRP-IPv4.md`** ve **`FHRP-IPv6.md`** dosyalarına göz atabilirsiniz.
---

