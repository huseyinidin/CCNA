# Cisco Cihazlarda `service password-encryption` ve `Banner` Komutu

## 🔐 Amaç

Cisco switch ve router'larda kullanıcı parolaları, yapılandırma dosyalarında **varsayılan olarak düz metin (plain text)** şeklinde görünür. Bu, güvenlik açısından büyük bir risk oluşturur.

- `Startup-config` ve `running-config` dosyaları çoğu parolayı düz metin olarak görüntüler.

- Tüm düz metin paroları şifrelemek için `service password-encryption` global config komutunu kullanın.

- `service password-encryption` komutu sayesinde, yapılandırma dosyasında geçen tüm parolalar **temel seviyede şifrelenir**.

- Cihazdaki paroların şifrelenmiş olduklarını teyit etmek için show running-config komutunu kullanın. 

---

## 🧪 Komut Kullanımı

```
Switch(config)# service password-encryption
```
---

## ✅ Neden Kullanılmalı?
    **Avantaj**					**Açıklama**
🔏 Gizlilik sağlar				Parolalar yapılandırma çıktısında gizlenir, gözle okunamaz.
🛡️ Fiziksel erişim riskini azaltır		Yetkisiz kullanıcılar show running-config ile parola göremez.
🧩 Konfigürasyon yedeklerinde güvenlik		Config dosyaları başka sistemlerde saklanırken parola açığa çıkmaz.
💼 Standart güvenlik politikalarına uyum	Ağ güvenliği prosedürlerinde önerilir.

---

# Cisco Cihazlarda Banner Yapılandırması

## 📘 Banner Nedir?

Cisco router ve switch’lerde **banner**, bir kullanıcı cihazla bağlantı kurduğunda karşısına çıkan **metin tabanlı uyarı/karşılama mesajıdır**.  
Genellikle **güvenlik uyarısı** ya da **yetkisiz erişim bildirimi** amacıyla kullanılır.


## 🎯 Kullanım Amaçları

- Güvenlik bildirimi göstermek (örneğin: yetkisiz erişim yasaktır)
- Yasal uyarı mesajı vermek
- Yönetici notu ya da sistem durumu hakkında bilgi vermek

---

## 🔠 Banner Türleri

| Tür       | Açıklama                                  |
|-----------|-------------------------------------------|
| `banner motd`  | "Message of the Day" – en yaygın banner türü |
| `banner login` | Giriş yapmadan önce görünen banner     |
| `banner exec`  | Giriş yaptıktan sonra gösterilen banner |

---

## 🛠 Temel Komut – MOTD Banner

```
Switch(config)# banner motd # Yetkisiz giriş yasaktır! Bu sistem izlenmektedir.#
```
```
banner motd # Yetkisiz giriş yasaktır! Bu sistem izlenmektedir.#
```
