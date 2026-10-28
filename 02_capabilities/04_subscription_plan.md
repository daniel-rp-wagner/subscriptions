# Fähigkeit: Alle verfügbaren Abonnement-Formen bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, einen Überblick über alle möglichen Abonnement-Formen zu erhalten.

Der Seitenbesucher kann dadurch:

* die passende Laufzeit für sein persönliches Abonnement auswählen
* Abonnements verschenken
* Eine weitere Person werben und eine Prämie als Belohnung erhalten

## Fachliche Eingabe

Keine

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher die Auswahl treffen kann, welche Abonnement-Form er wählen kann.

Zu jeder Abonnement-Form wird bereitgestellt:

* Abonnement-Form.Id
* Abonnement-Form.Name
* Abonnement-Form.Kurzbeschreibung
* Abonnement-Form.Langbeschreibung
* Abonnement-Form.Variante
* Abonnement-Form.Rabatt

Zu jeder Abonnement-Form wird berechnet:

* Angebotsform

## Fachliche Regeln

* Die Abonnement-Formen sind nach Abonnement-Form.Reihenfolge sortiert. Der niedrigste Wert kommt zuerst; bei gleicher Reihenfolge wird alphabetisch nach Abonnement-Form.Name sortiert, danach nach Abonnement-Form.Id
* Es werden nur Abonnement-Formen ausgegeben, die Abonnement-Form.Aktiv = Ja haben
* Die Angebotsform ist „rabattbasiert“, wenn Abonnement-Form.Rabatt > 0, ansonsten „prämienpflichtig“

## Mögliche fachliche Ergebnisse

| Situation                         | Fachliches Ergebnis                 |
| --------------------------------- | ----------------------------------- |
| Abonnement-Formen existieren      | Alle Informationen werden geliefert |
| Keine Abonnement-Formen vorhanden | Leere Ergebnismenge                 |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte und geänderte Abonnement-Formen sollen zeitnah sichtbar sein.
* Die Antwort soll performant bereitgestellt werden