# Fähigkeit: Zeitschriften-Kategorien bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, alle Zeitschriften-Kategorien einzusehen.

Der Seitenbesucher kann dadurch:

* sich einen Überblick über alle Kategorien verschaffen
* eine Auswahl nach Kategorie treffen
* alle zur Verfügung stehenden Zeitschriften einer Kategorie einsehen

## Fachliche Eingabe

Keine

## Fachliches Ergebnis

Die Fähigkeit liefert alle Zeitschriften-Kategorien

Zu jeder Zeitschriften-Kategorie wird bereitgestellt:

* Zeitschriften-Kategorie.Id
* Zeitschriften-Kategorie.Name
* Zeitschriften-Kategorie.Reihenfolge

## Fachliche Regeln

* Die Zeitschriften-Kategorien werden nach Zeitschriften-Kategorie.Reihenfolge sortiert. Der niedrigste Wert kommt zuerst; bei gleicher Reihenfolge wird alphabetisch nach Zeitschriften-Kategorie.Name sortiert, danach nach Zeitschriften-Kategorie.Id.

## Mögliche fachliche Ergebnisse

| Situation                                | Fachliches Ergebnis                 |
| ---------------------------------------- | ----------------------------------- |
| Zeitschriften-Kategorien existieren      | Alle Informationen werden geliefert |
| Keine Zeitschriften-Kategorien vorhanden | Leere Ergebnismenge                 |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte Zeitschriften-Kategorien sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden