---
categories: ['Online-Marketing']
tags: ['SEO']
title: 'SEO-Grundlagen URLs und Statuscodes'
---

Als URL (Uniform Resource Locator) bezeichnet man die Adresse einer Ressource. Ressourcen können Textdokumente, Bilder, Videos und vieles mehr sein.

### Beispiel-URL

**https://www.couchidee.com/seo/onpage&seite=1**

- 'https' als Protokoll sollte dem normalen “http” immer vorgezogen werden. Auch weil Suchmaschinen das (veraltete) http negativ beurteilen.
- 'www' als Subdomain ist meistens standardmäßig ausgewählt. Die Version ohne www, also z.B. https://couchidee.com kannst Du aber ebenso problemlos nutzen.
- 'couchidee.com' ist die Domain. Dies könnte natürlich ebenso .de, .net usw. sein
- 'seo' ist (Unter-)Verzeichnis, in welchem sich dann entweder weitere Unterverzeichnisse oder die zugehörigen Artikel befinden.
- 'onpage' oder auch bspw. “onpage.html” ist letztendlich der Name des Dokuments.
- '&seite=1' um bestimmte Parameter an eine Seite zu übergeben

Alle Inhalte die über eine statische und eindeutige URL erreichbar sind, werden von Suchmaschinen gecrawlt. Ob der Inhalt der URL in den SERPs auftaucht bzw. in den Suchmaschinenindex aufgenommen werden soll, lässt sich mittels des Meta-Tags “noindex” festlegen.

Eine Fehlkonfiguration kann auch unbeabsichtigt zu vermehrtem duplicate-Content führen. Häufig ist hier das http- bzw. https-Protokoll oder das fehlende canonical-Tag schuld. Denn auch minimale Abweichungen der URL sind immer als neues Dokument anzusehen.

URLs sollten, wenn möglich, immer gleich bleiben und sich nicht ändern. Ist eine URL-Änderung jedoch unumgänglich, müssen die betroffenen Dokumente mittels 301-.htaccess-Konfiguration umgeleitet werden. 301-Redirects sind aus Suchmaschinen- und Nutzersicht die beste Lösung.

**Wissenswertes zur Gestaltung der URL**

- Bindestrich statt Leerzeichen
- Sonderzeichen und Umlaute vermeiden  
  - Kategorien und Gruppierungen sollten immer auch in der URL abgebildet werden
  - Google Search Console auf Verzeichnisebene einrichten
  - Monitoring und Analyse leichter
- Die URL sollte möglichst selbsterklärend sein z.B.: Hauptverzeichnis->Unterverzeichnis->Dokument

### HTTPS - SSL-Verschlüsselung

- Umstellungen von http- zu https-Seiten sollten mit dem 301-Redirect umgeleitet werden Würden beide URLs gleichermaßen bereitgestellt werden, wären beiden von Suchmaschinen als Duplikate betrachtet werden.
- Ebenso müssen alle Meta-Tags, Links usw. anschließend auf https-Version geändert werden.
- Bilder / Videos bzw. allgemeine Downloads und Ressourcen sollten immer per https ausgeliefert werden

In der Kommunikation zwischen Client und Server gibt es die http-Statuscodes. Mit diesen Statuscodes kann dem jeweiligen Crawler einer Suchmaschine übermittelt werden, wie dieser mit der URL umzugehen hat. Ein paar geläufige Statuscodes sind:

### Statuscodes und ihre Bedeutung

- **200 “Ok”** - Das Dokument ist erreichbar und könnte gecrawlt werden
- **404 “not found”** - gelöschte oder nicht existierende Inhalte, die aus dem Index entfernt werden können
- **410 “gone”** - dauerhaft entfernt, URL soll dauerhaft aus dem Index entfernt werden
- **301 “moved permanently”** - Das Dokument bzw. die Ressource ist verschoben worden und steht nun unter einer anderen URL zur Verfügung. Die alte URL ist ungültig und soll aus dem Index entfernt werden.
- **302 “found"** - Moved temporarily” Das Dokument bzw. die Ressource ist aktuell unter der neuen URL zu finden. Die alte URL soll aber weiterhin indexiert bleiben.