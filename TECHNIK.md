# 🔧 Zekat Hesaplayıcı – Technik-Dokumentation

**Live-URL:** https://Oez58.github.io/zekat-hesaplayici_EU

Diese Doku beschreibt die technische Funktionsweise für Debugging, Fehleranalyse und zukünftige Änderungen. Sie ist bewusst kompakt gehalten: nur was man braucht, um das System zu verstehen, ohne den gesamten Quellcode lesen zu müssen.

---

## 1. Aufbau

```
index.html (einzelne Datei, ~771 Zeilen)
├── HTML  → Eingabefelder, Karten, Layout
├── CSS   → Dark Theme, Responsive Design
└── JS    → API-Aufrufe + Berechnungslogik
```

- **Kein Framework, kein Build-Prozess, keine Abhängigkeiten**
- **Hosting:** GitHub Pages (statisch)
- **Kein localStorage:** Eingaben gehen beim Neuladen verloren

---

## 2. Datenquellen (APIs)

| Daten | Endpoint | Antwort |
|---|---|---|
| Gold USD/Ons | `https://api.gold-api.com/price/XAU` | `{ "price": 4176.10 }` |
| Silber USD/Ons | `https://api.gold-api.com/price/XAG` | `{ "price": 62.51 }` |
| EUR/USD-Kurs | `https://api.frankfurter.dev/v1/latest?from=USD&to=EUR` | `{ "rates": { "EUR": 0.8735 } }` |

**Wichtige Details:**
- Frankfurter liefert USD→EUR (z. B. 0.87). Code rechnet mit `1 / rate` auf EUR→USD um.
- Alle drei Calls laufen parallel via `Promise.all`.
- Schlägt ein Call fehl, schlägt alles fehl → Status-Dot wird rot, "Bağlantı hatası".
- Auto-Refresh alle 60 Minuten via `setInterval`.

---

## 3. Berechnungsformeln

**Gram-Preis:**
```
eurUsd     = 1 / fxData.rates.EUR
goldEurG   = goldUSD   / eurUsd / 31.1035
silverEurG = silverUSD / eurUsd / 31.1035
```
*(1 Troy-Ons = 31.1035g)*

**Ayar-Altın (Gram-Eingabe):**
```
ayar = (a24×1 + a22×(22/24) + a18×(18/24) + a14×(14/24)) × goldEurG
```

**Türkische Münzen (Stück-Eingabe → Reingold-Gewicht):**
```
coins = (ceyrek×1.75 + yarim×3.5 + tam×7 +
        cumhuriyet×7.216 + ata×7.216 + resat×7.216 + hamit×7.216 +
        ikibucuk×17.54 + besli×35.08 + gremse×1) × goldEurG
```

**Gesamtvermögen:**
```
brut = goldTotal + silver + cash + invest + business
net  = max(0, brut - schulden)
```

**Nisap-Prüfung:**
```
nisap = (typ == "gold") ? 87.48 × goldEurG : 612.36 × silverEurG
farz  = (net >= nisap && nisap > 0)
zekat = farz ? net × 0.025 : 0
```

---

## 4. HTML-Element-IDs

Schnellreferenz für Debugging oder neue Felder:

| Kategorie | IDs |
|---|---|
| Ayar-Altın | `a24`, `a22`, `a18`, `a14` |
| Türk-Münzen | `ceyrek`, `yarim`, `tam`, `cumhuriyet`, `ata`, `resat`, `hamit`, `ikibucuk`, `besli`, `gremse` |
| Silber | `silver`, `jewelry` |
| Bargeld | `cash`, `bank1`, `bank2`, `bank3` |
| Investition | `stocks`, `funds`, `crypto`, `invest` |
| Geschäft | `biz1`, `biz2`, `biz3` |
| Schulden | `debt1`, `debt2`, `debt3`, `debt4` |
| Nisap-Auswahl | `nisapSelect` (`gold` / `silver`) |
| Status-Anzeige | `statusDot`, `lastUpdate`, `goldGramDisplay`, `silverGramDisplay`, `eurUsdDisplay` |
| Buttons | `refreshBtn` (→ `fetchPrices()`), Reset-Button (→ `resetAll()`) |

---

## 5. Bekannte Schwachstellen

| # | Schwachstelle | Auswirkung |
|---|---|---|
| 1 | Kein localStorage | Eingaben verloren bei F5 / App-Neustart |
| 2 | Kein Offline-Modus | Ohne Internet keine Preise, keine Berechnung |
| 3 | Minimale Eingabevalidierung | Negativwerte über HTML `min="0"` blockiert, aber keine JS-Prüfung |
| 4 | Nur EUR | Keine andere Währung möglich |
| 5 | Kein Rate-Limit-Feedback | Wenn gold-api.com drosselt → stilles "Bağlantı hatası" |

---

## 6. Versionsverlauf (Doku-spezifisch)

| Version | Datum | Änderung Doku |
|---|---|---|
| 1.1.0 | 2026-07-05 | Frankfurter-Endpoint `.app`→`.dev` korrigiert nach Domain-Wechsel |
| 1.0.0 | initial | Erstellung der Doku |

*Code-Änderungen siehe README.md → Versionsverlauf*

---

## 7. Wartungs-Hinweise für die AI

Wenn Code geändert wird, diese Doku **mit** aktualisieren:
- Neue API oder Endpoint? → Abschnitt 2 aktualisieren
- Neue Formel oder Logik? → Abschnitt 3 aktualisieren
- Neue HTML-ID hinzugefügt? → Abschnitt 4 ergänzen
- Neue Schwachstelle entdeckt? → Abschnitt 5 ergänzen
- Bei jeder Doku-Änderung → Abschnitt 6 mit Version + Datum ergänzen

**Faustregel:** Doku und Code müssen immer denselben Stand haben. Veraltete Doku ist schlimmer als keine.
