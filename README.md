# Home Assistant Blueprints

Sammlung von Home Assistant Blueprints für Automatisierungen.

## Installation

### Methode 1: Import via URL
1. Gehe zu **Einstellungen → Automatisierungen & Szenen → Blueprints**
2. Klicke auf **Blueprint importieren**
3. Füge die URL des gewünschten Blueprints ein

### Methode 2: Manuell
1. Kopiere die YAML-Datei in deinen `config/blueprints/automation/` Ordner
2. Starte Home Assistant neu

---

## Blueprints

### Motion Time-of-Day Scenes with Override

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/hoizi89/ha-blueprints/blob/main/automation/motion_time_of_day_scenes.yaml)

**Datei:** `automation/motion_time_of_day_scenes.yaml`

Schaltet je nach Tageszeit unterschiedliche Szenen per Bewegungsmelder.

#### Features:
- 4 Tageszeit-Szenen (Morgen, Tag, Abend, Nacht) - alle optional
- Override-Schalter für helle Arbeitsszene (Wandschalter/Shelly)
- Optionale Helligkeitsprüfung (nur bei Dunkelheit aktivieren)
- Konfigurierbare Ausschaltverzögerung
- Sanfte Übergänge mit einstellbarer Transition-Zeit

#### Funktionsweise:
1. **Bewegung erkannt** → Szene passend zur Tageszeit wird aktiviert
2. **Bewegung weg** → Nach konfigurierbarer Verzögerung wird das Licht ausgeschaltet
3. **Override-Schalter EIN** → Helle Override-Szene wird aktiviert (Motion wird ignoriert)
4. **Override-Schalter AUS** → Licht wird ausgeschaltet, Motion-Automatik übernimmt wieder

#### Beispiel: Büro

| Tageszeit | Szene | Beschreibung |
|-----------|-------|--------------|
| Morgen (06:00-09:00) | Büro Morgen | Warmes, gedimmtes Licht |
| Tag (09:00-17:00) | - | Kein Licht (hell genug) |
| Abend (17:00-22:00) | Büro Abend | Warmes Arbeitslicht |
| Nacht (22:00-06:00) | Büro Nacht | Sehr gedimmt |
| Override | Büro Hell | Volle Helligkeit für konzentriertes Arbeiten |

---

### Geräte-PV-Start (Fast / Optimal)

[![Import Blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://github.com/hoizi89/ha-blueprints/blob/master/automation/device_pv_start.yaml)

**Datei:** `automation/device_pv_start.yaml`

> ⚠️ **Beta / lightly tested** – vor produktivem Einsatz selbst prüfen.

Startet ein Haushaltsgerät (Geschirrspüler, Waschmaschine …) bei verfügbarer PV-Überschussleistung. Die geräteabhängige Start-Sequenz wird als Aktion übergeben – damit passt eine Vorlage für beliebige Geräte.

#### Features:
- Zwei Modi über einen `input_select`-Helfer: **Fast** und **Optimal**
- **Fast:** Start ab der Fast-Schwelle, spätestens zur Garantie-Uhrzeit
- **Optimal:** wartet auf hohe PV-Leistung + Mindest-Ladestand; nach dem Tages-Peak abgestufte Fallbacks
- Sicherheitsnetz: Start spätestens bei Sonnenuntergang
- Optionale Aktionen bei Aktivierung/Deaktivierung (z. B. Steckdose trennen/freigeben)
- Alle Schwellen und Zeiten konfigurierbar

#### Voraussetzung:
Ein `input_select`-Helfer mit exakt den Optionen **Aus**, **Fast**, **Optimal**.

#### Funktionsweise:
1. **PV-Modus auf Fast/Optimal** → Automatik aktiv (optionale Aktivierungs-Aktion)
2. **Genug PV-Leistung** (modusabhängig) → Start-Aktion läuft, Modus springt auf „Aus"
3. **Sonnenuntergang** → Start in jedem Fall (Timeout-Sicherung)
4. **PV-Modus zurück auf Aus** → optionale Deaktivierungs-Aktion

In allen Aktions-Eingaben verfügbar: `reason`, `mode`, `pv_now`, `soc_now`.

---

## Lizenz

MIT License
