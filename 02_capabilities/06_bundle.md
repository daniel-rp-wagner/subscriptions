# Fähigkeit: Die Informationen zu einem Bündelangebot bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, Informationen zu einem Bündelangebot einzusehen.

Der Seitenbesucher kann dadurch:

* spezielle Angebote erhalten, um eine Zeitschrift auch kurzfristig auszuprobieren.

## Fachliche Eingabe

Zur Identifikation wird eine eindeutige Id des Bündelangebots angegeben.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher das Bündelangebot einsehen kann.

Zu jeder Zeitschrift wird bereitgestellt:

* Zeitschrift.Id
* Zeitschrift.Bild
* Zeitschrift.Name
* Zeitschrift.Kurzbeschreibung
* Zeitschrift.Erscheinungsweise
* Zeitschrift.Einzelpreis
* Zeitschrift.Ausgaben

Zu jedem Bündelangebot wird bereitgestellt:

* Bündelangebot.Id
* Bündelangebot.Laufzeit in Monaten
* Bündelangebot.Ausgaben
* Bündelangebot.Zeitraum
* Bündelangebot.Rabatt für Bankeinzug
* Bündelangebot.Geldwert (leer, wenn keine Geldwert-Prämie zugeordnet ist)

Zur Sachprämie und zur Geldwert-Prämie wird jeweils getrennt bereitgestellt (leer, wenn das Bündelangebot sie nicht enthält):

* Prämie.Id
* Prämie.Bild
* Prämie.Name
* Prämie.Merkmale
* Prämie.Art
* Prämie.Warenwert

Zu jedem Bündelangebot wird berechnet:

* Angebotsausgaben
* Angebotspreis
* Zahlungsrhythmus

## Fachliche Regeln

* Der Angebotspreis berechnet sich nach der Business Rule BR-003; die Angebotsausgaben ergeben sich aus BR-006.
* Je nach Bündelangebot.Zeitraum ist entweder Bündelangebot.Laufzeit in Monaten oder Bündelangebot.Ausgaben gesetzt; das andere Feld ist leer.
* Bündelangebot.Geldwert ist der maßgebliche Geldwert; die referenzierte Geldwert-Prämie liefert Stammdaten, nicht den Betrag.
* Bündelangebot.Name dient der internen Verwaltung und wird nicht ausgegeben.
* Der Zahlungsrhythmus ergibt sich aus der BR-005 (bei Zeitraum „Ausgaben“ einmalig).

## Mögliche fachliche Ergebnisse

| Situation                     | Fachliches Ergebnis                              |
| ----------------------------- | ------------------------------------------------ |
| Bündelangebot existiert       | Alle Informationen werden geliefert              |
| Bündelangebot inaktiv         | Fachlicher Fehler „Bündelangebot nicht gefunden“ |
| Bündelangebot existiert nicht | Fachlicher Fehler „Bündelangebot nicht gefunden“ |

## Fachliche Qualitätsanforderungen

* Geänderte Bündelangebot-Informationen sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden