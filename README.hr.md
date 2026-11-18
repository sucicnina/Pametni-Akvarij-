[🇬🇧 English](README.md) | 🇭🇷 Hrvatski

# 🐠 Pametni akvarij

**Mikroračunalni sustav za upravljanje i regulaciju uvjeta u akvariju** – projekt iz kolegija *Ugradbeni računalni sustavi* (UgRS), FERIT Osijek, 2026.

Autori: Luka Idžanović, Nina Sučić

Sustav temeljen na mikroračunalu **ESP32** automatski regulira temperaturu vode, simulira dnevni ciklus osvjetljenja, periodički hrani ribe i omogućuje ručno upravljanje crpkom za cirkulaciju vode.

## Funkcionalnosti

- 🌡️ **Regulacija temperature** – senzor DS18B20 očitava temperaturu svake 3 s; ispod zadane vrijednosti (28 °C) relej uključuje H7 žarulju koja služi kao grijač.
- 🛡️ **Filtriranje šuma** – očitanje `-127 °C` (pogreška OneWire komunikacije uzrokovana smetnjama crpke) se odbacuje, a relej zadržava prethodno stanje.
- 💡 **Simulacija sunčevog ciklusa** – WS2812B LED traka postupno pojačava i smanjuje svjetlinu (ciklus od 5 min u demonstracijskom načinu rada).
- 🍽️ **Automatsko hranjenje** – SG90 servo motor periodički otvara dozator hrane.
- 💧 **Ručno upravljanje crpkom** – tipkalo uključuje/isključuje potopnu crpku (s *debounce* zaštitom).

## Komponente

| Komponenta | Namjena |
|---|---|
| ESP32 NodeMCU + Expansion Board | središnje mikroračunalo |
| DS18B20 (vodootporni) | mjerenje temperature (OneWire) |
| H7 žarulja 12 V / 55 W | grijač (radi na 5 V, ≈ 9,6 W) |
| Dvokanalni relejni modul 5 V (*Active LOW*) | upravljanje grijačem i crpkom |
| Potopna crpka 5 V DC | cirkulacija vode |
| SG90 mikro servo | dozator hrane |
| WS2812B LED traka (30 LED) | osvjetljenje |
| Tipkalo | ručna komanda crpke |
| Napajanje 5 V / 10 A + WAGO 221 | distribucija napajanja |

## Spajanje (pinovi ESP32)

| Pin | Komponenta |
|---|---|
| GPIO 13 | WS2812B LED traka (data) |
| GPIO 18 | SG90 servo |
| GPIO 14 | tipkalo (`INPUT_PULLUP`) |
| GPIO 16 | relej – crpka |
| GPIO 2 | relej – žarulja (grijač) |
| GPIO 4 | DS18B20 (data) |

## Pokretanje

1. Instalirati [Arduino IDE](https://www.arduino.cc/en/software) i podršku za ESP32 ploče.
2. Kroz *Library Manager* instalirati biblioteke: `FastLED`, `ESP32Servo`, `OneWire`, `DallasTemperature`.
3. Otvoriti [KOD.txt](KOD.txt) (preimenovati u `.ino` ili zalijepiti u novi sketch), odabrati ESP32 ploču i učitati program.
4. Serijski monitor (115200 baud) prikazuje stanje termostata, hranilice i crpke.
5. git clone https://github.com/sucicnina/Pametni-Akvarij-.git

## Videoprezentacija

🎬 [Pogledaj videoprezentaciju na Google Driveu](https://drive.google.com/file/d/1V9iYCyiI1syzogd-55SNvuv7ObN_iCeJ/view?usp=drivesdk)
