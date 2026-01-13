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

## Lizenz

MIT License
