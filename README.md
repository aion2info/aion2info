# mmo-guide

Selbstgebaute Klassen-Guides im Stil der Wowhead-Klassenguides. Statische Seiten ohne Build-Step.

| Guide | Datei | Stand |
|---|---|---|
| Aion 2 – Leveling &amp; Global-Start (klassenübergreifend) | [aion2/leveling/index.html](aion2/leveling/index.html) | Recherche 19.09.2026, vor Global-Release (05.10.2026) |
| Aion 2 – Assassin PvE DPS | [aion2/assassin/index.html](aion2/assassin/index.html) | Skilldaten 15.09.2026 (KR/TW-Client), Meta Juli–Sept 2026 |
| Aion 2 – Ranger PvE DPS | [aion2/ranger/index.html](aion2/ranger/index.html) | Skilldaten 18.09.2026 (questlog.gg-API, korrigiert), Meta Aug–Sept 2026 |
| Aion 2 – Gladiator PvE Bruiser/Off-Tank | [aion2/gladiator/index.html](aion2/gladiator/index.html) | Skilldaten 18.09.2026 (questlog.gg-API, Freischalt-Level bestätigt), Meta Aug–Sept 2026 |
| Aion 2 – Sorcerer PvE Feuer/Wasser-DPS | [aion2/sorcerer/index.html](aion2/sorcerer/index.html) | Skilldaten 19.09.2026 (questlog.gg-API), Meta Juli–Sept 2026 |

## Öffnen

- Doppelklick auf `aion2/leveling/index.html`, `aion2/assassin/index.html`, `aion2/ranger/index.html`, `aion2/gladiator/index.html` bzw. `aion2/sorcerer/index.html` (die Assassin-/Ranger-/Gladiator-/Sorcerer-Guides laden Daten aus `data/…/skills.js`; nur der Leveling-Guide braucht keine Skilldaten), oder
- lokaler Server für saubere Hash-Links:

```bash
python3 -m http.server 8080
```

dann http://localhost:8080/aion2/leveling/, http://localhost:8080/aion2/assassin/, http://localhost:8080/aion2/ranger/, http://localhost:8080/aion2/gladiator/ bzw. http://localhost:8080/aion2/sorcerer/ öffnen.

## Struktur

```
aion2/leveling/index.html      Klassenübergreifender Guide (Reiter: Übersicht · Leveling 1–45 · Skillpunkte & Federn · Ab Level 45 · Alt-Charaktere · Global vs. KR · Quellen), keine Skilldaten nötig
aion2/assassin/index.html      Guide (Reiter: Übersicht · Skills · Leveling · Stigmas · Rotation · Makros · Stats · Quellen)
aion2/ranger/index.html        Guide, gleicher Aufbau, Ranger-Inhalte
aion2/gladiator/index.html     Guide, gleicher Aufbau, Gladiator-Inhalte (Bruiser/Off-Tank-Framing)
aion2/sorcerer/index.html      Guide, gleicher Aufbau, Sorcerer-Inhalte (Feuer/Wasser-Framing)
assets/css/guide.css           Layout, Reiter, Skill-Chips, Quickbar-Mockup (klassenübergreifend)
assets/js/guide.js             Reiter-Routing, Rendering der Skill-Chips aus den Daten, Tooltips (klassenübergreifend)
assets/icons/aion2/assassin/   Skill-Icons Assassin (96 px; raw/ = 256 px Original)
assets/icons/aion2/ranger/     Skill-Icons Ranger (96 px, vollständig)
assets/icons/aion2/gladiator/  Skill-Icons Gladiator (96 px, vollständig)
assets/icons/aion2/sorcerer/   Skill-Icons Sorcerer (96 px, vollständig; raw/ = 256 px Original)
data/aion2/assassin/skills.json  Skilldaten Assassin – Quelle der Wahrheit (Namen, Level, CD, Spezialisierungen, Empfehlungen)
data/aion2/ranger/skills.json    Skilldaten Ranger – gleiches Schema, siehe dortiges meta.notes-Feld für Einschränkungen
data/aion2/gladiator/skills.json Skilldaten Gladiator – gleiches Schema, Freischalt-Level bestätigt (siehe meta.notes)
data/aion2/sorcerer/skills.json  Skilldaten Sorcerer – gleiches Schema, Freischalt-Level unbestätigt (siehe meta.notes)
data/aion2/<klasse>/skills.js    Generierter Wrapper für file://
docs/research/aion2/           Recherche: Quellen, Spielsysteme, Meta, Glossar (assassin-meta.md, ranger-meta.md, gladiator-meta.md, sorcerer-meta.md)
docs/superpowers/specs/        Design-Spezifikationen
scripts/fetch-icons.sh         Icons laden und verkleinern (Aufruf: `bash scripts/fetch-icons.sh <klasse>`)
scripts/sync-data.sh           skills.json → skills.js (Aufruf: `bash scripts/sync-data.sh <klasse>`)
```

## Aktualisieren

1. Daten in `data/aion2/<klasse>/skills.json` ändern.
2. `bash scripts/sync-data.sh <klasse>` ausführen (z. B. `assassin`, `ranger` oder `gladiator`; ohne Argument = `assassin`).
3. Textänderungen direkt in `aion2/<klasse>/index.html`; Skills im Text als `<span class="skill" data-skill="heart-gore"></span>` referenzieren, der Chip (Icon + Name + Tooltip) wird automatisch gerendert.
4. Recherche-Notizen unter `docs/research/aion2/` nachziehen (siehe dortige README).

Skillnamen sind Englisch (offizielle Namen der Spieldaten). Deutsche Namen sind vorläufig, bis die deutsche Lokalisierung mit dem Global-Release (05.10.2026) vorliegt.
