# Business Specification

## 1. Ziel & Zweck

Dieses Dokument beschreibt das Geschäftsmodell für Zeitschriften-Abonnements.

Ziel ist es, Kunden regelmäßig Zugang zu Zeitschrifteninhalten zu bieten und dabei wiederkehrende Einnahmen zu generieren.
Durch die Kombination des Zeitschriften-Abonnements mit verschiedenen Prämien oder einem weiteren Rabatt entsteht dem Kunden ein echter Vorteil gegenüber einem direkten Abonnement beim Anbieter.

**Problemstellung:**
Kunden möchten bequem und kontinuierlich Zugriff auf relevante Inhalte, ohne einzelne Ausgaben separat kaufen zu müssen.

**Mehrwert:**
 * Kontinuierliche Belieferung (physisch oder digital)
 * Preisvorteil gegenüber Einzelkauf

---

## 2. Akteure

**Abonnent**: Der Abonnent schließt das Abonnement ab. Der Begriff „Abonnent“ wird fachlich nur als Oberbegriff verwendet. Als Rollen werden nur Rechnungsempfänger, Zeitschriftenempfänger und Prämienempfänger gespeichert.

**Zeitschriftenempfänger**: Bezieht die Zeitschrift.

**Prämienempfänger**: Empfänger der Prämie. Der Empfänger der Prämie bezahlt auch eine gegebenenfalls anfallende Zuzahlung per Nachnahme. Der Prämienversand ist nicht Teil der Anwendung. Für die fachliche Auslobung kann jedoch der Hinweis gespeichert oder angezeigt werden, dass der Versand üblicherweise sechs bis acht Wochen nach Zahlungseingang erfolgt.

**Rechnungsempfänger**: Person, die das Abonnement bezahlt und auch kündigen kann.

**Anbieter**: Externes Unternehmen, dass die Zeitschrift verschickt und Abos verwaltet.

**Partner**: Werbepartner, die Abonnements für uns bewerben und dafür Provision erhalten.

**Marketing-Mitarbeiter**: Pflege von Kontakt zu Affiliate-Partner und Pflege von Marketingaktionen (Banner, Flyer, etc.)

**Controlling-Mitarbeiter**: Datenpflege im Shopbackend

**KS-Mitarbeiter**: Auftragserfassung, Auftragskorrektur / Datenanreicherung und Weitergabe an Anbieter (PVZ) und Kundenschnittstelle

---

## 3. Geschäftsmodell

**Grundprinzip:**
Ein Kunde schließt ein Abonnement ab und erhält regelmäßig Zugriff auf Zeitschrifteninhalte, solange er bezahlt.
Je länger das Abonnement abgeschlossen wird und je höher der damit generierte Auftragswert ist, desto höherwertig sind die Prämien die angeboten werden.
Es gibt zwei Arten von Prämien: Geldwert und Sach-Prämien. Geldwert steht für den Wert eines Gutscheins oder Bargeld. Sach-Prämien, die den Wert des Abonnements übersteigen, können mit einer Zuzahlung ausgewählt werden.

Ein Prämienbetrag besteht aus zwei getrennten Beträgen, von denen je nach Prämienart genau einer gesetzt ist; der andere ist leer:

| Betrag      | Prämienart          | Bedeutung                                                   |
| ----------- | ------------------- | ----------------------------------------------------------- |
| `Geldwert`  | Gutschein, Bargeld  | Kunde erhält Geld-/Gutscheinwert                            |
| `Zuzahlung` | Sachprämie          | Kunde zahlt Betrag zusätzlich; 0 bedeutet „Kein Betrag“     |

Beispiel:

| Prämie                | Prämienart | Geldwert | Zuzahlung |
| --------------------- | ---------- | -------: | --------: |
| Kaffeemaschine        | Sachprämie |     leer |   49,00 € |
| Best Choice-Gutschein | Gutschein  |  30,00 € |      leer |
| 40 € Bargeld          | Bargeld    |  40,00 € |      leer |
| Gratis-Kopfhörer      | Sachprämie |     leer |    0,00 € |

Die Zuzahlung begleicht der Prämienempfänger bei der Lieferung der Prämie per Nachnahme.

**Varianten:**
 * **Mein-Abo**: Ein Abonnement, bei dem der Seitenbesucher eine Zeitschrift für sich selbst auswählt. Der Abonnent ist Zeitschriftenempfänger, Rechnungsempfänger sowie Prämienempfänger. Die Abonnement-Formen unterscheiden sich anhand der Laufzeit. Einzelne Abonnement-Formen können mit einem zusätzlichen Rabatt versehen sein. Beim Mein-Abo ist nur eine Person involviert.
 * **Prämien-Abo**: Beim Prämien-Abo kann eine Person einen Zeitschriftenempfänger werben. Der Abonnent ist Prämienempfänger, der Zeitschriftenempfänger ist der Rechnungsempfänger und bezahlt das Abonnement. Beim Prämien-Abo gibt es immer zwei beteiligte Personen.
 * **Geschenk-Abo**: Das Geschenk-Abo ermöglicht es, dass eine Person einer anderen ein Zeitschriften-Abonnement schenkt. Der Abonnent ist Rechnungsempfänger und Prämienempfänger. Der Zeitschriftenempfänger erhält die Zeitschrift. Beim Geschenk-Abo gibt es immer zwei beteiligte Personen.

| Abo-Variante | Person 1    | Person 2    | Rechnungsempfänger? | Zeitschriftenempfänger? | Prämienempfänger?  |
| ------------ | ----------- | ----------- | ------------------- | ----------------------- | ------------------ |
| Mein-Abo     | Kunde       | —           | Kunde               | Kunde                   | Kunde              |
| Prämien-Abo  | Werber      | Geworbener  | Geworbener          | Geworbener              | Werber             |
| Geschenk-Abo | Schenkender | Beschenkter | Schenkender         | Beschenkter             | Schenkender        |

**Anbieter:**
Der Anbieter schließt den Abonnementvertrag mit dem Kunden. Unsere Anträge werden an den Anbieter (PVZ) weitergereicht. Die Antragsweitergabe ist nicht Teil dieser Spezifikation. Der Anbieter kümmert sich um die Auslieferung und die Verwaltung des Abonnements.

## 4. Fachliche Abläufe (Flows)

 * Auswahl der Zeitschrift, dann Abo-Form, dann Prämie
 * Auswahl der Abo-Form, dann Zeitschrift, dann Prämie
 * Direkteinstieg auf ein Bündelangebot (aus Zeitschrift und Prämie vorausgewählt). Das Bündelangebot kann besondere Abonnement-Bedingungen abbilden (z.B. nur 2 Ausgaben, 5 Ausgaben, 2 Monate, ...).

---

## 5. Geschäftsregeln (Business Rules)

 * Alle Bestellungen werden als Gastbestellung durchgeführt
 * Es kann nur per Rechnung oder Bankeinzug gezahlt werden
 * Für Bankeinzug kann ein Rabatt gewährt werden; Der Betrag ist standardmäßig 5 Euro
 * Es kann pro Auftrag nur ein Zeitschriften-Abo abgeschlossen werden

### BR-001 Angebotsausgaben
Berechnung der Angebotsausgaben:

1. `Zeitschrift.Ausgaben` wird durch 12 geteilt.
2. Das Ergebnis wird mit `Abonnement-Form.Mindestlaufzeit` multipliziert.
3. Das Resultat wird kaufmännisch auf eine ganze Zahl gerundet.

```
Formel: Angebotsausgabe = round((Zeitschrift.Ausgaben / 12) × Abonnement-Form.Mindestlaufzeit)
```

### BR-002 Angebotspreis
Der Angebotspreis ergibt sich aus den Angebotsausgaben multipliziert mit Zeitschrift.Einzelpreis, ggf. reduziert um einen Rabatt.

```
Formel: Angebotspreis = Angebotsausgabe x Zeitschrift.Einzelpreis x (1 - (Abonnement-Form.Rabatt / 100))
```

* Der Angebotspreis ist immer in Euro.
* Abonnement-Form.Rabatt reduziert den Gesamtpreis prozentual.
* Abonnement-Form.Rabatt ist ein Wert zwischen 0 und 100.
* Der berechnete Angebotspreis wird kaufmännisch auf zwei Nachkommastellen gerundet.

### BR-003 Regulärer Preis
Der reguläre Preis ergibt sich aus den Angebotsausgaben multipliziert mit Zeitschrift.Einzelpreis.

```
Formel: Regulärer Preis = Angebotsausgabe x Zeitschrift.Einzelpreis
```

* Der reguläre Preis ist immer in Euro.
* Der berechnete reguläre Preis wird kaufmännisch auf zwei Nachkommastellen gerundet.

### BR-004 Gesamtbetrag
Der Gesamtbetrag ergibt sich aus dem Angebotspreis abzüglich einem optionalen Rabatt für Bankeinzug. Eine eventuelle Zuzahlung zu einer Sachprämie wird separat ausgewiesen.

```
Formel: Gesamtbetrag = Angebotspreis - Rabatt für Bankeinzug
```

* Der Gesamtbetrag ist immer in Euro.
* Der Rabatt für Bankeinzug ist ein fixer Betrag pro Laufzeitumgebung, (Standardmäßig 5 Euro)

Der Gesamtbetrag darf nicht kleiner als 0 Euro sein. Ergibt die Berechnung einen negativen Wert, wird der Gesamtbetrag auf 0 Euro gesetzt.

### BR-005 Zahlungsrhythmus

Der Zahlungsrhythmus gibt dem Kunden Auskunft, in welchem Abstand eine Rechnung oder ein Bankeinzug fällig wird. Er wird unterschiedlich ermittelt. Je nachdem ob es sich um eine Abonnement-Form oder ein Bündelangebot handelt.

Bei einem Abonnement über eine Abonnement-Form ergibt sich der Zahlungsrhythmus durch das Feld Abonnement-Form.Mindestlaufzeit. Abonnement-Form.Mindestlaufzeit kann ausschließlich die Werte 3, 6, 12 oder 24 Monate annehmen.

| Mindestlaufzeit | Zahlungsrhythmus         |
| --------------- | ------------------------ |
| 3 Monate        | vierteljährlich          |
| 6 Monate        | halbjährlich             |
| 12 Monate       | jährlich                 |
| 24 Monate       | 2 Jahre, danach jährlich |

Bei einem Bündelangebot ist Bündelangebot.Laufzeit in Monaten immer gesetzt. Es bestimmt bei Zeitraum „Monate“ sowohl die Angebotslaufzeit als auch den anschließenden Abrechnungsrhythmus. Bei Zeitraum „Ausgaben“ bestimmt es den Abrechnungsrhythmus nach der vereinbarten Anzahl von Ausgaben.

Bei einem Bündelangebot mit Bündelangebot.Zeitraum = „Monate“ ergibt sich der Zahlungsrhythmus aus Bündelangebot.Laufzeit in Monaten.

| Laufzeit        | Zahlungsrhythmus |
| --------------- | ---------------- |
| 3 Monate        | vierteljährlich  |
| 6 Monate        | halbjährlich     |
| 12 Monate       | jährlich         |
| Sonstiges       | alle x Monate    |

Bei „alle x Monate“ ist x die Bündelangebot.Laufzeit in Monaten.

Bei einem Bündelangebot mit Bündelangebot.Zeitraum = „Ausgaben“ ist der Zahlungsrhythmus für das ursprüngliche Angebot „einmalig“. Nach Bündelangebot.Ausgaben Ausgaben erfolgt die weitere Abrechnung in dem durch Bündelangebot.Laufzeit in Monaten bestimmten Rhythmus gemäß obiger Tabelle.

Der ausgegebene und im Antrag festgeschriebene Zahlungsrhythmus enthält bei Zeitraum „Ausgaben“ beide Angaben. Beispiel bei 5 Ausgaben und Laufzeit in Monaten = 6: „einmalig. Nach 5 Ausgaben erfolgt die Abrechnung halbjährlich“.

Beispiel bei Zeitraum „Monate“ und Laufzeit in Monaten = 3: Der Zahlungsrhythmus lautet „vierteljährlich“; auch die anschließende Abrechnung erfolgt vierteljährlich.

### BR-006 Angebotsausgaben Bündelangebot
Die Angebotsausgaben eines Bündelangebots richten sich nach Bündelangebot.Zeitraum:

| Zeitraum | Angebotsausgaben |
| -------- | ---------------- |
| Monate   | `round((Zeitschrift.Ausgaben / 12) × Bündelangebot.Laufzeit in Monaten)`, kaufmännisch auf eine ganze Zahl gerundet |
| Ausgaben | `Bündelangebot.Ausgaben` |

Angebotspreis und regulärer Preis eines Bündelangebots werden mit diesen Angebotsausgaben nach BR-003 berechnet.

### BR-007 Bestellbarkeit prämienpflichtiger Kombinationen

Eine aktive Kombination aus Zeitschrift und prämienpflichtiger Abonnement-Form (Abonnement-Form.Rabatt = 0) muss mindestens eine auswählbare Hauptprämie besitzen. Eine Hauptprämie ist auswählbar, wenn:

1. die Prämie aktiv ist,
2. die Prämie der Abonnement-Form zugeordnet ist,
3. der Kombination Zeitschrift × Abonnement-Form eine Prämienbetragskategorie zugeordnet ist und
4. für die Prämie in dieser Prämienbetragskategorie ein gültiger Prämienbetrag existiert.

Bei der Stammdatenpflege werden Änderungen abgelehnt, die für eine Kombination aus aktiver Zeitschrift und aktiver prämienpflichtiger Abonnement-Form diese Voraussetzung verletzen würden. Das gilt insbesondere für Aktivierungen, Änderungen von Zuordnungen und Prämienbeträgen sowie das Entfernen oder Deaktivieren der letzten auswählbaren Hauptprämie. Das Fehlen einer auswählbaren Hauptprämie ist nur zulässig, solange die Zeitschrift oder die Abonnement-Form inaktiv ist; die Pflicht zur Prämienbetragskategorie bleibt unabhängig davon bestehen.

Für rabattbasierte Abonnement-Formen (Abonnement-Form.Rabatt > 0) gilt diese Voraussetzung nicht.

### BR-008 Mindestens eine Angebotsausgabe bei Standard-Abonnements

Für jede aktive Kombination aus Zeitschrift und Abonnement-Form muss die Berechnung nach BR-001 mindestens eine Angebotsausgabe ergeben. Die Stammdatenpflege lehnt Änderungen ab, die diese Voraussetzung verletzen würden. Dies wird insbesondere bei Zuordnung oder Aktivierung von Zeitschrift und Abonnement-Form sowie bei Änderungen von Zeitschrift.Ausgaben oder Abonnement-Form.Mindestlaufzeit geprüft. Inaktive Stammdaten dürfen zur Vorbereitung unvollständig sein.

### BR-009 Idempotente Antragseinreichung

Jede Einreichung eines Abonnement-Antrags muss einen nicht leeren, für die jeweilige beabsichtigte Antragstellung eindeutigen `Idempotency-Key`-Header enthalten. Diese Regel gilt für Standard- und Bündelangebot-Bestellungen gleichermaßen.

Bei der ersten erfolgreichen Einreichung wird der Schlüssel dauerhaft eindeutig der Antragsnummer und den fachlich normalisierten Eingabedaten zugeordnet.

* Wird derselbe Schlüssel mit fachlich identischen Eingabedaten erneut verwendet, wird das ursprüngliche erfolgreiche Ergebnis einschließlich Antragsnummer zurückgegeben; es wird kein weiterer Antrag angelegt.
* Wird derselbe Schlüssel mit abweichenden Eingabedaten erneut verwendet, wird die Einreichung mit „Idempotency-Key-Konflikt“ abgelehnt.
* Gleichzeitige Einreichungen mit demselben Schlüssel dürfen höchstens einen Antrag erzeugen.
* Für eine neue beabsichtigte Antragstellung muss ein neuer Schlüssel verwendet werden.

---

## 6. Abgrenzung (Nicht Teil des Geschäftsmodells)

* Kundenverwaltung
* Auftragsabwicklung
* Verwaltung des Abonnements (Kündigung, Auslieferung)
* Prämienversand
