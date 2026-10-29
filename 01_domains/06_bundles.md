# Domäne: Bündelangebot

## Bündelangebot

**Beschreibung:**

Ein Bündelangebot ist ein Komplettangebot aus Zeitschrift und Prämie vorausgewählt. Das Angebot kann besondere Abonnement-Bedingungen abbilden (z.B. nur 2 Ausgaben, 5 Ausgaben, 2 Monate, ...).

**Eigenschaften:**

| **Bezeichnung**         | **Hinweis**                                                             | **Beispiel**                     |
| ----------------------- | ----------------------------------------------------------------------- | -------------------------------- |
| Name                    | Zur internen Verwaltung; wird öffentlich nicht ausgegeben               | 10xAutozeitung + 30€ Geldprämie  |
| Aktiv                   | Kennzeichnet, ob das Bündelangebot derzeit verwendet werden kann        | ja                               |
| Laufzeit in Monaten     | Ganze Zahl > 0; immer Pflicht²                                    | 6                                |
| Ausgaben                | Laufzeit in Ausgaben (> 0); Pflicht bei Zeitraum „Ausgaben“, sonst leer | 4                                |
| Zeitraum                | Bestimmt, ob das Angebot nach Monaten oder Ausgaben endet¹              | Monate                           |
| Rabatt für Bankeinzug   | ja/nein                                                                 | nein                             |
| Geldwert                | Maßgeblicher Gutschein- / Bargeldwert der Geldwert-Prämie               | 55                               |

¹ **Hinweis**: einer der Werte: _Monate oder Ausgaben_
² **Hinweis**: Bei Zeitraum „Monate“ sowohl Angebotslaufzeit als auch anschließender Abrechnungsrhythmus, bei Zeitraum „Ausgaben“ nur der anschließende Abrechnungsrhythmus.

**Beziehungen:**

- Jedem Bündelangebot ist genau eine Zeitschrift zugewiesen; eine Zeitschrift kann mehreren Bündelangeboten zugewiesen sein (n:1)
- Ein Bündelangebot kann eine Sachprämie enthalten (0:1). Sie hat die Prämienart Sachprämie.
- Ein Bündelangebot kann eine Geldwert-Prämie enthalten (0:1). Sie hat die Prämienart Gutschein oder Bargeld.
- Mindestens eine der beiden Beziehungen muss bestehen.

**Regeln:**

- Ist eine Geldwert-Prämie zugeordnet, muss Bündelangebot.Geldwert > 0 sein. Ohne Geldwert-Prämie ist Bündelangebot.Geldwert leer oder 0.
- Bündelangebot.Laufzeit in Monaten ist immer gesetzt und > 0. Bei Zeitraum „Monate“ ist Bündelangebot.Ausgaben leer. Bei Zeitraum „Ausgaben“ ist Bündelangebot.Ausgaben gesetzt und > 0.
- Bei Zeitraum „Monate“ entspricht der Abrechnungsrhythmus nach der Angebotslaufzeit dieser Laufzeit in Monaten. Bei Zeitraum „Ausgaben“ bestimmt Laufzeit in Monaten den Abrechnungsrhythmus nach den vereinbarten Ausgaben (BR-005).
- Angebotsausgaben, Angebotspreis und Zahlungsrhythmus werden nach BR-006, BR-003 und BR-005 ermittelt.
- Ein Bündelangebot ergibt mindestens 1 Angebotsausgabe. Speichern eines Bündelangebots und Änderungen der Ausgaben der Zeitschrift, die weniger ergäben, werden abgelehnt.
- Wird die zugeordnete Zeitschrift, die Sachprämie oder die Geldwert-Prämie inaktiv gesetzt, wird das Bündelangebot automatisch inaktiv gesetzt. Beim erneuten Aktivieren der Zeitschrift oder Prämie wird das Bündelangebot nicht automatisch aktiviert.
- Ein Bündelangebot kann nur aktiv angelegt, aktiv gesetzt oder einer anderen Zeitschrift bzw. Prämie zugeordnet werden, wenn die zugeordnete Zeitschrift und alle zugeordneten Prämien aktiv sind; andernfalls wird das Speichern abgelehnt.
- Ein Bündelangebot kann gelöscht werden; eingereichte Anträge behalten ihre Angaben zum Bündelangebot.
