# REQ-001: Freitextsuche über Zeitschriftennamen und Schlagworte

## Ziel

Dem Benutzer soll eine Freitextsuche zur Verfügung stehen, mit der Zeitschriften anhand von Zeitschrift.Name und ihren hinterlegten Schlagworten gefunden werden können.

## Datenbasis

Jede Zeitschrift verfügt über Zeitschrift.Name und über **Schlagworte**, die in einer separaten Tabelle gespeichert sind.

## Funktionale Anforderungen

### Suchverhalten

* Die Suche erfolgt ausschließlich auf Basis von Zeitschrift.Name und den zugeordneten Schlagworten.
* Die Suche ist unabhängig von der Groß- und Kleinschreibung.
* Führende und nachfolgende Leerzeichen in der Suchanfrage, Zeitschrift.Name sowie in den Schlagworten werden bei der Suche nicht berücksichtigt.
* Umlaute und deren alternative Schreibweisen werden gleich behandelt (z. B. „Müller" = „Mueller", „Über" = „Ueber").
* `ß` und `ss` werden gleich behandelt (z. B. „Straße" = „Strasse").
* Die Suchanfrage kann aus einem oder mehreren Suchbegriffen bestehen. Suchbegriffe werden durch Leerzeichen getrennt; mehrere aufeinanderfolgende Leerzeichen trennen wie eines, doppelte Suchbegriffe werden nur einmal berücksichtigt. Tabulatoren und Zeilenumbrüche sind in der Suchanfrage unzulässig (Validierungsfehler).
* Zeitschrift.Name und die zugeordneten Schlagworte werden ebenfalls an einem oder mehreren aufeinanderfolgenden Leerzeichen in einzelne Wörter zerlegt.
* Ein Suchbegriff trifft genau dann zu, wenn er nach Normalisierung vollständig mit einem normalisierten Wort aus Zeitschrift.Name oder einem zugeordneten Schlagwort übereinstimmt. Präfix- und Teilstring-Treffer sind ausgeschlossen.
* Mehrere Suchbegriffe werden standardmäßig als ODER-Verknüpfung interpretiert. Eine Zeitschrift wird somit gefunden, wenn mindestens einer der Suchbegriffe einen solchen Worttreffer ergibt.
* Bindestriche und andere Sonderzeichen werden nicht normalisiert und gelten nicht als Worttrenner.
* Wenn keine Zeitschriften zu einer Suchanfrage gefunden werden, wird eine leere Ergebnismenge zurückgeliefert.

### Ergebnisermittlung

* Eine Zeitschrift wird als Treffer zurückgegeben, wenn mindestens ein Wort aus Zeitschrift.Name oder einem ihrer Schlagworte den Suchkriterien entspricht. Jede Zeitschrift erscheint höchstens einmal; nur aktive Zeitschriften werden gefunden.
* Die Suchergebnisse werden alphabetisch sortiert.

Beispiele für Zeitschrift.Name (dieselben Regeln gelten für Schlagworte):

| Zeitschrift.Name | Suchanfrage | Treffer |
| ---------------- | ----------- | ------- |
| Auto Zeitung     | Auto        | ja      |
| Auto Zeitung     | Aut         | nein    |
| Auto-Zeitung     | Auto        | nein    |
| Müller Magazin   | Mueller     | ja      |
| Auto Zeitung     | Zeitung Auto | ja     |

### Nichtfunktionale Anforderungen

* Die Suche soll auch bei einer hohen Anzahl von Artikeln eine kurze Antwortzeit gewährleisten.
* Die Suchergebnisse müssen reproduzierbar und nachvollziehbar sein.
* Es gilt eine Längenbeschränkung für die Eingabe von 80 Zeichen (Unicode-Zeichen, nicht Bytes). Die Länge wird vor dem Entfernen führender und nachfolgender Leerzeichen geprüft.
* Ist die Suchanfrage nach dem Entfernen führender und nachfolgender Leerzeichen leer, ist sie ungültig (Validierungsfehler).
