# Domäne: Prämien

## Prämie

**Beschreibung:**

Eine Prämie ist ein Anreiz, der im Rahmen eines Abonnement-Angebots gewährt wird, z. B. Sachartikel, Gutscheine oder Geldbeträge, ggf. verbunden mit einem Prämienbetrag.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis**                                     | **Beispiel**                |
| --------------- | ----------------------------------------------- | --------------------------- |
| Name            |                                                 | CLEANMAXX Akkusauger 3 in 1 |
| Artikelnummer   | Eindeutig                                       | 30225                       |
| Bild            | Dateiname/Pfad                                  | akkusauger_3_in_1_30532.jpg |
| Aktiv           | Kennzeichnet, ob Artikel noch verfügbar         | ja                          |
| Art             | Art der Prämie¹                                 | Sachprämie                  |
| Warenwert       | optional; ≥ 0                                   | 29.99                       |
| Merkmale        | Freitext (HTML); relevant für die Anzeige       | Mit waschbarem HEPA-Filter  |

¹ **Hinweis**: einer der Werte: _Bargeld, Sachprämie, Gutschein_.

**Beziehungen:**

- Eine Prämie ist mindestens einer Prämien-Kategorie zugewiesen (n:m)
	Die Zuordnung enthält zusätzlich die Eigenschaft Reihenfolge, die die Sortierung der Prämie innerhalb der jeweiligen Kategorie bestimmt.
- Eine Prämie kann Abonnement-Formen zugewiesen sein (n:m, siehe Domäne Abonnement)
- Eine Prämie hat Prämienbeträge je Prämienbetragskategorie; beim Löschen der Prämie werden ihre Zuordnungen und Prämienbeträge mitgelöscht. Ist die Prämie einem Bündelangebot oder einer Zugabe zugeordnet, ist sie nicht löschbar.

## Prämien-Kategorie

**Beschreibung:**

Zur Gruppierung der Prämien sind diese in Prämien-Kategorien unterteilt. Die Prämien-Kategorien sind flach ohne Hierarchie.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis**                  | **Beispiel**            |
| --------------- | ---------------------------- | ----------------------- |
| Name            | Für Filterung und Navigation | Bargeld + Gutscheine    |
| Reihenfolge     | aufsteigend numerisch        | 12                      |

**Beziehungen:**

- Eine Prämie ist einer oder mehreren Prämien-Kategorie zugewiesen (n:m)
