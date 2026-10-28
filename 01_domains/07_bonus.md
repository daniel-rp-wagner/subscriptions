# Domäne: Zugabe

## Zugabe

**Beschreibung:**

Eine Zugabe ist eine weitere Prämie, die in Abhängigkeit eines URL-Parameter-Wertes zusätzlich vergeben werden kann.

**Eigenschaften:**

| **Bezeichnung** | **Hinweis**                                                     | **Beispiel**          |
| --------------- | --------------------------------------------------------------- | --------------------- |
| Name            |                                                                 | Gratis Regenschirm    |
| Bild            | Dateiname/Pfad                                                  | gutschein-praemie.jpg |
| Aktiv           | Kann eine Zugabe deaktivieren, unabhängig von der Gültigkeit    | ja                    |
| von             | Gültigkeit: Beginn der Aktion; Datum ohne Uhrzeit, Pflicht      | 01.05.2026            |
| bis             | Gültigkeit: Ende der Aktion; Datum ohne Uhrzeit, Pflicht, ≥ von | 31.08.2026            |

### Anwendbarkeit je Abonnement-Form

Für jede einer Zugabe zugewiesene Abonnement-Form kann definiert werden, für welche Produkte die Zugabe gültig ist.

| **Bezeichnung**    | **Hinweis**                                                                           | **Beispiel**  |
| ------------------ | ------------------------------------------------------------------------------------- | ------------- |
| Abonnement-Form    | Zugeordnete Abonnement-Form                                                           | 2-Jahres-Abo  |
| Gültigkeitsbereich | Definiert den Anwendungsbereich der Zugabe¹                                           | Alle          |
| Zeitschriften      | Auswahl der gültigen Zeitschriften bei Gültigkeitsbereich „Ausgewählte Zeitschriften“ | Focus, Stern  |
| Prämien            | Auswahl der gültigen Prämien bei Gültigkeitsbereich „Ausgewählte Prämien“             | JBL Kopfhörer |

¹ **Hinweis**: einer der Werte: _Alle, Ausgewählte Zeitschriften, Ausgewählte Prämien_. Bei „Alle“ sind weder Zeitschriften noch Prämien ausgewählt, bei „Ausgewählte Zeitschriften“ mindestens eine Zeitschrift und keine Prämie, bei „Ausgewählte Prämien“ mindestens eine Prämie und keine Zeitschrift. Die ausgewählten Zeitschriften und Prämien müssen der Abonnement-Form nicht zugeordnet sein.

**Beziehungen:**

* Jeder Zugabe ist genau eine Prämie zugewiesen (1:1). Die Prämie muss die Art Sachprämie haben.
* Jeder Zugabe muss ein oder mehrere URL-Parameter-Werte zugewiesen sein (1:n). Ein Parameter-Wert darf nur einer Zugabe zugeordnet werden.
* Jeder Zugabe können ein oder mehrere Partner zugewiesen werden (0:n).
* Jeder Zugabe können eine oder mehrere Abonnement-Formen zugewiesen werden (1:n).
* Einer Zuordnung zwischen Zugabe und Abonnement-Form können mehrere Zeitschriften zugeordnet werden (0:n).
* Einer Zuordnung zwischen Zugabe und Abonnement-Form können mehrere Prämien zugeordnet werden (0:n).

**Regeln:**

* Wird die der Zugabe zugewiesene Prämie inaktiv gesetzt, wird die Zugabe automatisch inaktiv gesetzt. Beim erneuten Aktivieren der Prämie wird die Zugabe nicht automatisch aktiviert.
* Eine Zugabe kann nur aktiv angelegt, aktiv gesetzt oder einer anderen Prämie zugeordnet werden, wenn die zugeordnete Prämie aktiv ist; andernfalls wird das Speichern abgelehnt.
* Zeitschriften und Prämien im Gültigkeitsbereich einer Zugabe beeinflussen den Aktiv-Status der Zugabe nicht.
* Die Gültigkeit (von/bis, jeweils einschließlich) wird in der Zeitzone Europe/Berlin ausgewertet.
* Der Gültigkeitsbereich „Ausgewählte Prämien“ darf auch bei rabattbasierten Abonnement-Formen hinterlegt werden, ist dort aber nie anwendbar, da keine Hauptprämie gewählt werden kann.
* Eine Zugabe kann gelöscht werden; ihre URL-Parameter-Werte und Zuordnungen werden mitgelöscht, eingereichte Anträge behalten ihre Angaben zur Zugabe.
