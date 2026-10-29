# Fähigkeit: Abonnement-Antrag für ein Bündelangebot einreichen

## Fachlicher Zweck

Ein Interessent soll ein vordefiniertes Bündelangebot (Zeitschrift und Prämie bereits kombiniert) verbindlich beantragen können, ohne Zeitschrift, Abonnement-Form oder Hauptprämie einzeln auszuwählen.

Der Seitenbesucher kann dadurch:

* ein speziell zusammengestelltes Angebot einfach und schnell bestellen
* eine Zeitschrift auch kurzfristig ausprobieren

Hinweis: Für die freie Auswahl von Zeitschrift, Abonnement-Form und Hauptprämie siehe die Fähigkeit „Abonnement-Antrag für eine Standard-Bestellung einreichen".

## Fachliche Eingabe

* `Idempotency-Key`-Header (Pflicht; siehe BR-009)
* Einreichungsart „Bündelangebot-Bestellung“
* Bündelangebot
* URL-Parameter-Wert (optional; wird nur gespeichert)
* Partner (optional, externe Partner-Id)
* Zahlungsart
* IBAN und Kontoinhaber (bei Zahlungsart Bankeinzug)
* Genau eine beteiligte Person mit Rollen, Anrede, Name, Firma (optional), Anschrift, E-Mail-Adresse, Telefon (optional)

Zeitschrift, Laufzeit, Angebotsausgaben, Preise, Zahlungsrhythmus und Prämienbestandteile werden nicht vom Antragsteller angegeben. Sie ergeben sich vollständig aus dem gewählten Bündelangebot. Eine zusätzliche, freie Auswahl von Abonnement-Form, Zeitschrift oder Hauptprämie ist bei dieser Einreichungsart nicht vorgesehen.

## Fachliches Ergebnis

Ein Abonnement-Antrag wird angelegt und erhält eine eindeutige, aufsteigende numerische Antragsnummer (beginnend bei 1, höchstens 9 Stellen; Lücken sind möglich).

Der Antrag hält die zum Zeitpunkt der Antragstellung gültigen Werte dauerhaft und unveränderlich fest (Wertfestschreibung, siehe Domäne Abonnement). Dazu gehören insbesondere:

* Variante (bei Bündelangebot-Bestellung immer „Mein-Abo")
* Partner und URL-Parameter-Wert
* Bündelangebot und die daraus bestimmte Zeitschrift; die Abonnement-Form bleibt leer
* Laufzeit und Angebotsausgaben
* Zahlungsrhythmus und Zahlungsart, bei Bankeinzug IBAN und Kontoinhaber
* Regulärer Preis und Angebotspreis
* Bankeinzug-Rabatt (ja/nein) und Bankeinzug-Rabattbetrag
* Prämienbestandteile des Bündelangebots: Sachprämie mit Zuzahlung 0 und ohne Geldwert; Geldwert-Prämie mit Geldwert = Bündelangebot.Geldwert und ohne Zuzahlung
* Gesamtbetrag
* Beteiligte Person mit der Rolle und Kontaktdaten

Nach erfolgreicher Einreichung befindet sich der Abonnement-Antrag im Status „Eingereicht".

Die Antwort enthält Antragsnummer, Status, Zeitpunkt und die ermittelten Werte (Angebot, Preise, Rabatte, Gesamtbetrag, Zahlungsart, Zahlungsrhythmus, Prämienzeilen), aber keine Personendaten und keine IBAN.

## Fachliche Regeln

* Das gewählte Bündelangebot muss aktiv sein.
* Das Bündelangebot bestimmt Zeitschrift, Laufzeit, Angebotsausgaben, Preislogik und Zahlungsrhythmus; diese Werte dürfen durch den Antragsteller nicht überschrieben werden.
* Werden zusätzlich Abonnement-Form, Zeitschrift oder Hauptprämie übergeben, wird der Antrag fachlich abgelehnt (Einreichungsart passt nicht zu den Daten).
* Das Bündelangebot enthält eine Sachprämie, eine Geldwert-Prämie oder beides.
* Die Angebotsausgaben ergeben sich aus BR-006; der Angebotspreis und der reguläre Preis werden damit nach BR-003 berechnet.
* Der Zahlungsrhythmus ergibt sich gemäß BR-005. Bei Zeitraum „Ausgaben“ umfasst er den einmaligen Zahlungsrhythmus des Bündelangebots und den anschließenden, aus Bündelangebot.Laufzeit in Monaten ermittelten Abrechnungsrhythmus. Beide Angaben werden im Antrag festgeschrieben und ausgegeben.
* Bei Zahlungsart Bankeinzug wird ein Bankeinzug-Rabatt nur berücksichtigt, wenn dieser für das Bündelangebot zulässig ist; die IBAN muss Format und Prüfziffer gemäß ISO 13616 erfüllen und aus einem Land des SEPA-Raums stammen.
* Zugaben sind bei Bündelangeboten nicht vorgesehen. Ein angegebenes URL-Parameter-Wert wird gespeichert, es wird jedoch keine Zugabe ermittelt.
* Partner ist optional; ist eine externe Partner-Id angegeben, die keinem Partner entspricht, wird kein Partner gespeichert.
* Ein Antrag muss genau eine Person enthalten, deren Rollenverteilung zur Variante „Mein-Abo" passt.
* Pflichtangaben der Person: Anrede, Vorname, Nachname, Straße, Hausnummer, Postleitzahl (5 Ziffern), Ort, E-Mail-Adresse.
* Bei Zahlungsart Bankeinzug sind IBAN und Kontoinhaber Pflicht; bei Zahlungsart Rechnung dürfen sie nicht angegeben werden, andernfalls „Antrag kann nicht eingereicht werden“.
* Ist die höchste Antragsnummer (999999999) erreicht, wird der Antrag mit „Antrag kann nicht eingereicht werden“ abgelehnt.
* Spätere Änderungen an Stammdaten (Bündelangebot, Prämien, Preise) verändern einen bereits eingereichten Antrag nicht.
* Die Einreichungsart muss „Standard-Bestellung“ oder „Bündelangebot-Bestellung“ sein; fehlt sie oder ist sie unbekannt, wird der Antrag mit „Einreichungsart ungültig“ abgelehnt.
* Textangaben werden ohne führende und nachfolgende Leerzeichen gespeichert; eine Angabe, die danach leer ist, gilt als nicht angegeben.
* Keine beteiligte Person führt zu „Personenangaben unvollständig“; mehr Personen, als die Variante vorsieht, führen zu „Rollenverteilung ungültig“.
* Die Einreichung folgt BR-009: Wiederholungen mit demselben Idempotency-Key und identischen Daten liefern das ursprüngliche Ergebnis ohne einen weiteren Antrag; ein fehlender Schlüssel oder eine Wiederholung mit abweichenden Daten wird abgelehnt.

## Mögliche fachliche Ergebnisse

| Ergebnis                             | Beschreibung                                                                             |
| ------------------------------------- | ------------------------------------------------------------------------------------------ |
| Antrag eingereicht                   | Der Abonnement-Antrag wurde erfolgreich angelegt.                                          |
| Idempotente Wiederholung             | Das Ergebnis eines bereits erfolgreich eingereichten Antrags wird unverändert zurückgegeben. |
| Idempotency-Key fehlt                | Der erforderliche Header fehlt oder ist leer.                                             |
| Idempotency-Key-Konflikt             | Der Schlüssel wurde bereits mit abweichenden Eingabedaten erfolgreich verwendet.          |
| Bündelangebot ungültig               | Das Bündelangebot ist nicht aktiv oder für die Bestellung nicht zulässig.                  |
| Antrag enthält unzulässige Angaben   | Es wurden zusätzlich Abonnement-Form, Zeitschrift oder Hauptprämie übergeben.               |
| Zahlungsdaten unvollständig          | Für die gewählte Zahlungsart fehlen erforderliche Angaben.                                 |
| IBAN ungültig                        | Die IBAN erfüllt Format oder Prüfziffer nicht.                                              |
| Personenangaben unvollständig        | Erforderliche Angaben zur beteiligten Person fehlen.                                        |
| Rollenverteilung ungültig            | Die angegebenen Personenrollen passen nicht zur Variante „Mein-Abo".                        |
| Antrag kann nicht eingereicht werden | Der Antrag verletzt mindestens eine weitere fachliche Regel.                                |

## Fachliche Qualitätsanforderungen

* Änderungen an Bündelangeboten und Preisen sollen zeitnah berücksichtigt werden.
* Die Antwort soll performant bereitgestellt werden.
* Ein eingereichter Antrag soll dauerhaft nachvollziehbar bleiben.
* Die im Antrag festgehaltenen Preise, Prämien und Personendaten bleiben auch bei späteren Änderungen an Stammdaten unverändert erhalten.
* Die Berechnung des Antrags soll reproduzierbar und fachlich nachvollziehbar sein.
