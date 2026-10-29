# Fähigkeit: Prämien zu einer Zeitschrift / Abonnement-Form-Kombination bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, aus allen verfügbaren Prämien auszuwählen.

Der Seitenbesucher kann dadurch:

* sich die Prämien nach Kategorie geordnet anschauen
* Details zum Wert und zum eventuellen Prämienbetrag einsehen
* Eine Prämie zu seiner Abonnement-Kombination auswählen

## Fachliche Eingabe

Zur Identifikation wird eine Zeitschrift sowie die Abonnement-Form angegeben.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher die Auswahl treffen kann, welche Prämie er wählen kann.

* Zeitschrift.Id
* Zeitschrift.Bild
* Zeitschrift.Name
* Zeitschrift.Erscheinungsweise
* Zeitschrift.Einzelpreis
* Zeitschrift.Ausgaben
* Abonnement-Form.Id
* Abonnement-Form.Name
* Abonnement-Form.Variante
* Abonnement-Form.Mindestlaufzeit
* Abonnement-Form.Rabatt
* Abonnement-Form.Rabatt für Bankeinzug
* Angebotsausgaben

Zu jeder Prämie wird bereitgestellt:

* Prämie.Id
* Prämie.Bild
* Prämie.Name
* Prämie.Merkmale
* Prämie.Art
* Prämie.Warenwert
* Prämienbetrag.Geldwert
* Prämienbetrag.Zuzahlung

## Fachliche Regeln

* Nur aktive Prämien werden berücksichtigt
* Eine Prämie wird nur geliefert, wenn sie der Abonnement-Form zugeordnet ist und für die ermittelte Prämienbetragskategorie ein Prämienbetrag existiert
* Bei prämienpflichtigen Abonnement-Formen wird die Prämienbetragskategorie aus der Kombination Zeitschrift × Abonnement-Form ermittelt; fehlt die Zuordnung, ist die Kombination ungültig. Die Prämienbetragskategorie ist eine interne Kalkulationsgruppe und wird nicht ausgegeben
* Die Kombination ist ebenfalls unbekannt, wenn die Zeitschrift oder die Abonnement-Form inaktiv oder unbekannt ist oder die Abonnement-Form der Zeitschrift nicht zugewiesen ist
* Die Prämien werden nach Prämien-Kategorie gruppiert ausgegeben. Eine Prämie, die mehreren Prämien-Kategorien zugeordnet ist, erscheint in jeder dieser Gruppen. Eine Prämie ohne Prämien-Kategorie wird nicht ausgegeben
* Bei einer rabattbasierten Abonnement-Form (Abonnement-Form.Rabatt > 0) werden keine Prämien ausgegeben, da dort keine Hauptprämie gewählt werden darf. Bei diesen Kombinationen darf die Prämienbetragskategorie fehlen; dies führt nicht zu einem Fehler, sondern zu einer leeren Prämienliste
* Aktive prämienpflichtige Kombinationen erfüllen die Bestellbarkeitsregel BR-007
* Die Gruppen sind nach Prämien-Kategorie.Reihenfolge sortiert. Der niedrigste Wert kommt zuerst
* Die Prämien sind nach der Reihenfolge der Prämie innerhalb der Prämien-Kategorie sortiert. Der niedrigste Wert kommt zuerst; bei gleicher Reihenfolge wird alphabetisch nach Prämie.Name sortiert
* Die Angebotsausgaben berechnen sich nach der Business Rule BR-001
* Für Gutscheine und Bargeld ist Prämienbetrag.Geldwert gesetzt und Prämienbetrag.Zuzahlung leer. Für Sachprämien ist Prämienbetrag.Zuzahlung gesetzt (0 = „Kein Betrag“, ein positiver Betrag ist die Höhe der Zuzahlung, die der Kunde zahlen muss) und Prämienbetrag.Geldwert leer

## Mögliche fachliche Ergebnisse

| Situation                                   | Fachliches Ergebnis                                            |
| ------------------------------------------- | -------------------------------------------------------------- |
| Zeitschrift/Abo-Kombination existiert       | Alle Informationen werden geliefert                            |
| Zeitschrift/Abo-Kombination unbekannt       | Fachlicher Fehler „Zeitschrift/Abo-Kombination nicht gefunden“ |
| Keine Prämien gefunden                      | Zeitschrift, Abonnement-Form und Angebotsausgaben werden geliefert, die Liste der Prämien-Kategorien ist leer |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte und geänderte Prämien sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden
