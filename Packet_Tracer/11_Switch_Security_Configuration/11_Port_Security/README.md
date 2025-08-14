\# 🔒 Port Security



\## 1. Tanım



Port Security, \*\*switch portlarının güvenliğini artırmak\*\* için kullanılan bir mekanizmadır. Bu özellik sayesinde \*\*yalnızca yetkili cihazlar\*\* ağa bağlanabilir.



---



\## 🎯 2. Amaç

\- \*\*Yetkisiz cihazların bağlanmasını önlemek\*\*

\- \*\*MAC Flooding saldırılarını engellemek\*\*

\- \*\*Fiziksel port güvenliğini artırmak\*\*



---



\## 🔧 3. Çalışma Mantığı

1\. Port Security aktif edilir.

2\. Switch portu yalnızca \*\*tanımlı MAC adreslerinden gelen trafiğe izin verir\*\*.

3\. Tanımlı sınır aşılırsa, \*\*violation mode\*\* devreye girer.



---

**## 🚨 4. Violation Modları**

**| Mod      | Açıklama |**

**|----------|----------|**

**| \*\*Protect\*\* | Tanımsız MAC adreslerinden gelen trafik \*\*drop edilir\*\*, port çalışmaya devam eder |**

**| \*\*Restrict\*\* | Tanımsız MAC adresleri \*\*drop edilir\*\* ve \*\*log kaydı tutulur\*\* |**

**| \*\*Shutdown\*\* | Tanımsız MAC adresi görülürse port \*\*err-disabled (kapalı) duruma geçer)\*\* |**



**> \*\*Not:\*\* Varsayılan mod \*\*Shutdown\*\*’dır.**



**---**



\## 🧠 5. MAC Adresi Öğrenme Yöntemleri

\- \*\*Statik:\*\* MAC adresini manuel ekleme

\- \*\*Dinamik:\*\* Cihaz bağlandığında otomatik öğrenme (RAM’de saklanır, reboot sonrası silinir)

\- \*\*Sticky:\*\* Dinamik öğrenilen MAC adreslerini \*\*startup-config\*\*’e kaydeder, reboot sonrası da saklanır



---



\## 🌟 6. Avantajları

\- Fiziksel erişimi \*\*sınırlar\*\*

\- \*\*Basit ve hızlı güvenlik\*\* sağlar

\- VLAN ataması ile birlikte kullanılabilir



---



\## 🏢 7. Kullanım Alanları

\- \*\*Kurumsal ağlar\*\*

\- \*\*Misafir ağ erişim kısıtlaması\*\*

\- \*\*IoT cihaz portları\*\*



---





