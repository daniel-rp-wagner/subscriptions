# Fähigkeit: Gültige Zugabe zu einem Einsprung ermitteln

## Fachlicher Zweck

Die Fähigkeit ermittelt die für einen Einsprung gültige Zugabe anhand eines URL-Parameter-Wertes und optional eines Partners. Da ein URL-Parameter-Wert höchstens einer Zugabe zugeordnet ist, gibt es zu einem Einsprung höchstens eine gültige Zugabe.

Der Marketing-Mitarbeiter kann dadurch:

* bei Partnern beworbene Angebote noch attraktiver für den Kunden machen.

## Fachliche Eingabe

Zur Identifikation wird ein URL-Parameter-Wert angegeben (nur Ziffern, 1–20 Stellen). Optional kann zusätzlich die externe Partner-Id (`Partner.Externe Id`) angegeben werden. Ist die angegebene Partner-Id keinem Partner zugeordnet, wird so verfahren, als wäre keine Partner-Id angegeben.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit das System die Zugabenprämie anzeigen kann.

Zur Zugabe wird bereitgestellt:

* Zugabe.Name
* Zugabe.Bild
* Zu jeder gültigen Zugabe werden alle zugeordneten aktiven Abonnement-Formen geliefert (sortiert nach Abonnement-Form.Reihenfolge, dann Name)

Zu jeder Abonnement-Form wird bereitgestellt:

* Gültigkeitsbereich
* Abonnement-Form.Id
* Abonnement-Form.Name
* Alle in dieser Abonnement-Form gültigen Zeitschriften (Id, Bild, Name; nur aktive; alphabetisch; leer außer bei „Ausgewählte Zeitschriften“)
* Alle in dieser Abonnement-Form gültigen Prämien (Id, Bild, Name; nur aktive; alphabetisch; leer außer bei „Ausgewählte Prämien“)

Die Id der Zugabe wird nicht ausgegeben; bei der Antragstellung ermittelt das System die Zugabe selbst aus dem URL-Parameter-Wert.

Zur Gratis-Prämie wird bereitgestellt:

* Prämie.Id
* Prämie.Bild
* Prämie.Name
* Prämie.Merkmale
* Prämie.Art
* Prämie.Warenwert

## Fachliche Regeln

* Eine Zugabe wird nur berücksichtigt, wenn sie aktiv ist.
* Eine Zugabe wird nur berücksichtigt, wenn das aktuelle Datum (Zeitzone Europe/Berlin) zwischen dem Gültigkeitsbeginn und dem Gültigkeitsende (einschließlich) liegt.
* Eine Zugabe wird nur berücksichtigt, wenn das angegebene URL-Parameter-Wert der Zugabe zugeordnet ist.
* Eine Zugabe wird nur berücksichtigt, wenn ihr mindestens eine aktive Abonnement-Form zugeordnet ist.
* Zugaben ohne Partnerzuordnung gelten für alle Einsprünge, mit oder ohne Partner-Id.
* Zugaben mit Partnerzuordnung gelten nur, wenn die angegebene Partner-Id einem ihrer Partner entspricht; ohne Partner-Id oder mit unbekannter Partner-Id gelten sie nicht.
* Es werden nur aktive Abonnement-Formen, Zeitschriften und Prämien der Zugabe geliefert.
* Bei Gültigkeitsbereich „Alle“ dürfen keine Zeitschriften oder Prämien hinterlegt werden.
* Bei Gültigkeitsbereich „Ausgewählte Zeitschriften“ muss mindestens eine Zeitschrift hinterlegt werden.
* Bei Gültigkeitsbereich „Ausgewählte Prämien“ muss mindestens eine Prämie hinterlegt werden.

## Mögliche fachliche Ergebnisse

| Situation                                          | Fachliches Ergebnis                 |
| -------------------------------------------------- | ----------------------------------- |
| Gültige Zugabe gefunden                            | Alle Informationen werden geliefert |
| Keine gültige Zugabe gefunden                      | Leere Ergebnismenge                 |
| URL-Parameter-Wert fehlt oder ist ungültig         | Validierungsfehler                  |

## Fachliche Qualitätsanforderungen

* Geänderte Zugabe-Informationen sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden