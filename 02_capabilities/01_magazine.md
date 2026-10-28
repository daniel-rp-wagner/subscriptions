# Fähigkeit: Zeitschriften-Details bereitstellen

## Fachlicher Zweck

Die Fähigkeit liefert die für die Auswahl einer Zeitschrift und einer Abonnement-Form relevanten Informationen.

Der Seitenbesucher kann dadurch:

* Sich über die Zeitschrift informieren
* Details über Erscheinungsweise und Ausgaben einsehen
* Alle aktiven und der Zeitschrift zugewiesenen Abonnement-Formen mit den Vorteilen ansehen

## Fachliche Eingabe

Zur Identifikation wird eine Zeitschrift angegeben.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher die Auswahl treffen kann, welche Zeitschrift und Abonnement-Form er wählen soll.

Zu jeder Zeitschrift wird bereitgestellt:

* Zeitschrift.Id
* Zeitschrift.Bild
* Zeitschrift.Name
* Zeitschrift.Verlag (Name des Verlags; leer, wenn kein Verlag zugeordnet ist)
* Zeitschrift.Kurzbeschreibung
* Zeitschrift.Langbeschreibung
* Zeitschrift.Erscheinungsweise
* Zeitschrift.Erscheinungstag
* Zeitschrift.Einzelpreis
* Zeitschrift.Ausgaben
* Zeitschrift.Typ
* Alle der Zeitschrift zugewiesenen Zeitschriften-Kategorien (Liste), je Kategorie:
  * Zeitschriften-Kategorie.Id
  * Zeitschriften-Kategorie.Name
* Alle der Zeitschrift zugewiesenen Schlagworte (alphabetisch sortiert)
* Alle aktiven und der Zeitschrift zugewiesenen Abonnement-Formen

Zu jeder Abonnement-Form wird bereitgestellt:

* Abonnement-Form.Id
* Abonnement-Form.Name
* Abonnement-Form.Kurzbeschreibung
* Abonnement-Form.Langbeschreibung
* Abonnement-Form.Variante
* Abonnement-Form.Mindestlaufzeit
* Abonnement-Form.Rabatt
* Abonnement-Form.Rabatt für Bankeinzug

Zu jeder Abonnement-Form wird berechnet:

* Angebotsform
* Angebotsausgaben
* Angebotspreis
* Regulärer Preis
* Maximaler Vorteil

## Fachliche Regeln

* Nur aktive Zeitschriften werden angezeigt
* Nur aktive und der Zeitschrift zugewiesenen Abonnement-Formen dürfen angezeigt werden
* Die Abonnement-Formen sind nach dem Abonnement-Form.Reihenfolge sortiert. Der niedrigste Wert kommt zuerst.
* Die Zeitschriften-Kategorien sind nach Zeitschriften-Kategorie.Reihenfolge sortiert. Der niedrigste Wert kommt zuerst; bei gleicher Reihenfolge alphabetisch nach Name, danach nach Id.
* Die Prämienbetragskategorie ist eine interne Kalkulationsgruppe und wird nicht ausgegeben.
* Die Angebotsform ist „rabattbasiert“, wenn Abonnement-Form.Rabatt > 0, ansonsten „prämienpflichtig“
* Die Angebotsausgaben berechnen sich nach der Business Rule BR-001
* Der Angebotspreis berechnet sich nach der Business Rule BR-002
* Der reguläre Preis berechnet sich nach der Business Rule BR-003
* Der maximale Vorteil ist der höchste Wert von Prämienbetrag.Geldwert bei aktiven Prämien mit Prämie.Art = „Gutschein“, die der Abonnement-Form zugeordnet sind und in der für die Kombination Zeitschrift × Abonnement-Form ermittelten Prämienbetragskategorie einen Prämienbetrag besitzen (z.B. Auslobung im Frontend „bis zu 280 € Gutschein für Sie.“). Bargeldprämien werden beim maximalen Vorteil nicht berücksichtigt. Fehlt die Prämienbetragskategorie-Zuordnung für die Kombination oder gibt es keine solche Gutscheinprämie, entfällt der maximale Vorteil (kein Wert).

## Mögliche fachliche Ergebnisse

| Situation                   | Fachliches Ergebnis                            |
| --------------------------- | ---------------------------------------------- |
| Zeitschrift existiert       | Alle Informationen werden geliefert            |
| Zeitschrift inaktiv         | Fachlicher Fehler „Zeitschrift nicht gefunden“ |
| Zeitschrift unbekannt       | Fachlicher Fehler „Zeitschrift nicht gefunden“ |

## Fachliche Qualitätsanforderungen

* Änderungen an den Zeitschriften sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden

---

# Fähigkeit: Alle Zeitschriften einer Zeitschriften-Kategorie bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es, alle Zeitschriften einer bestimmten Zeitschriften-Kategorie einzusehen.

Der Seitenbesucher kann dadurch:

* eine Auswahl nach Zeitschriften-Kategorie treffen
* alle zur Verfügung stehenden Zeitschriften einer Zeitschriften-Kategorie einsehen

## Fachliche Eingabe

Eine Zeitschriften-Kategorie als Auswahl-Kriterium sowie jeweils ein Sortier-Kriterium und ein Filter-Kriterium. Alle Eingaben sind optional.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Zeitschriften einer Zeitschriften-Kategorie, damit der Seitenbesucher eine Übersicht erhält, welche Zeitschriften angeboten werden.

Zu jeder Zeitschrift wird bereitgestellt:

* Zeitschrift.Id
* Zeitschrift.Bild
* Zeitschrift.Name
* Zeitschrift.Typ

Zur Zeitschriften-Kategorie wird bereitgestellt:

* Zeitschriften-Kategorie.Id
* Zeitschriften-Kategorie.Name

Zu jeder Zeitschriften-Kategorie wird berechnet:

* Anzahl der angezeigten Zeitschriften

## Fachliche Regeln

* Nur aktive Zeitschriften werden angezeigt
* Die Anzahl der Zeitschriften wird dynamisch berechnet und ausgegeben
* Wenn keine gültige Zeitschriften-Kategorie angegeben wird, werden alle vorhandenen Zeitschriften ausgegeben
* Optional kann nach der Reihenfolge der Zeitschrift in dieser Zeitschriften-Kategorie sortiert werden; bei gleicher Reihenfolge wird alphabetisch nach Zeitschrift.Name sortiert. Die Sortierung nach Kategorie-Reihenfolge setzt eine gültige Zeitschriften-Kategorie voraus; fehlt sie oder ist sie ungültig, führt das zu einem Validierungsfehler
* Falls kein Sortier-Kriterium angegeben wird, erfolgt die Sortierung alphabetisch nach Zeitschrift.Name
* Zulässige Sortier-Kriterien sind ausschließlich „alphabetisch nach Name“ (`name`) und „Kategorie-Reihenfolge“ (`category_order`). Ein anderes Sortier-Kriterium führt zu einem Validierungsfehler.
* Das Filter-Kriterium filtert nach dem Anfangsbuchstaben von Zeitschrift.Name. Zulässig ist genau ein Buchstabe A–Z; Groß- und Kleinschreibung wird nicht unterschieden. Umlaute am Namensanfang werden dem Grundbuchstaben zugeordnet (Ä → A, Ö → O, Ü → U). Ein unzulässiges Filter-Kriterium führt zu einem Validierungsfehler.
* Wird keine gültige Zeitschriften-Kategorie angegeben, bleibt die Zeitschriften-Kategorie im Ergebnis leer; die Anzahl bezieht sich auf alle gelieferten Zeitschriften.

## Mögliche fachliche Ergebnisse

| Situation                                       | Fachliches Ergebnis                              |
| ----------------------------------------------- | ------------------------------------------------ |
| Mindestens eine Zeitschrift existiert           | Alle Informationen werden geliefert              |
| Keine gültige Zeitschriften-Kategorie angegeben | Alle vorhandenen Zeitschriften werden geliefert  |
| Keine Zeitschrift gefunden                      | Leere Ergebnismenge                              |
| Ein Sortier-Kriterium wurde angegeben           | Zeitschriften werden danach sortiert ausgegeben  |
| Ungültiges Sortier-Kriterium angegeben          | Validierungsfehler                               |
| Sortierung nach Kategorie-Reihenfolge ohne gültige Zeitschriften-Kategorie | Validierungsfehler |
| Ungültiges Filter-Kriterium angegeben           | Validierungsfehler                               |


## Fachliche Qualitätsanforderungen

* Neu veröffentlichte Zeitschriften sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden

---

# Fähigkeit: Alle Zeitschriften einer Abonnement-Form bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es, nach Auswahl einer Abonnement-Form, alle angebotenen Zeitschriften einzusehen.

Der Seitenbesucher kann dadurch:

* zuerst die für ihn passende Abonnement-Form auswählen
* anschließend die möglichen Zeitschriften durchstöbern

## Fachliche Eingabe

Eine gültige, aktive Abonnement-Form sowie optional ein Sortier-Kriterium für die Zeitschriften und optional eine Zeitschriften-Kategorie-Id für die Sortierung nach Kategorie-Reihenfolge.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher die Auswahl treffen kann, welche Zeitschrift und Abonnement-Form er wählen soll.

Zu jeder Zeitschrift wird bereitgestellt:

* Zeitschrift.Id
* Zeitschrift.Bild
* Zeitschrift.Name
* Zeitschrift.Typ
* Abonnement-Form.Mindestlaufzeit
* Angebotspreis
* Regulärer Preis

## Fachliche Regeln

* Nur aktive Zeitschriften, denen die Abonnement-Form zugewiesen ist, werden angezeigt
* Standard ist die alphabetische Sortierung nach Zeitschrift.Name
* Zulässige Sortier-Kriterien sind ausschließlich „alphabetisch nach Name“ (`name`) und „Kategorie-Reihenfolge“ (`category_order`). Ein anderes Sortier-Kriterium führt zu einem Validierungsfehler.
* Wird als Sortier-Kriterium die Kategorie-Reihenfolge gewählt, muss eine gültige Zeitschriften-Kategorie-Id angegeben werden; sortiert wird dann nach der Reihenfolge der Zeitschrift innerhalb dieser Kategorie; bei gleicher Reihenfolge alphabetisch nach Zeitschrift.Name. Zeitschriften, die dieser Kategorie nicht zugeordnet sind, folgen am Ende alphabetisch nach Zeitschrift.Name
* Wird nach Kategorie-Reihenfolge sortiert und fehlt die Zeitschriften-Kategorie-Id oder ist sie ungültig, führt das zu einem Validierungsfehler
* Eine Zeitschriften-Kategorie-Id ist nur zusammen mit dem Sortier-Kriterium Kategorie-Reihenfolge zulässig; andernfalls führt sie zu einem Validierungsfehler
* Der Angebotspreis berechnet sich nach der Business Rule BR-002
* Der reguläre Preis berechnet sich nach der Business Rule BR-003

## Mögliche fachliche Ergebnisse

| Situation                                            | Fachliches Ergebnis                               |
| ---------------------------------------------------- | ------------------------------------------------- |
| Mindestens eine Zeitschrift existiert                | Alle Informationen werden geliefert               |
| Keine gültige, aktive Abonnement-Form angegeben      | Fachlicher Fehler Abonnement-Form nicht gefunden“ |
| Keine Zeitschrift gefunden                           | Fachlicher Fehler „Zeitschriften nicht gefunden“  |
| Ein Sortier-Kriterium wurde angegeben                | Zeitschriften werden danach sortiert ausgegeben   |
| Ungültiges Sortier-Kriterium angegeben               | Validierungsfehler                                |
| Sortierung nach Kategorie-Reihenfolge ohne gültige Zeitschriften-Kategorie-Id | Validierungsfehler |
| Zeitschriften-Kategorie-Id ohne Sortierung nach Kategorie-Reihenfolge | Validierungsfehler |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte Zeitschriften sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden
