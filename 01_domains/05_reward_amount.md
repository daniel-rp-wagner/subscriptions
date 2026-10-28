# Domäne: Prämienbetrag

## Prämienbetrag

**Beschreibung:**

Ein Prämienbetrag beschreibt die für eine Prämie und eine Prämienbetragskategorie gültigen Beträge. Je nach Prämienart ist entweder ein Geldwert, den der Kunde als Bargeld- oder Gutscheinprämie erhält, oder eine vom Kunden zu leistende Zuzahlung gesetzt.

**Eigenschaften:**

| **Bezeichnung**         | **Hinweis**                                                                  | **Beispiel** |
| ----------------------- | ---------------------------------------------------------------------------- | ------------ |
| Prämie                  | Verweis zur Prämie                                                           |              |
| Prämienbetragskategorie | Verweis zur Prämienbetragskategorie                                          |              |
| Geldwert                | Wert bei Gutschein und Bargeld; leer bei Sachprämie                          | 80.00        |
| Zuzahlung               | Zuzahlung bei Sachprämie (0 = „Kein Betrag“); leer bei Gutschein und Bargeld | 29.90        |

Genau einer der beiden Beträge ist gesetzt. Bei Prämie.Art = Gutschein oder Bargeld ist der Geldwert gesetzt und > 0, bei Prämie.Art = Sachprämie die Zuzahlung. Hier ist der Wert >= 0.

**Beziehungen:**

- Eine Prämie kann mehrere Prämienbeträge haben. (1:n)
- Pro Kombination aus Prämie und Prämienbetragskategorie existiert höchstens ein Prämienbetrag.

## Prämienbetragskategorie

**Beschreibung:**

Die Prämienbetragskategorie ist eine interne Kalkulationsgruppe und bestimmt die Höhe der Prämienbeträge für die Prämien in Abhängigkeit des Werts eines Angebots. Der Wert hängt von mehreren Faktoren ab und wird von Controlling individuell festgelegt.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis**             | **Beispiel** |
| --------------- | ----------------------- | ------------ |
| Name            | Zur internen Verwaltung | Kategorie UU |

**Beziehungen:**

- Prämienbeträge sind jeweils einer Prämienbetragskategorie zugewiesen. (n:1)
- Jeder Kombination aus Abonnement-Form und Zeitschrift ist höchstens eine Prämienbetragskategorie zugeordnet. Die Zuordnung ist eine Eigenschaft der Zuordnung Zeitschrift × Abonnement-Form und kann fehlen.
