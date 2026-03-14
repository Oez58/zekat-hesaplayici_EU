# ☪ Zekat Hesaplayıcı · Zekat Rechner

> **TR:** Türkiye kökenli Almanya'da yaşayan Müslümanlar için geliştirilmiş, canlı altın ve gümüş fiyatlı zekat hesaplayıcı.
>
> **DE:** Zekat-Rechner für in Deutschland lebende Muslime türkischer Herkunft – mit Live-Gold- und Silberpreisen.

---

## 🌐 Live App

**→ [zekat-hesaplayici\_EU öffnen](https://Oez58.github.io/zekat-hesaplayici_EU)**

---

## 📱 Installation als App (PWA)

**DE:** Die App kann auf Android und iPhone ohne App Store direkt auf dem Homescreen installiert werden.

**TR:** Uygulama, App Store'a gerek kalmadan Android ve iPhone ana ekranına kurulabilir.

### Android
1. Link in **Chrome** öffnen · Linki **Chrome**'da aç
2. Drei Punkte oben rechts → **"Zum Startbildschirm hinzufügen"**
3. Bestätigen → App erscheint als Icon · Onayla → Uygulama ikon olarak görünür

### iPhone (Safari)
1. Link in **Safari** öffnen · Linki **Safari**'de aç
2. Teilen-Symbol unten → **"Zum Home-Bildschirm"**
3. Bestätigen · Onayla

---

## ✨ Funktionen · Özellikler

| Funktion · Özellik | Details |
|---|---|
| 🥇 Altın – Ayar (gram) | 24, 22, 18, 14 Ayar |
| 🪙 Türk Altın Çeşitleri | Çeyrek, Yarım, Tam, Cumhuriyet, Ata, Reşat, Hamit, İkibuçuk, Beşli, Gremse |
| 🥈 Gümüş · Silber | Gram + Takı / Schmuck |
| 💶 Nakit & Banka · Bargeld & Bank | Vadesiz, Vadeli, Diğer |
| 📈 Hisse & Yatırım · Aktien & Investitionen | Hisse, Fon/ETF, Kripto |
| 🏪 Ticari Varlıklar · Geschäftsvermögen | Stok, Alacaklar, Kasa |
| 🔴 Borçlar · Schulden | Otomatik düşülür · Automatisch abgezogen |
| ⚙️ Nisap Standardı | Altın (87.48g) veya Gümüş (612.36g) |
| 📡 Canlı Fiyat · Live-Preis | Otomatik güncelleme · Automatische Aktualisierung |

---

## 📡 Veri Kaynakları · Datenquellen

| Veri · Daten | Kaynak · Quelle |
|---|---|
| Altın & Gümüş · Gold & Silber (USD/Ons) | [api.gold-api.com](https://api.gold-api.com) – ücretsiz, limitsiz |
| EUR/USD Kuru · Kurs | [api.frankfurter.app](https://api.frankfurter.app) – Avrupa Merkez Bankası · Europäische Zentralbank (EZB) |
| EUR/gram hesaplama · Berechnung | `USD/Ons ÷ EUR/USD ÷ 31.1035` |

---

## 🧮 Hesaplama Mantığı · Berechnungslogik

```
Net Servet · Nettovermögen  =  Altın + Gümüş + Nakit + Yatırım + Ticari  −  Borçlar
Zekat                       =  Net Servet × %2.5  (Nisap aşıldığında · wenn Nisab erreicht)
```

**Nisap:**
- **Altın Nisabı:** 87.48g saf altın değeri · Wert von 87.48g Feingold
- **Gümüş Nisabı:** 612.36g gümüş değeri · Wert von 612.36g Silber

---

## 📊 Google Sheets Versiyonu · Version

**DE:** Zusätzlich zur Web-App gibt es eine vollständige Google Sheets Version mit Apps Script für automatische Kurs-Aktualisierung.

**TR:** Web uygulamasına ek olarak, otomatik kur güncellemesi için Apps Script ile tam bir Google Sheets versiyonu mevcuttur.

### Apps Script Kurulumu · Einrichtung
1. Google Sheets'te · In Google Sheets: `Uzantılar → Apps Script`
2. Script kodu yapıştır · Script-Code einfügen
3. `kurulumYap` fonksiyonunu çalıştır · Funktion `kurulumYap` ausführen
4. İzin ver · Berechtigung erteilen

**Otomatik Triggerlar · Automatische Trigger:**
- ✅ Dosya açılışında · Beim Öffnen der Datei
- ✅ Saatlik arka plan · Stündlich im Hintergrund

---

## ⚠️ Önemli Not · Wichtiger Hinweis

**TR:** Bu araç yönlendirme amaçlıdır ve dini bir fetva yerine geçmez. Kesin zekat hesabı için bir din âlimine danışmanız tavsiye edilir.

**DE:** Dieses Tool dient der Orientierung und ersetzt kein religiöses Gutachten. Für eine verbindliche Zekat-Berechnung wird die Beratung durch einen Gelehrten empfohlen.

---

## 🛠️ Teknoloji · Technologie

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **PWA:** Web App Manifest
- **API:** REST/JSON – keine Anmeldung erforderlich · kayıt gerekmez
- **Hosting:** GitHub Pages

---

*Oluşturuldu · Erstellt mit Claude · Anthropic*
