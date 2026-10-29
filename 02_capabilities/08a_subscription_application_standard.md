# Fähigkeit: Abonnement-Antrag für eine Standard-Bestellung einreichen

## Fachlicher Zweck

Ein Interessent soll ein Zeitschriften-Abonnement verbindlich beantragen können, indem er selbst eine Zeitschrift, eine Abonnement-Form und – sofern erforderlich – eine Hauptprämie auswählt. Optional kann zusätzlich eine Zugabe berücksichtigt werden.

Der Seitenbesucher kann dadurch:

* seine gewünschte Kombination aus Zeitschrift und Abonnement-Form verbindlich bestellen
* je nach Angebotsmodell eine Hauptprämie auswählen
* von einer zusätzlichen Zugabe profitieren, sofern diese für seinen Einstieg gültig ist

Hinweis: Für die Bestellung eines vordefinierten Bündelangebots siehe die Fähigkeit „Abonnement-Antrag für ein Bündelangebot einreichen".

## Fachliche Eingabe

* `Idempotency-Key`-Header (Pflicht; siehe BR-009)
* Abonnement-Form
* Zeitschrift
* Hauptprämie (sofern für das Angebotsmodell erforderlich oder zulässig)
* Einreichungsart „Standard-Bestellung“
* URL-Parameter-Wert (optional); daraus ermittelt das System die Zugabe
* Partner (optional, externe Partner-Id)
* Zahlungsart
* IBAN und Kontoinhaber (bei Zahlungsart Bankeinzug)
* Eine oder zwei beteiligte Personen mit Rollen, Anrede, Name, Firma (optional), Anschrift, E-Mail-Adresse (Pflicht beim Rechnungsempfänger und beim Zeitschriftenempfänger, sonst optional), Telefon (optional)

Zugabe, Laufzeit, Angebotsausgaben, Preise, Rabattbeträge, Zahlungsrhythmus und Prämienbetrag werden nicht vom Antragsteller angegeben, sondern vom System aus der gewählten Kombination ermittelt.

## Fachliches Ergebnis

Ein Abonnement-Antrag wird angelegt und erhält eine eindeutige, aufsteigende numerische Antragsnummer (beginnend bei 1, höchstens 9 Stellen; Lücken sind möglich).

Der Antrag hält die zum Zeitpunkt der Antragstellung gültigen Werte dauerhaft und unveränderlich fest (Wertfestschreibung, siehe Domäne Abonnement). Dazu gehören insbesondere:

* Variante (ergibt sich aus der gewählten Abonnement-Form)
* Partner und URL-Parameter-Wert
* Zeitschrift und Abonnement-Form
* Laufzeit und Angebotsausgaben
* Zahlungsrhythmus und Zahlungsart, bei Bankeinzug IBAN und Kontoinhaber
* Rabatt in Prozent
* Bankeinzug-Rabatt (ja/nein) und Bankeinzug-Rabattbetrag
* Regulärer Preis und Angebotspreis
* Hauptprämie mit Geldwert bzw. Zuzahlung, sofern vorhanden
* Zugabe und Zugabeprämie, sofern vorhanden
* Gesamtbetrag
* Beteiligte Personen mit ihren Rollen und Kontaktdaten

Nach erfolgreicher Einreichung befindet sich der Abonnement-Antrag im Status „Eingereicht".

Die Antwort enthält Antragsnummer, Status, Zeitpunkt und die ermittelten Werte (Angebot, Preise, Rabatte, Gesamtbetrag, Zahlungsart, Zahlungsrhythmus, Prämienzeilen), aber keine Personendaten und keine IBAN.

## Fachliche Regeln

* Werden bei einer Standard-Bestellung Angaben zu einem Bündelangebot übergeben, wird der Antrag abgelehnt (Einreichungsart passt nicht zu den Daten).
* Die gewählte Abonnement-Form muss aktiv sein.
* Die gewählte Zeitschrift muss aktiv sein.
* Die gewählte Zeitschrift muss für die gewählte Abonnement-Form zulässig sein.
* Die Variante des Antrags ergibt sich aus der gewählten Abonnement-Form.
* Laufzeit und Angebotsausgaben werden aus Abonnement-Form und Zeitschrift berechnet (BR-001).
* Die berechneten Angebotsausgaben müssen mindestens 1 betragen (BR-008).
* Der reguläre Preis wird nach BR-003 berechnet, der Angebotspreis nach BR-002.
* Der Zahlungsrhythmus ergibt sich aus Abonnement-Form.Mindestlaufzeit gemäß BR-005.
* Bei Zahlungsart Bankeinzug wird ein Bankeinzug-Rabatt berücksichtigt, sofern dieser für die Abonnement-Form zulässig ist (BR-004); die IBAN muss Format und Prüfziffer gemäß ISO 13616 erfüllen und aus einem Land des SEPA-Raums stammen.
* Eine Hauptprämie ist erforderlich, wenn das Angebotsmodell prämienpflichtig ist (Abonnement-Form.Rabatt = 0), und unzulässig, wenn es rabattbasiert ist (Abonnement-Form.Rabatt > 0).
* Eine gewählte Hauptprämie muss aktiv sein, der Abonnement-Form zugeordnet sein und für die aus Zeitschrift × Abonnement-Form ermittelte Prämienbetragskategorie einen Prämienbetrag besitzen; fehlt diese Zuordnung, ist die Kombination ungültig.
* Ist ein URL-Parameter-Wert angegeben, ermittelt das System die Zugabe nach den Regeln der Fähigkeit „Gültige Zugabe zu einem Einsprung ermitteln“ (URL-Parameter-Wert, Partner, Aktiv-Status, Gültigkeit zum Zeitpunkt der Antragstellung, aktive Abonnement-Form).
* Wird keine gültige Zugabe ermittelt, oder passt die ermittelte Zugabe nicht zur Bestellung, wird der Antrag mit „Zugabe ungültig“ abgelehnt. Die Zugabe passt zur Bestellung, wenn der Zugabe die gewählte Abonnement-Form zugeordnet ist und der Gültigkeitsbereich erfüllt ist: „Alle“ immer; „Ausgewählte Zeitschriften“, wenn die gewählte Zeitschrift hinterlegt ist; „Ausgewählte Prämien“, wenn die gewählte Hauptprämie hinterlegt ist. Das gilt auch, wenn wegen eines Rabatts keine Hauptprämie gewählt werden darf; in diesem Fall ist „Ausgewählte Prämien“ nie erfüllt.
* Ist kein URL-Parameter-Wert angegeben, enthält der Antrag keine Zugabe.
* Die Zugabeprämie wird mit Zuzahlung 0 und ohne Geldwert gespeichert.
* Partner ist optional; ist eine externe Partner-Id angegeben, die keinem Partner entspricht, wird kein Partner gespeichert.
* Ein Antrag muss ein bis zwei beteiligte Personen enthalten, deren Rollenverteilung zur Variante passt.
* Pflichtangaben je Person: Anrede, Vorname, Nachname, Straße, Hausnummer, Postleitzahl (5 Ziffern), Ort. Die E-Mail-Adresse ist beim Rechnungsempfänger und beim Zeitschriftenempfänger Pflicht.
* Bei Zahlungsart Bankeinzug sind IBAN und Kontoinhaber Pflicht; bei Zahlungsart Rechnung dürfen sie nicht angegeben werden, andernfalls „Antrag kann nicht eingereicht werden“.
* Ist die höchste Antragsnummer (999999999) erreicht, wird der Antrag mit „Antrag kann nicht eingereicht werden“ abgelehnt.
* Spätere Änderungen an Stammdaten (Zeitschrift, Abonnement-Form, Prämie, Preise) verändern einen bereits eingereichten Antrag nicht.
* Die Einreichungsart muss „Standard-Bestellung“ oder „Bündelangebot-Bestellung“ sein; fehlt sie oder ist sie unbekannt, wird der Antrag mit „Einreichungsart ungültig“ abgelehnt.
* Textangaben werden ohne führende und nachfolgende Leerzeichen gespeichert; eine Angabe, die danach leer ist, gilt als nicht angegeben.
* Keine beteiligte Person führt zu „Personenangaben unvollständig“; mehr Personen, als die Variante vorsieht, führen zu „Rollenverteilung ungültig“.
* Die Einreichung folgt BR-009: Wiederholungen mit demselben Idempotency-Key und identischen Daten liefern das ursprüngliche Ergebnis ohne einen weiteren Antrag; ein fehlender Schlüssel oder eine Wiederholung mit abweichenden Daten wird abgelehnt.

## Mögliche fachliche Ergebnisse

| Ergebnis                             | Beschreibung                                                                                   |
| ------------------------------------- | ------------------------------------------------------------------------------------------------ |
| Antrag eingereicht                   | Der Abonnement-Antrag wurde erfolgreich angelegt.                                                |
| Idempotente Wiederholung             | Das Ergebnis eines bereits erfolgreich eingereichten Antrags wird unverändert zurückgegeben.      |
| Idempotency-Key fehlt                | Der erforderliche Header fehlt oder ist leer.                                                    |
| Idempotency-Key-Konflikt             | Der Schlüssel wurde bereits mit abweichenden Eingabedaten erfolgreich verwendet.                 |
| Einreichungsart ungültig             | Die Einreichungsart passt nicht zu den übergebenen Daten (z. B. Angaben zu einem Bündelangebot).  |
| Abonnement-Form ungültig             | Die gewählte Abonnement-Form ist nicht aktiv oder nicht verfügbar.                                |
| Zeitschrift ungültig                 | Die Zeitschrift ist nicht aktiv oder mit der gewählten Abonnement-Form nicht kombinierbar.        |
| Hauptprämie fehlt                    | Für das prämienpflichtige Angebot ist eine Hauptprämie erforderlich.                              |
| Hauptprämie nicht zulässig           | Für das rabattbasierte Angebot darf keine Hauptprämie ausgewählt werden.                          |
| Hauptprämie ungültig                 | Die gewählte Hauptprämie ist nicht zulässig oder passt nicht zur Abonnement-Form.                 |
| Zugabe ungültig                      | Die gewählte Zugabe ist nicht gültig, nicht verfügbar oder passt nicht zum Einstieg.               |
| Zahlungsdaten unvollständig          | Für die gewählte Zahlungsart fehlen erforderliche Angaben.                                        |
| IBAN ungültig                        | Die IBAN erfüllt Format oder Prüfziffer nicht.                                                     |
| Personenangaben unvollständig        | Erforderliche Angaben zu den beteiligten Personen fehlen.                                          |
| Rollenverteilung ungültig            | Die angegebenen Personenrollen passen nicht zur ermittelten Variante.                              |
| Antrag kann nicht eingereicht werden | Der Antrag verletzt mindestens eine weitere fachliche Regel.                                       |

## Fachliche Qualitätsanforderungen

* Neu veröffentlichte und geänderte Prämien sollen zeitnah berücksichtigt werden.
* Änderungen an Abonnement-Formen und Preisen sollen zeitnah berücksichtigt werden.
* Die Antwort soll performant bereitgestellt werden.
* Ein eingereichter Antrag soll dauerhaft nachvollziehbar bleiben.
* Die im Antrag festgehaltenen Preise, Rabatte, Prämien, Prämienbeträge und Personendaten bleiben auch bei späteren Änderungen an Stammdaten unverändert erhalten.
* Die Berechnung des Antrags soll reproduzierbar und fachlich nachvollziehbar sein.
