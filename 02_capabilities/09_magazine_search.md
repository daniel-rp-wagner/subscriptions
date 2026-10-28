# Fähigkeit: Nach Zeitschriften suchen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, Zeitschriften nach bestimmten Schlagworten zu finden.

Der Seitenbesucher kann dadurch:

* Zeitschriften nach Themengebieten anzeigen lassen, um eine interessensbasierte Auswahl zu treffen.

## Fachliche Eingabe

Ein Freitext mit maximal 80 Zeichen Länge. Weitere Eingaben (z. B. Zeitschriften-Kategorie oder Anfangsbuchstabe) sind nicht vorgesehen und führen zu einem Validierungsfehler.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher eine Zeitschrift auswählen kann.

Zu jeder Zeitschrift wird bereitgestellt:

* Zeitschrift.Id
* Zeitschrift.Bild
* Zeitschrift.Name

Zu jeder Suche wird berechnet:

* Anzahl der angezeigten Zeitschriften

## Fachliche Regeln

* Nur aktive Zeitschriften werden angezeigt
* Die Anzahl der Zeitschriften wird dynamisch berechnet und ausgegeben
* Die Zeitschriften werden alphabetisch sortiert
* Die Suche folgt den Anforderungen aus REQ-001 (inkl. exaktem Match nach Normalisierung)

## Mögliche fachliche Ergebnisse

| Situation                                       | Fachliches Ergebnis                              |
| ----------------------------------------------- | ------------------------------------------------ |
| Mindestens eine Zeitschrift existiert           | Alle Informationen werden geliefert              |
| Keine Zeitschrift gefunden                      | Leere Ergebnismenge                              |
| Suchanfrage leer oder länger als 80 Zeichen     | Validierungsfehler                               |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte Zeitschriften sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden