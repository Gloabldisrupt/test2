# Mischwald – hybrides Planspiel für die Hochschullehre

Prototyp einer Web-App für das Modul **M5 Management interner Stakeholder** im MA Nonprofit Management. Rund 20 Studierende arbeiten in fünf Gruppen einen Parcours mit fünf Stationen im Seminarraum ab. An jeder Station lernen sie ein Konzept kennen, lösen eine Präsenzaufgabe am Tisch und treffen eine strategische Entscheidung. Das Modell trägt deren Folgen über sechs Halbjahre weiter.

## Fall

Lernumwelt ist das fiktive **Evangelische Dekanat Lindenau** mit dem Erprobungsraum »Quartierswerkstatt Nordstadt«. Die Studierenden leiten die Stabsstelle »Kirchenentwicklung und Innovation« und sollen die Werkstatt verstetigen, ohne die Ortsgemeinden zu verlieren. Theoretischer Rahmen ist die Mehrebenenperspektive (Nische – Regime – Landschaft) nach Geels, so wie sie Bils, Faix und Hilbrands (2024) auf kirchliche Erprobungsräume anwenden.

| Station | M5-Baustein | Präsenzaufgabe | Konzept |
|---|---|---|---|
| S1 | Personalmanagement | Bindungsgespräch mit Rollenkarte (alternativ: KI spielt die Rolle) | Herzberg, Schlüsselpersonen |
| S2 | Freiwilligenmanagement | Engagement-Landkarte | Strukturwandel des Ehrenamts |
| S3 | Mikropolitik | Bodenaufstellung Einfluss × Haltung | Crozier/Friedberg, Kühl |
| S4 | Internes Rechnungswesen | Kalkulation Deckungslücke und Vollkosten | Voll- vs. Teilkosten, Kennzahlen |
| S5 | Change-Management | Zeitstrahl mit Phasen | MLP-Phasen, Kotter, Ambidextrie |
| F | Synthese im Plenum | Synodenrede | Paradoxien, Bewertungskriterien |

## Bereiche der App

- **Gruppe**: das Spiel auf dem Gerät einer Gruppe, mit Lagebild, Stationsablauf und KI-Gespräch
- **Stationen**: Rotationsplan, Material, Präsenzaufträge, Rollenkarten, Akteursprofile
- **Leinwand**: Live-Vergleich aller Gruppen für den Beamer (Pfaddiagramm, Kennzahlen, Entscheidungsmatrix)
- **Für Lehrende**: Ablauf, Lernziele, Debriefing, Literatur, technische Hinweise

## Technik

Eine einzelne Datei `index.html` mit Vanilla JS, ohne Build-Schritt. Der Spielstand liegt im Browser (`localStorage`).

Als Claude-Artifact nutzt der Prototyp zwei Laufzeitfunktionen:

- `db`: geteilter Spielstand, damit die Leinwand alle Gruppen live zeigt (Collection `gruppen`, Dokumente `g1` bis `g5`)
- `sample`: KI-Gespräch mit den Akteuren und einem Tutor. Das Modell bekommt Fallbeschreibung, Akteursprofil, Stationskonzept und Spielstand mit. Es ist promptgesteuert und kein eigens trainiertes Modell.

Fehlen beide, läuft die App lokal weiter. Die Leinwand zeigt dann Beispieldaten, und das KI-Gespräch wird ausgeblendet.

## Ausbaustufe Netlify und Supabase

1. Hosting der statischen Seite auf Netlify, QR-Codes an den Stationstischen
2. Supabase-Tabellen `sessions` (Seminartermin, Code) und `groups` (Session, Gruppe, Spielstand als JSON); Realtime-Abo für die Leinwand
3. Netlify Function als Proxy zur Claude API mit Hochschul-Schlüssel, damit Studierende kein eigenes Konto brauchen
4. Optional: Admin-Ansicht für Lehrende (Sessions anlegen, Gruppen zurücksetzen, Export der Protokolle)

Die Modell-Logik (Abschnitt 2 im Skript) ist DOM-frei und lässt sich unverändert übernehmen.

Siehe auch [`docs/leitfaden.md`](docs/leitfaden.md).
