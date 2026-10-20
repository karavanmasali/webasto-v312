# Karavan Webasto V3.12 — Üç Sekmeli Web Kontrolü

Bu paket **V3.11 web sürümünün** üzerine hazırlanmıştır. START / STOP / sıcaklık hedefi için kullanıcı tarafından doğrulanan BLE protokol dosyaları (`ble.js`, `protocol.mjs`, `command-profile.mjs`) ve termostat motorları (`auto-engine.mjs`, `thermostat.mjs`) V3.11 ile **aynıdır**.

## V3.12 yenilikleri

1. `Gerçek Webasto komutlarına izin veriyorum` kutusu ve buna bağlı çift izin engeli kaldırıldı.
2. Otomatik moda **KAPALI → AÇIK** geçişte kullanıcıdan tek kez açık onay istenir. Bağlı değilken de bu tercih onaylanıp kaydedilebilir.
3. Otomatik mod onaylı bir kez açıldıktan sonra sayfa yenilense, Bluetooth bağlantısı kopsa, otomatik START/STOP döngüsü yaşansa veya bağlantı tekrar sağlansa da **AÇIK** saklanır. Sadece kullanıcı otomatik anahtarı kapatırsa tercih kapanır. Manuel START/STOP da otomatiği kapatır.
4. Manuel START/STOP, düğmeye basıldığında ikinci bir onay sorusu olmadan gönderilir. Komut öncesi cihaz ve bağlantı güvenlik denetimleri korunur.
5. Bluetooth kesildiğinde gönderim durur. BLE otomatik tekrar bağlanabiliyorsa denemeleri sürdürür. Tekrar bağlandığında CRC-doğrulanmış *yeni* durum ile mevcut çalışma/kapalı/soğutma durumu değerlendirilir ve otomatik kontrol eski eşiklerden devam eder. **Bağlantı yokken Webasto kontrol edilmez.**
6. Cihaz hata bildirirse otomatik kontrol, kullanıcı tercihinin tikini silmeden **güvenlik duraklatması** durumuna geçer. Sorun giderildikten sonra kullanıcı bilerek yeniden etkinleştirebilir.
7. Bluetooth'u kullanıcı kendisi kapatırsa bile saklı otomatik mod AÇIK kalır; yeniden el ile bağlanınca kontrol devam edebilir.
8. Kontrol / Geçmiş / Ayarlar sekmeleri, olay geçmişi, sıcaklık grafiği ve sessiz bildirim seçeneği korundu.

## GitHub Pages kurulumu

1. GitHub'da `webasto-v312` adlı **Public** yeni depo oluştur.
2. ZIP içindeki 14 dosyayı deponun **ana dizinine** yükle. `index.html` kökte bulunmalı.
3. Settings → Pages → Deploy from a branch → `main` ve `/(root)` → Save.
4. Yayınlandıktan sonra `https://karavanmasali.github.io/webasto-v312/` adresini aç; önce demo, ardından gerçek RE5011 üzerinde gözetimli deneme yap.

## Önemli sınırlamalar

- Web Bluetooth, çoğunlukla masaüstü Chrome/Edge gibi desteklenen tarayıcılarda çalışır. **Yeniden bağlanma** mevcut sayfa açık ve tarayıcı çalışır durumdayken denenir; tarayıcı/sekme kapanınca veya web sitesi yeniden açılınca cihaz seçimi yeniden gerekebilir.
- Ekrandaki otomatik mod tercihi **açık** görünse de gerçek kontrol yalnızca Bluetooth bağlı, veri güncel ve güvenlik kilidi yokken çalışır. Bağlantı koparsa ısıtıcı çalışmaya devam edebilir; telefon/PC uzaktayken otomatik STOP yapılamaz.
- Demo testleri gerçek cihaz davranışını kanıtlamaz. Soğutma ve hatalı bağlanma durumlarını gerçek cihazda ayrıca kontrollü test edin.
- Uygun egzoz, havalandırma ve çalışan CO alarmı olmadan gözetimsiz/gece kullanımına geçmeyin. Bu sürüm cihazın kendi güvenlik mekanizmalarını değiştirmez.
