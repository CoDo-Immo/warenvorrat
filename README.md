# Warenvorrat Adlemsried

Eine kleine Web-App zum Verwalten unseres privaten Warenvorrats. Sie zeigt alle eingelagerten Produkte, lässt sich nach Typ und Jahr filtern und läuft auf Android, Apple und Windows – direkt im Browser, ohne Installation.

## Funktionen

- Alphabetische Liste aller eingelagerten Produkte mit Buchstaben-Gliederung
- Filter nach Typ und Einlagerungsjahr sowie ein Suchfeld
- Typen mit Icon dargestellt: 🥕 Gemüse · 🍎 Früchte · 🧀 Milchprodukte · 🌾 Trockenprodukte · 🍲 Gerichte
- Einträge erfassen, bearbeiten, duplizieren und löschen
- Abbuchen einzelner Mengen beim Verbrauchen (Standard 1, anpassbar bis zum vorhandenen Bestand)
- Installierbar als App (eigenes Icon, Einmachglas) auf Handy und Desktop, offline-startfähig
- Design in Lavendel-Tönen

## Datenmodell

Ein Eintrag entspricht einer konkreten Einlagerung. Vom gleichen Produkt kann es mehrere Einträge geben (z.B. gefroren und eingemacht).

| Feld | Bedeutung |
|------|-----------|
| `produkt` | Name des Produkts |
| `typ` | Gemüse / Früchte / Milchprodukte / Trockenprodukte / Gerichte |
| `form` | getrocknet / gefroren / eingekellert / eingemacht |
| `jahr` | Einlagerungsjahr |
| `menge` | Anzahl (optional) |
| `einheit` | kg, Gläser (gross/klein), Gefäss (gross/klein/mini), Beutel (gross/klein), Stück, Liter, Flaschen, Portionen |
| `notiz` | Freitext (optional) |
| `erstellt_am` | Zeitstempel, automatisch |

## Technik

- Eine einzige `index.html` (HTML, CSS, JavaScript) – keine Build-Schritte
- Daten in [Supabase](https://supabase.com) (PostgreSQL), Zugriff über die Supabase-JS-Bibliothek
- Veröffentlicht über GitHub Pages

## Dateien

| Datei | Zweck |
|-------|-------|
| `index.html` | Die App |
| `sw.js` | Service Worker – macht die App installierbar und offline-startfähig |
| `manifest.json` | App-Metadaten für «Zum Startbildschirm hinzufügen» |
| `icon.svg`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`, `favicon-32.png` | App-Icon (Einmachglas) |
| `supabase_setup.sql` | Legt die Datenbank-Tabelle in Supabase an (nur einmal nötig, **nicht** auf GitHub laden) |
| `ANLEITUNG.md` | Schritt-für-Schritt-Einrichtung von Supabase und GitHub |

## Einrichtung

Die vollständige Anleitung steht in [`ANLEITUNG.md`](ANLEITUNG.md). Kurz:

1. In Supabase ein Projekt anlegen und `supabase_setup.sql` im SQL-Editor ausführen.
2. In `index.html` oben die beiden Werte `SUPABASE_URL` und `SUPABASE_ANON_KEY` eintragen.
3. Alle App-Dateien ins GitHub-Repository laden und GitHub Pages aktivieren.

Ohne eingetragene Supabase-Werte startet die App in einem Demo-Modus mit Beispieldaten.

## Hinweis zur Sicherheit

Der `anon`/Publishable-Key steht im veröffentlichten Code – bei Supabase vorgesehen und in Kombination mit Row Level Security unbedenklich. Wer die App-Adresse kennt, kann jedoch Einträge lesen und ändern. Für einen privaten Familien-Vorrat ist das in der Regel ausreichend.

---

Privates Projekt · nicht zur Weitergabe bestimmt.
