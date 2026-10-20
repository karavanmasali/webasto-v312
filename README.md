# Karavan Webasto V3.13 — V3.12 Tasarımı Korunmuş

Bu sürüm **V3.12 paketinden** hazırlanmıştır. V3.12 renkleri, alt sabit **Kontrol / Geçmiş / Ayarlar** sekmeleri, kart ölçüleri, yerleşim ve mevcut bağlantı/otomatik termostat davranışı korunmuştur. CSS değişiklikleri yalnızca manuel hedef kartı için dosyanın sonuna eklenmiştir.

## Sadece iki özellik eklendi

1. START / STOP eşikleri geniş aralıkta bağımsız; 2 °C minimum mesafede birbirini kaydırır. Örnek START 19, STOP 21 iken START + => 20/22; STOP - => 18/20. Minimum/maximum 10–40 °C sınırları korunur.
2. Manuel kontrol alanında START/STOP **düğmelerinin altında** manuel hedef sıcaklık +/- ayarı (10–40 °C) bulunur. Otomatik STOP değerinden ayrı olarak tarayıcıda kaydedilir. Manuel START öncesinde 3A00 üzerinden cihazdaki hedef geri okunarak doğrulanır; doğrulanmıyorsa komut gönderilmez.

## Korunan yapılar

- V3.12 sabit 3 sekme ve tasarım; uygulama tek sayfada çalışır. Sekme değişimi BLE'yi koparmaz.
- V3.12 Bluetooth Dizi C START, STOP / CLEAR, hedef sıcaklık, otomatik mod hatırlama ve yeniden bağlantı kontrolleri.
- `ble.js`, `auto-engine.mjs`, `protocol.mjs`, `command-profile.mjs`, `activity-log.mjs` dosyaları V3.12 ile aynı.

## Kurulum

ZIP içindeki **14 dosyayı** GitHub deposunun kök dizinine yükle; `index.html` kökte kalmalı. GitHub Pages > Deploy from a branch > `main` / `(root)`.

## Test ve güvenlik

Arayüz ve temel otomatik kontrol testleri tarayıcı demosunda yapılır. Gerçek RE5011 üzerinde bu güncellenmiş sürüm henüz doğrulanmadı. Isıtıcı için fiziksel egzoz, havalandırma ve karbonmonoksit alarmı gereklidir. Bluetooth bağlantısı veya web sayfası çalışmıyorken otomatik kontrol yapılamaz.
