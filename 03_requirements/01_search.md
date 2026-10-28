# REQ001: Freitextsuche über Schlagworte

## Ziel

Dem Benutzer soll eine Freitextsuche zur Verfügung stehen, mit der Zeitschriften anhand ihrer hinterlegten Schlagworte gefunden werden können.

## Datenbasis

Jede Zeitschrift verfügt über **Schlagworte**, die in einer separaten Tabelle gespeichert sind.

## Funktionale Anforderungen

### Suchverhalten

* Die Suche erfolgt ausschließlich auf Basis der in **Schlagworte** hinterlegten Begriffe.
* Die Suche ist unabhängig von der Groß- und Kleinschreibung.
* Führende und nachfolgende Leerzeichen in der Suchanfrage sowie in den Schlagworten werden bei der Suche nicht berücksichtigt.
* Umlaute und deren alternative Schreibweisen werden gleich behandelt (z. B. „Müller" = „Mueller", „Über" = „Ueber").
* `ß` und `ss` werden gleich behandelt (z. B. „Straße" = „Strasse").
* Die Suchanfrage kann aus einem oder mehreren Suchbegriffen bestehen. Suchbegriffe werden durch Leerzeichen getrennt; mehrere aufeinanderfolgende Leerzeichen trennen wie eines, doppelte Suchbegriffe werden nur einmal berücksichtigt. Tabulatoren und Zeilenumbrüche sind in der Suchanfrage unzulässig (Validierungsfehler).
* Mehrere Suchbegriffe werden standardmäßig als ODER-Verknüpfung interpretiert. Eine Zeitschrift wird somit gefunden, wenn mindestens einer der Suchbegriffe in den Schlagworten enthalten ist.
* Ein Suchbegriff trifft nur bei **exakter Übereinstimmung** eines normalisierten Schlagworts (kein Teilstring-Match).
* Bindestriche und andere Sonderzeichen werden nicht normalisiert.
* Schlagworte, die Leerzeichen enthalten, können nicht gefunden werden, da Suchbegriffe an Leerzeichen getrennt werden.
* Wenn keine Zeitschriften zu einer Suchanfrage gefunden werden, wird eine leere Ergebnismenge zurückgeliefert.

### Ergebnisermittlung

* Eine Zeitschrift wird als Treffer zurückgegeben, wenn mindestens eines seiner Schlagworte den Suchkriterien entspricht. Jede Zeitschrift erscheint höchstens einmal; nur aktive Zeitschriften werden gefunden.
* Die Suchergebnisse werden alphabetisch sortiert.

### Nichtfunktionale Anforderungen

* Die Suche soll auch bei einer hohen Anzahl von Artikeln eine kurze Antwortzeit gewährleisten.
* Die Suchergebnisse müssen reproduzierbar und nachvollziehbar sein.
* Es gilt eine Längenbeschränkung für die Eingabe von 80 Zeichen (Unicode-Zeichen, nicht Bytes). Die Länge wird vor dem Entfernen führender und nachfolgender Leerzeichen geprüft.
* Ist die Suchanfrage nach dem Entfernen führender und nachfolgender Leerzeichen leer, ist sie ungültig (Validierungsfehler).
