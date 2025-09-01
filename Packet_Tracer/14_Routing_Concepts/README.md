# 🛣️ Routing Concepts (CCNA) 📡

---

## 1. Routing Kavramları
Routing, ağlar arası veri paketlerinin en uygun yoldan iletilmesini sağlar. Router’lar, Layer 3 cihazlar olarak IP tabanlı yönlendirme yapar.

🔑 Temel kavramlar:
- **Router:** Farklı ağları birbirine bağlar.
- **Routing Table:** Hedef IP’ye giden yolları tutar.
- **Statik Routing:** Manuel olarak tanımlanan yollar.
- **Dinamik Routing:** OSPF, EIGRP, RIP gibi protokollerle otomatik yol öğrenimi.
- **Default Route:** Bilinmeyen tüm ağlara gidiş için varsayılan yol.
- **Administrative Distance (AD):** Farklı protokoller arasında güvenilirlik derecesi.
- **Metric:** Aynı protokolde en iyi yolun seçilmesinde kullanılan maliyet değeri.

---

## 🔹 Yol Belirleme Nedir?
- Router’ın paketi kaynaktan hedefe en uygun yoldan iletme işlemidir.  
- Yönlendirme algoritmaları, metrikler kullanarak en iyi yolu belirler.  

---

## 📏 Algoritmalar
- **Distance Vector:** Hedefe olan mesafeyi ve yönleri temel alır (RIP).  
- **Link State:** Ağ topolojisini öğrenir, en kısa yolu hesaplar (OSPF).  
- **Path Vector:** BGP gibi yönlendirme protokollerinde kullanılır, yol politikalarını takip eder.  

---

## 🏆 En İyi Yol ve En Uzun Eşleşme
- **Longest Prefix Match:** Paketin IP adresine en çok uyan rota seçilir.  
- Örnek: Hedef IP 192.168.1.10, tablodaki rotalar:  
- 192.168.0.0/16  
- 192.168.1.0/24 → Seçilen rota /24  

---

## 📦 Paket İletimi
- Router, paketi doğru çıkış arayüzüne yönlendirir.  
- Paket, hedef IP’ye doğru adım adım iletilir.  

---

## 🌐 Uçtan Uca Paket İletimi Protokolleri
- **TCP:** Güvenilir, bağlantılı iletim sağlar.  
- **UDP:** Hızlı, bağlantısız iletim sunar.  
- **ICMP:** Hata ve kontrol mesajlarını iletir.  
- **SCTP:** Çoklu akış ve hata toleransı sağlar.  

---

## ⚙️ Paket İletme Mekanizmaları
- **Process Switching:** Her paket CPU tarafından işlenir, yavaş.  
- **Fast Switching:** İlk paket CPU ile işlenir, sonraki paketler cache’den iletilir.  
- **CEF (Cisco Express Forwarding):** FIB ve adjacency table ile hızlı yönlendirme sağlar.  

---

## 📋 IP Yönlendirme Tablosu
- Hangi IP aralıklarının hangi çıkış arayüzünden veya next-hop’a gideceğini gösterir.  
- Kaynaklar: statik rotalar, dinamik rotalar, varsayılan rota.  

---

## 📝 Statik Rotalar
- Manuel olarak tanımlanır.  
- Örnek: `ip route 192.168.2.0 255.255.255.0 192.168.1.1`  

---

## 🔄 Dinamik Rotalar
- Yönlendirme protokolleri ile öğrenilir: OSPF, EIGRP, RIP, BGP.  
- Ağ değişikliklerine otomatik uyum sağlar.  

---

## 🛑 Varsayılan Rota
- Eşleşmeyen paketler için kullanılır.  
- Örnek: `ip route 0.0.0.0 0.0.0.0 10.1.1.1`  
- İnternet çıkışı gibi senaryolarda kritik rol oynar.  

---