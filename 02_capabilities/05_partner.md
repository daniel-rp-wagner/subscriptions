# Fähigkeit: Die Informationen zu einem Partner bereitstellen

## Fachlicher Zweck

Die Fähigkeit ermöglicht es dem Seitenbesucher, Informationen zu dem aktuellen Partner einzusehen.

Der Seitenbesucher kann dadurch:

* verifizieren, dass er nach der Weiterleitung durch den Partner auf der richtigen Seite ist.

## Fachliche Eingabe

Zur Identifikation wird die externe Partner-Id (`Partner.Externe Id`) angegeben.

## Fachliches Ergebnis

Die Fähigkeit liefert alle Informationen, damit der Seitenbesucher den Partner erkennen kann.

Zu jedem Partner wird bereitgestellt:

* Partner.Externe Id
* Partner.Name
* Partner.Logo (leer, wenn kein Logo hinterlegt ist)


## Fachliche Regeln

* Keine

## Mögliche fachliche Ergebnisse

| Situation               | Fachliches Ergebnis                        |
| ----------------------- | ------------------------------------------ |
| Partner existiert       | Alle Informationen werden geliefert        |
| Partner existiert nicht | Fachlicher Fehler „Partner nicht gefunden“ |

## Fachliche Qualitätsanforderungen

* Geänderte Partner-Informationen sollen zeitnah sichtbar sein
* Die Antwort soll performant bereitgestellt werden