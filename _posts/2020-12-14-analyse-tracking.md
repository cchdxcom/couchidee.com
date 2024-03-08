---
categories: ['Online-Marketing']
tags: ['Analytics']
title: 'Analyse und Tracking'
---

Mithilfe von Analysetools wie Google Analytics kannst Du allgemeine Informationen über deine Webseitenbesucher, sowie Inhalte und Aktionen auf deiner Webseite tracken. Google Analytics ist aufgrund der kostenfreien Nutzung am weitesten verbreitet. Aufgrund der Tatsache, dass Google einen großen Marktanteil in Deutschland besitzt, ist es auch ganz praktisch, dass Du gleich Daten zwischen Google Analytics, Google Search Console, Google Adwords usw. austauschen kannst. Für ganz große Projekte gibt es die kostenpflichtige Version Google Analytics 360.

**Unterschieden wird meist zwischen zwei verschiedenen Profilen. Das Nutzerprofil und das Sitzungsprofil sind die beiden elementaren Kenngrößen.**

Neben Google Analytics gibt es natürlich noch das Tracking-Tool-Matomo (ehemals Piwik), etracker, Webtrekk, Adobe, IBM, Econda und viele weitere.  
**Bemerkung:** Matomo lässt sich als "lokale Installation" sehr **datensparsam** konfigurieren.

Um Tracking auf deiner Webseite zu implementieren, ist es notwendig, dass Du ein paar Zeilen Javascript in deinen Quellcode einfügen kannst. Dieser wird dann auf jeder Webseite geladen und übermittelt an dein Tracking-Tool alle notwendigen Informationen. Hier solltest Du dich unbedingt mit den aktuellen Datenschutzverordnungen auseinandersetzen. Dinge wie IP-Anonymisierung müssen unbedingt umgesetzt werden.

### Ohne Ziele ist die Analyse planlos

Jede Webseite bzw. jede bestimmte Unterseite verfolgt einen bestimmten Zweck. Zumindest sollte sie das. Definiere Ziele und wann diese für dich erreicht sind.

**Beispiel:**

Nehmen wir an, Du hast für Produkt X eine Landingpage. Ziel könnte es sein, Anfragen über ein eingebundenes Formular zu erhalten -> Leads. Das Ziel der Seite ist also erreicht, wenn ein Besucher das Formular mit einer Anfrage abschickt. Wird das Ziel nicht erfüllt, solltest Du gewöhnlich Ursachenforschung betreiben.

Deine Ursachenforschung könnte so aussehen:

- Funktioniert das absenden des Formulars überhaupt?
- wird das Formular optimal gefunden?
- Forderst Du zu viele Daten?
- Fehlen Vertrauenserweckende Elemente?

Um spezifische Events wie Klicks auf bestimmte Elemente zu tracken ist es in der Regel notwendig, dass Du dies nachträglich konfigurierst bzw. implementieren musst.

## Analyse und Auswertungen

Wenn Du das Tracking auf deiner Seite implementiert hast, sammelst Du stetig neue Daten. Um diese zielgerichtet auszuwerten Bedarf einiger Einarbeitungszeit. Nachfolgend möchte ich Dir einen groben Überblick anhand der verfügbaren Auswertungen in Google Analytics geben.

### Grundlegende Begrifflichkeiten

- **Seitenaufrufe:** wie oft eine Seite angeklickt wurde. Auch mehrfache Besuche desselben Nutzers, gecachte und zwischengespeicherte Seiten werden gezählt.
- **Einzelne Seitenaufrufe:** Anzahl der Sitzungen, die diese Seite aufgerufen haben. Wird eine Seite während einer Sitzung mehrfach besucht, zählt sie in diesem Wert nur 1x.
- **Durchschnittliche Besuchszeit:** Zeit die ein Besucher auf dieser Seite verbracht hat (Differenz zwischen einem Seitenaufruf und dem nächsten )
- **Einstiege:** Sitzungen die auf dieser Seiten starten.
- **Absprungrate:** Verhältnis von Einstiegen zu Ausstiegen.
- **Ausstiege:** Anzahl der beendeten Sitzungen auf dieser Seite. Ein Ausstieg kann ein Klick zurück in die SERPs “Lösung nicht gefunden” oder auch ein “Lösung gefunden” und Tab geschlossen sein.
- **Seitenwert:** Für E-Commerce relevanter Wert - geht ein Kunde über diese Seite zum Kauf über, bekommt sie den entsprechenden Wert des Warenkorbs zugewiesen.

### Tracking mit Events

Mit Events kannst Du das Webseitentracking noch besser steuern und mehr Daten erfassen. Als Beispiele seien hier genannt:

- Downloads, Klicks auf Buttons / Links, Scrolltiefe u.v.m.

## Analyse URL-Tags

Um Kampagnen besser auszuwerten ist es notwendig, dass URLs mit Parametern ausgestattet werden. Meist ist nur so eine sauber Zuordnung möglich. Bei Google Analytics sind dies die 'utm_'-Parameter. Du musst nun aber nicht eigenhändig deine URL anpassen, nutze einen Generator für Kampagnen-URLs. ;)

[https://ga-dev-tools.appspot.com/campaign-url-builder/](https://ga-dev-tools.appspot.com/campaign-url-builder/){:target="_blank" rel="nofollow"}

### Mögliche Parameter:

- 'utm_source*': Quelle
- 'utm_medium*': Medium
- 'utm_campaign*': Eintrag im Kampagnenbericht
- 'utm_content': Gedacht für die jeweilige Variante des Werbemittels
- 'utm_term': Wenn Du Beispielsweise Adwords nutzt, kannst Du hier in deinem Link das getroffene Keyword bzw. den Suchbegriff mitgeben

‘*’ Werte müssen immer vorhanden sein, wobei 'utm_content' und 'utm_term' nicht zwingend erforderlich sind

**Beispiel-URL:**

'utm_source': werbeplattform.de  
'utm_medium': display  
'utm_campaign': digitalkampagne2020  
'utm_content': 1

Die zusammengesetzte URL lautet nun:

```conf
https://couchidee.com/produkt?utm_source=werbeplattform&utm_medium=display&utm_campaign=digitalkampagne2020&utm_content=1 
```

Wenn Du nun eine solche URL für deine Kampagne nutzt, erhältst Du genauere Werte und kannst deine Ziele besser kontrollieren.

Der Einsatz von URL-Tagging kann vielfältig eingesetzt werden:

Google Adwords, Anzeigennetzwerke, Social-Media, Mailing, Offline (via Weiterleitung) und QR-Codes