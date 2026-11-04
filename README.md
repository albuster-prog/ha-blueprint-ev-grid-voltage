# EV charging by grid voltage – Home Assistant blueprint

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Falbuster-prog%2Fha-blueprint-ev-grid-voltage%2Fblob%2Fmain%2Fev_charging_by_grid_voltage.yaml)

🇷🇴 **Română** · 🇬🇧 [English](#english)

Blueprint care reglează automat curentul de încărcare al mașinii electrice după **tensiunea din rețea** și **puterea absorbită din rețea**. Este util pentru case pe rețele slabe (subtensiune seara, invertor hibrid care se deconectează) și/sau cu limită de putere în ATR.

## Ce face

- Pornește încărcarea automat când conectezi mașina (opțional).
- Urcă curentul pe trepte (ex. 6/8/10/13/16/20 A) doar când tensiunea e stabilă peste prag și importul din rețea rămâne sub limită.
- Coboară o treaptă la tensiune mică sau import peste limită.
- Urgență: rețea căzută sau tensiune foarte mică → curent minim, apoi urcă din nou treaptă cu treaptă.
- Bateria casei (opțional): pornește cu curent mare când bateria e plină și plafonează curentul când bateria scade sub prag.
- Repornește încărcarea dacă încărcătorul intră singur în pauză/eroare (nu îl pornește dacă l-ai oprit tu).
- Acțiuni proprii la conectare/deconectare (ex. setări TOU invertor DEYE) și notificări.

## Instalare

1. Butonul de mai sus **sau** Settings → Automations & Scenes → Blueprints → Import Blueprint, cu linkul fișierului `ev_charging_by_grid_voltage.yaml` din acest repo.
2. Create automation → From blueprint → „EV charging by grid voltage”.
3. Completează entitățile. La **Allowed current steps** pune doar valorile acceptate de încărcătorul tău.
4. Ajustează pragurile după rețeaua ta (implicit: urcare ≥ 218 V / 5 min, coborâre < 205 V, urgență < 198 V, import 4,5 / 4,7 kW).

Testat cu invertor DEYE 8 kW (Solarman), baterie 16 kWh și încărcător Navo 7,4 kW (Tuya).

⚠️ Folosește-l pe propria răspundere; nu înlocuiește protecțiile electrice. Urmărește logbook-ul în primele zile.

---

## English

Automatically adjusts the EV charger current from the **grid voltage** and **grid import power**. Made for homes on a weak grid (evening undervoltage, hybrid inverter disconnecting) and/or with a contracted power limit.

**Features:** auto-start on plug-in (optional) · step up only when voltage is stable above a threshold and import stays under the limit · step down on low voltage / high import · emergency minimum current on grid loss or very low voltage, then step-by-step recovery · optional home battery support (higher start current, cap when SOC is low) · watchdog restart on charger pause/fault · custom actions on connect/disconnect · notifications.

**Install:** use the button above or import `ev_charging_by_grid_voltage.yaml` via Settings → Blueprints → Import Blueprint, then create an automation from it. Use only current steps your charger accepts.

Use at your own risk; it does not replace electrical protection.

License: MIT
