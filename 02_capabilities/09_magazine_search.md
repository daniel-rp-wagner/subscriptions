# Fähigkeit: Nach Zeitschriften suchen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, Zeitschriften anhand ihres Namens und ihrer zugeordneten Schlagworte zu finden.

Der Seitenbesucher kann dadurch:

* Zeitschriften nach ihrem Namen oder nach Themengebieten finden, um eine passende Auswahl zu treffen.

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
* Die Suche folgt REQ-001: Ein Treffer setzt die vollständige Übereinstimmung eines normalisierten Suchbegriffs mit einem normalisierten Wort aus Zeitschrift.Name oder einem zugeordneten Schlagwort voraus. Teilstring-Treffer sind ausgeschlossen.

## Mögliche fachliche Ergebnisse

| Situation                                       | Fachliches Ergebnis                              |
| ----------------------------------------------- | ------------------------------------------------ |
| Mindestens eine Zeitschrift existiert           | Alle Informationen werden geliefert              |
| Keine Zeitschrift gefunden                      | Leere Ergebnismenge                              |
| Suchanfrage leer oder länger als 80 Zeichen     | Validierungsfehler                               |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte Zeitschriften sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden
