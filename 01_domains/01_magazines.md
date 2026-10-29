# Domäne: Zeitschriften

## Zeitschrift

**Beschreibung:**

Ein periodisch erscheinendes Medium als Print, E-Paper oder als Kombination von Print und E-Paper. Diese Varianten eines Mediums sind jeweils eigenständige Zeitschriften.

**Eigenschaften:**

| **Bezeichnung**   | **Hinweis**                                     | **Beispiel**                                       |
| ----------------- | ----------------------------------------------- | -------------------------------------------------- |
| Name              | eindeutig                                       | Auto Zeitung                                       |
| Bild              | Dateiname/Pfad                                  | autozeitung-abo(55).jpg                            |
| Aktiv             | Kennzeichnet, ob die Zeitschrift angezeigt wird | ja                                                 |
| Kurzbeschreibung  | Kann HTML beinhalten                            |                                                    |
| Langbeschreibung  | Kann HTML beinhalten                            |                                                    |
| Einzelpreis       | je Ausgabe in Euro; > 0                         | 4.99                                               |
| Erscheinungsweise | leer bei unregelmäßiger Erscheinung¹            | monatlich                                          |
| Erscheinungstag   | Optionaler Wochentag; leer, wenn kein einzelner Wochentag eindeutig bestimmbar ist² | Mittwoch |
| Ausgaben          | Anzahl im Jahr; 1–365                           | 11                                                 |
| Typ               | Medientyp³                                      | Print                                              |

¹ **Hinweis**: einer der Werte: _täglich, werktäglich, wöchentlich, 2x wöchentlich, 14-täglich, monatlich, 2-monatlich, quartalsweise_  
² **Hinweis**: einer der Werte: _Montag, Dienstag, Mittwoch, Donnerstag, Freitag, Samstag, Sonntag_  
³ **Hinweis**: einer der Werte: _Print, E-Paper, Kombination_

**Beziehungen:**

- Eine Zeitschrift hat mindestens eine oder mehrere Zeitschriften-Kategorien (z.B. „TV + Fernsehen“) (n:m)
	- Die Zuordnung enthält zusätzlich die Eigenschaft Reihenfolge, die die Sortierung der Zeitschrift innerhalb der jeweiligen Kategorie bestimmt.
- Eine Zeitschrift kann einen Verlag haben (0:1)
- Einer Zeitschrift können Abonnement-Formen zugewiesen sein (0..n, n:m)
	- Die Zuordnung enthält zusätzlich die Prämienbetragskategorie dieser Kombination (0:1, siehe Domäne Prämienbetrag). Bei aktiven prämienpflichtigen Kombinationen gelten BR-007 und BR-008, bei aktiven rabattbasierten Kombinationen BR-008.
- Eine Zeitschrift kann ein oder mehrere Schlagworte haben (n:m)

## Zeitschriften-Kategorie

**Beschreibung:**

Zur Gruppierung der Zeitschriften sind diese in Kategorien unterteilt. Die Kategorien sind flach ohne Hierarchie.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis**                  | **Beispiel**    |
| --------------- | ---------------------------- | --------------- |
| Name            | Für Filterung und Navigation | E-Paper/E-Kombi |
| Reihenfolge     | aufsteigend numerisch        | 3               |

**Beziehungen:**

- Eine Zeitschrift ist einer oder mehreren Kategorien zugewiesen (n:m)

## Zeitschriften-Schlagworte

**Beschreibung:**

Für eine Suche kann jeder Zeitschrift mehrere Schlagworte zugewiesen werden.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis**       | **Beispiel** |
| --------------- | ----------------- | ------------ |
| Name            | Für Suche und SEO | Politik      |

**Beziehungen:**

- Ein Zeitschriften-Schlagwort ist einer oder mehreren Zeitschriften zugewiesen (n:m)

## Verlag

**Beschreibung:**

Ein Zeitschriftenverlag entwirft, produziert und vertreibt periodisch erscheinende Druck- und Digitalmedien. Er steuert Redaktion, Drucklegung sowie Distribution.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis** | **Beispiel**  |
| --------------- | ----------- | ------------- |
| Name            |  			| Gruner + Jahr |

**Beziehungen:**

- Ein Verlag kann eine oder mehrere Zeitschriften haben (0..n)
