# 💾 Cisco Cihazlarda Yapılandırma Dosyalarını Kaydetme

Cisco cihazlarda yapılan yapılandırmalar, cihaz yeniden başlatıldığında kaybolmaması için **kalıcı belleğe (NVRAM)** kaydedilmelidir. Bu işlem, geçici konfigürasyonun kalıcı hale getirilmesini sağlar.

## 🔄 Çalışma Mantığı

Cisco cihazlarda iki tür yapılandırma vardır:

| Tür                  | Açıklama                            | Bellek Türü |
|----------------------|-------------------------------------|-------------|
| Running Configuration | Anlık olarak çalışan yapılandırma  | RAM         |
| Startup Configuration | Cihaz açıldığında yüklenen yapılandırma | NVRAM     |

## 💡 Yapılandırmayı Kaydetme Komutları

### 1. `copy running-config startup-config`

Anlık yapılandırmayı kalıcı hale getirir:

```
SW1# copy running-config startup-config
Destination filename [startup-config]?  (Enter tuşuna bas)
```