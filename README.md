# Basit Log Analiz ve Uyarı Sistemi

Bu proje, "Linux sistemlerinde başarısız giriş denemelerini" takip etmek için hazırlanmış basit bir Python scriptidir. Özellikle SSH üzerinden yapılan hatalı girişler (ör. *Failed password*, *Invalid user*) log dosyalarında yakalanır ve belirlenen eşik değerini aşan IP adresleri için uyarı verilir.

## Özellikler
- Belirli log dosyasını satır satır okur (örn: `/var/log/auth.log`).
- SSH başarısız giriş denemelerini tespit eder.
- IP adreslerini çıkarır ve tekrar sayılarını tutar.
- Belirlenen zaman penceresi içinde aynı IP’den gelen hatalar eşiği aşarsa uyarı üretir.

## Kullanım

1. Script’i terminalden şu şekilde çalıştırabilirsin:

```bash
python3 kisa_log_uyari.py <log_dosyasi> <dakika_penceresi> <esik>
