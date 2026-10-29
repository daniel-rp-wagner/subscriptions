# Domäne: Abonnement

## Abonnement-Form

**Beschreibung:**

Zeitschriften können entweder über verschiedene Zeiträume selbst bezogen werden, vermittelt durch einen Werber oder als Geschenk für einen Dritten. Dies wird über die Abonnement-Formen abgebildet. Eine Abonnement-Form ist entweder prämienpflichtig oder rabattbasiert.

**Eigenschaften:**

| **Bezeichnung**       | **Hinweis**                                                                      | **Beispiel**     |
| --------------------- | -------------------------------------------------------------------------------- | ---------------- |
| Name                  |                                                                                  | 3-Monats-Abo     |
| Aktiv                 | Kennzeichnet, ob die Abonnement-Form derzeit verwendet werden kann               | ja               |
| Reihenfolge           | aufsteigend numerisch                                                            | 1                |
| Kurzbeschreibung      |                                                                                  |                  |
| Langbeschreibung      |                                                                                  |                  |
| Variante              | Kennzeichnet die Abonnement-Variante¹                                            | Mein-Abo         |
| Mindestlaufzeit       | in Monaten; einer der Werte 3, 6, 12, 24                                         | 12               |
| Rabatt                | in Prozent, ganzzahlig 0–100; Angebotsmodell abgeleitet: 0 = prämienpflichtig, > 0 = rabattbasiert | 30               |
| Rabatt für Bankeinzug | ja/nein                                                                          | nein             |

¹ **Hinweis**: einer der Werte: _Prämien-Abo, Mein-Abo, Geschenk-Abo_

**Beziehungen:**

- Jeder Abonnement-Form können verschiedene Prämien zugewiesen sein (n:m).
- Jeder Abonnement-Form sind verschiedene Zeitschriften zugewiesen (n:m).

## Abonnement-Antrag

**Beschreibung:**

Ein Abonnement-Antrag repräsentiert den Wunsch eines Interessenten, ein Zeitschriften-Abonnement abzuschließen. Er enthält die zum Zeitpunkt der Antragstellung gültigen Informationen über das gewählte Angebot, die Laufzeit, die Zahlungsweise, die ausgewählten Prämien sowie die am Abonnement beteiligten Personen. Die spätere Prüfung, Weitergabe und Umwandlung in ein verwaltetes Abonnement ist nicht Teil der ersten Version. Der Antrag wird zunächst nur im Status „Eingereicht“ gespeichert.

**Wertfestschreibung:** Ein Abonnement-Antrag hält alle für ihn relevanten Werte (Preise, Rabatte, Prämien, Prämienbeträge, Zahlungsrhythmus und Personendaten) zum Zeitpunkt der Antragstellung dauerhaft und unveränderlich fest. Spätere Änderungen an Stammdaten wie Zeitschrift, Prämie, Bündelangebot oder Preisen wirken sich nicht auf einen bereits eingereichten Antrag aus. Referenzen auf Stammdaten werden ohne Fremdschlüssel gespeichert, sodass Stammdaten gelöscht werden können, ohne den Antrag zu verändern. Zu Zeitschrift, Abonnement-Form, Bündelangebot und Zugabe werden jeweils Id und Name gespeichert, zum Partner die externe Id.

**Eigenschaften:**

| **Bezeichnung**            | **Hinweis**                                                                      | **Beispiel**  |
| -------------------------- | -------------------------------------------------------------------------------- | ------------- |
| Antragsnummer              | eindeutig, aufsteigend numerisch; höchstens 9 Stellen (max. 999999999);          | 16352642      |
| Datum                      | Zeitpunkt der Antragstellung (Datum und Uhrzeit, gespeichert in UTC)             | 01.03.2025 14:12 |
| Einreichungsart            | Standard-Bestellung oder Bündelangebot-Bestellung                                | Standard-Bestellung |
| Variante                   | aus der Abonnement-Form; bei Bündelangebot-Bestellung immer Mein-Abo             | Prämien-Abo   |
| Partner.Externe Id         | Referenz auf einen Partner; optional                                             | 4711          |
| URL-Parameter-Wert         | URL-Parameter-Wert des Einsprungs; optional, bei beiden Einreichungsarten gespeichert | 253037      |
| Abonnement-Form            | Id und Name; bei Standard-Bestellung; leer bei Bündelangebot-Bestellung          | Prämien-Abo   |
| Bündelangebot              | Id und Name; bei Bündelangebot-Bestellung                                        | Sommeraktion  |
| Zugabe                     | Id und Name; optionale Zugabe; nur bei Standard-Bestellung                       | + Kopfhörer   |
| Zahlungsart                | Bankeinzug oder Rechnung                                                         | Bankeinzug    |
| Zahlungsrhythmus           | BR-005; bei Bündelangebot mit Zeitraum „Ausgaben“ einschließlich des Hinweises zur anschließenden Abrechnung | jährlich |
| IBAN                       | nur bei Bankeinzug erforderlich⁷                                                 | DE12…         |
| Kontoinhaber               | nur bei Bankeinzug erforderlich; Freitext, max. 100 Zeichen                      | Max Mustermann |
| Zeitschrift                | Id und Name der gewählten bzw. vom Bündelangebot bestimmten Zeitschrift          | GARTEN        |
| Erscheinungsweise          | monatlich, wöchentlich usw.                                                      | monatlich     |
| Laufzeit                   | Eine Zahl für Monate oder Ausgaben                                               | 12            |
| Laufzeit-Einheit           | Monate oder Ausgaben²                                                            | Monate        |
| Angebotsausgaben           | BR-001 bzw. bei Bündelangebot BR-006                                             | 12            |
| Regulärer Preis            | BR-003                                                                           | 119.88        |
| Angebotspreis              | BR-002 bzw. bei Bündelangebot BR-003                                             | 119.88        |
| Rabatt                     | Rabatt in Prozent aus der Abonnement-Form; leer bei Bündelangebot-Bestellung     | 30            |
| Rabatt für Bankeinzug      | ja, wenn Zahlungsart Bankeinzug und Abonnement-Form bzw. Bündelangebot den Rabatt zulassen; sonst nein | nein          |
| Bankeinzug-Rabattbetrag    | konfigurierter fixer Betrag gemäß BR-004, sofern angewendet, auch wenn der Gesamtbetrag auf 0 begrenzt wird; sonst leer | 5.00          |
| Gesamtbetrag               | Gesamtpreis des Abonnements (BR-004)                                             | 89.90         |
| Status                     | Bearbeitungszustand des Antrags¹                                                 | Eingereicht   |

¹ **Hinweis**: vorerst nur der Wert: _Eingereicht_. Kann optional später erweitert werden um andere Status.  
² **Hinweis**: Standard-Bestellung: Monate (= Abonnement-Form.Mindestlaufzeit). Bündelangebot-Bestellung: gemäß Bündelangebot.Zeitraum; bei „Monate“ ist die Laufzeit Bündelangebot.Laufzeit in Monaten, bei „Ausgaben“ ist sie Bündelangebot.Ausgaben. Bei Bündelangeboten mit Zeitraum „Ausgaben“ wird der aus Bündelangebot.Laufzeit in Monaten ermittelte Abrechnungsrhythmus nach den vereinbarten Ausgaben im Zahlungsrhythmus des Antrags festgeschrieben (BR-005).

⁷ **Hinweis**: ISO 13616, nur SEPA-Länder (Länge gemäß IBAN-Register); normalisiert (Großbuchstaben, ohne Leerzeichen)

### Prämie

| **Bezeichnung**         | **Hinweis**                                                  | **Beispiel**  |
| ----------------------- | ------------------------------------------------------------ | ------------- |
| Herkunft                | Herkunft der Prämienzeile⁶                                   | Hauptprämie   |
| Id                      | Referenz auf die gewählte Prämie                             | 123           |
| Name                    | Name der Prämie zum Zeitpunkt der Antragstellung             | Apple AirPods |
| Art                     | Ausprägung³                                                  | Sachprämie    |
| Geldwert                | Geldwert bei Gutschein/Bargeld; sonst leer                   | 30.00         |
| Zuzahlung               | Zuzahlung bei Sachprämie (0 = „Kein Betrag“); sonst leer     | 29.90         |

³ **Hinweis**: einer der Werte: _Sachprämie, Bargeld, Gutschein_.  
⁶ **Hinweis**: einer der Werte: _Hauptprämie, Zugabeprämie, Bündelangebot-Sachprämie, Bündelangebot-Geldwertprämie_. Je Antrag gibt es jede Herkunft höchstens einmal.

Werte der Prämienzeilen je Herkunft:

| Herkunft                               | Geldwert                    | Zuzahlung                          |
| -------------------------------------- | --------------------------- | ---------------------------------- |
| Hauptprämie (Gutschein/Bargeld)        | Prämienbetrag.Geldwert      | leer                               |
| Hauptprämie (Sachprämie)               | leer                        | Prämienbetrag.Zuzahlung            |
| Zugabeprämie (immer Sachprämie)        | leer                        | 0                                  |
| Bündelangebot: Sachprämie              | leer                        | 0                                  |
| Bündelangebot: Geldwert-Prämie         | Bündelangebot.Geldwert      | leer                               |

### Beteiligte Person

| **Bezeichnung** | **Hinweis**                         | **Beispiel**                            |
| --------------- | ----------------------------------- | --------------------------------------- |
| Rollen          | Rollen der Person⁴                  | Prämienempfänger                        |
| Anrede          | Pflicht⁵                            | Herr                                    |
| Vorname         | Pflicht; max. 100 Zeichen           | Max                                     |
| Nachname        | Pflicht; max. 100 Zeichen           | Mustermann                              |
| Firma           | optional; max. 100 Zeichen          | Mustermann GmbH                         |
| Straße          | Pflicht; max. 100 Zeichen           | Musterstraße                            |
| Hausnummer      | Pflicht; max. 10 Zeichen            | 1b                                      |
| Postleitzahl    | Pflicht; 5 Ziffern                  | 12345                                   |
| Ort             | Pflicht; max. 100 Zeichen           | Musterstadt                             |
| E-Mail-Adresse  | Pflicht beim Rechnungsempfänger und beim Zeitschriftenempfänger, sonst optional; Format E-Mail, max. 254 Zeichen | [max@example.de](mailto:max@example.de) |
| Telefon         | optional; max. 30 Zeichen aus Ziffern, Leerzeichen und `+ / ( ) -` | 0781 123456                             |

⁴ **Hinweis**: einer oder mehrere der Werte: _Zeitschriftenempfänger, Prämienempfänger, Rechnungsempfänger_. Die Rollen einer Person werden in einer eigenen Zuordnung gespeichert. Die zulässige Rollenverteilung ergibt sich aus der Variante des Antrags. Nur beim Mein-Abo besitzt eine Person alle drei Rollen.  
⁵ **Hinweis**: einer der Werte: _Herr, Frau, Divers_

**Beziehungen:**

* Ein Abonnement-Antrag besitzt genau eine Einreichungsart: Standard-Bestellung oder Bündelangebot-Bestellung. Beide Einreichungsarten werden über denselben Einreichungsweg mit Angabe der Einreichungsart übermittelt.
* Bei Standard-Bestellungen bezieht sich der Antrag auf genau eine Abonnement-Form und genau eine Zeitschrift.
* Bei Bündelangebot-Bestellungen bezieht sich der Antrag auf genau ein Bündelangebot. Die Abonnement-Form bleibt leer, die Variante ist Mein-Abo. Zeitschrift, Prämien, Laufzeit, Angebotsausgaben, Preise und Zahlungsrhythmus werden aus dem Bündelangebot ermittelt und als Snapshot gespeichert.
* Ein Antrag kann eine Hauptprämie enthalten, sofern sie für die Einreichungsart und das Angebotsmodell zulässig oder erforderlich ist.
* Angebotsmodell: `Abonnement-Form.Rabatt = 0` ⇒ prämienpflichtig (Hauptprämie Pflicht); `Abonnement-Form.Rabatt > 0` ⇒ rabattbasiert (Hauptprämie verboten).
* Ein Antrag kann eine Zugabeprämie enthalten, sofern eine gültige Zugabe angewendet wurde.
* Ein Antrag enthält mindestens eine und höchstens zwei beteiligte Personen. Die Rollenverteilung ergibt sich aus der Variante.
* Partner ist optional; wenn eine externe Partner-Id angegeben ist und dieser Partner nicht existiert, wird kein Partner gespeichert.
* Der Snapshot wird als Antragskopf mit Kinddatensätzen für beteiligte Personen (inkl. ihrer Rollen) und Prämienzeilen gespeichert; Snapshot-Felder sind denormalisiert und unveränderlich.
