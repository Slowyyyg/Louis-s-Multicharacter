## Louis_Multicharacter

Ein modernes Multicharacter-System für FiveM mit ESX. Charaktere lassen sich über eine integrierte Oberfläche auswählen, erstellen und verwalten – inklusive individuell anpassbarer Vorschau.

## Funktionen

- Charaktere auswählen, erstellen und löschen
- Integrierte Registrierungsoberfläche – keine separate `esx_identity`-Resource erforderlich
- Konfigurierbare Charakter-Slots und Vorschauposition
- Vorschau mit Kamera, Beleuchtung und Idle-Animation
- Unterstützung gängiger Appearance-Ressourcen
- Mehrsprachige Oberfläche

## Voraussetzungen

- FiveM-Server ab Build 7290 mit OneSync
- ESX
- [ox_lib](https://github.com/overextended/ox_lib)
- [oxmysql](https://github.com/overextended/oxmysql)
- Eine unterstützte Appearance-/Skin-Ressource für das Anpassen der Charaktere

## Installation

1. Den Ordner `louis-multicharacter` in den `resources`-Ordner deines Servers kopieren.
2. Sicherstellen, dass ESX, `oxmysql` und `ox_lib` vor dieser Resource gestartet werden.
3. In der `server.cfg` eintragen:

   ```cfg
   ensure oxmysql
   ensure ox_lib
   ensure es_extended
   ensure louis-multicharacter
   ```

4. `config.lua` an Server, Datenbank und gewünschte Appearance-Ressource anpassen.
5. Prüfen, dass die ESX-Datenbank die vom Server verwendeten Charakter- und Skin-Felder enthält.

`esx_identity` nicht zusätzlich starten: Die Registrierung wird von `Louis_Multicharacter` übernommen. Andere ESX-Ressourcen, die nicht zur Identity-Registrierung gehören, bleiben davon unberührt.

## Konfiguration

Die wichtigsten Einstellungen befinden sich in `config.lua`:

| Einstellung | Zweck |
| --- | --- |
| `Config.Lang` | Sprache der Oberfläche (`de`, `en`, `es`, `fr`, `pt`, `tr`, `zh`) |
| `Config.Identifier` | Identifikatortyp passend zur ESX-Datenbank |
| `Config.Prefix` | Präfix der Charakter-Identifier |
| `Config.DefaultSlots` | Standardanzahl der Charakter-Slots |
| `Config.DeleteButton` | Charakter-Löschung in der Oberfläche aktivieren |
| `Config.Coords.Single.pedCoords` | Position und Ausrichtung der Charaktervorschau |
| `Config.CustomizationMenu` | Event zum Öffnen des Appearance-Menüs für neue Charaktere |

Beispiel für einen eigenen Vorschaupunkt:

```lua
Config.Coords = {
    Single = {
        pedCoords = vector4(x, y, z, heading)
    },
    Random = false
}
```

Optionale Community-Links lassen sich unter `Config.Pages.Links` eintragen. Die passenden Icon-Dateien gehören in `web/build/logo/`.

## Relog

Wenn `Config.Relog.Status` aktiviert ist, wird der Befehl aus `Config.Relog.Command` registriert. Standardmäßig ist dies `/relog`. Der Befehl kann abhängig von `Config.Relog.DeadCheck` bei einem toten Charakter gesperrt sein.

## Hinweise

- Vor Änderungen an der Live-Datenbank ein Backup erstellen.
- Appearance-Ressourcen und weitere optionale Integrationen müssen separat installiert und gestartet werden.
- Die Startreihenfolge und Datenbankstruktur können je nach ESX-Version und Server-Setup abweichen.
