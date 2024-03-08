---
categories: ['Online-Marketing']
tags: ['SEO']
title: 'Verlinkung, Crawling und Indexierung'
---

Content und alle Informationen drumherum erstellen wir für die Besucher unserer Webseiten. Deshalb muss Inhalt, der auch gelesen werden soll, gut und einfach durch Besucher und Suchmaschinen auffindbar sein. Unter Beachtung von ein paar einfachen Richtlinien sollte es funktionieren:

### Themencluster

Sobald Du zu einem Thema viele Inhalte für deine Webseitenbesucher anbietest, kann es sinnvoll sein, sogenannte Themenseiten zu erstellen. Man spricht oft auch von hollistischen Seiten. Diese verhelfen deinem Besucher zu einer besseren Orientierung und Suchmaschinen, den Kontext noch besser zu verstehen. Hierbei verlinkst Du von einer “umfangreichen” Seite, auf der Du alle Inhalte eingehst, immer im entsprechenden Abschnitt auf deinen “detaillierteren” Beitrag.

### starke interne Verlinkung

Anhand der internen Linkgraphen, welcher die beispielsweise die Verlinkungen von Unterseiten zählt, bewerten Suchmaschinen die jeweilige Seite. Es wird angenommen, je mehr Verlinkungen zu einer Unterseite existieren, desto wichtiger ist sie.

### Aussagekräftige Linkbeschriftung

Wenn möglich solltest “nichtssagende” Linkbezeichnungen wie “weiter” oder “hier” vermeiden. Das werden dir nicht nur deine Webseitenbesucher sondern auch Suchmaschinen danken.

### geringe Klicktiefe

Wichtige Seite sollten möglichst über die Startseite aufrufbar sein oder zumindest weit oben in der Webseitenstruktur angesiedelt werden. Beginnend von der Startseite, solltest Du immer auf die Besucherperspektive achten.

## Mobile & AMP

### responsive Design

In Zeiten, in denen bestimmte Zielgruppe nahezu ausschließlich mobil auf unsere Webseiten zugreifen, müssen diese auch dementsprechend optimiert sein. Optimiert bedeutet, dass Inhalte nicht unbedingt nur einfach ordentlich anzusehen sind, sondern mobile Seiten auch eine andere Haptik aufweisen können als die Desktop-Version.

Responsives Design heißt auch, dass deine Webseite auf das jeweilige Endgerät und dessen Auflösung reagiert sowie den Inhalt an die jeweiligen Bedingungen anpasst. Vor Allem solltest Du auf eine schnelle Ladezeit und bequeme Bedienung achten.

### Google AMP - Accelerated Mobile Pages

AMP-Seiten sind sehr schnell ladende Webseiten. Im Gegensatz zu “normalen” mobilen Seiten, ist der Funktionsumfang von AMP-Seiten stark eingeschränkt. Zudem müssen alle Inhalte auf Google Servern gecacht werden.

### Mobile First Index

Es ist eine Tatsache, dass immer mehr Menschen über mobile Endgeräte ein Suche über Google starten. Deshalb hat die Suchmaschinen den relevanten Index von Desktop auf Mobile umgestellt. Was bedeutet, dass die mobile Version deiner Webseite für die Ermittlung des Rankings herangezogen wird.

**Mobile First Index = bezieht sich auf Inhalt deiner Webseite - stelle sicher, dass Inhalte auch tatsächlich für mobile Endgeräte verfügbar sind.**

**Mobile Friendliness** = ist deine Webseite für mobile Geräte optimiert, rankst deine Seite besser.

## Crawling und Indexierung

Wie oft deine Webseite bzw. einzelne Resourcen gecrawlt werden, kannst Du nur bedingt beeinflussen (siehe [Google SearchConsole](https://www.google.com/webmasters/tools/settings){:target="_blank" rel="nofollow"}). Letztendlich entscheidet dies ein Algorithmus. Dokumente und Ressourcen mit veralteten oder nicht aktualisierten Inhalten werden seltener gecrawlt als jene, die häufige Update erfahren. So z.B. Blogs & Co.

Mit dem zur Verfügung stehenden Crawling-Budget für deine Webseite solltest Du sorgsam umgehen. Denn dieser Wert ist nicht bekannt. Es wird je nach Aktualität des Contents, Seitengröße und anderer Parameter zugeteilt.

Mithilfe der gecrawlten Daten erstellt die Suchmaschine einen Index der mit weiteren Informationen angereichert wird. Welche Keywords kommen wie oft vor, wie ist die interne Verlinkung usw. Daraus wird nun die Relevanz für einzelne URLs zu bestimmten Suchanfragen abgeleitet.

Für Suchergebnisse und z.B. dynamische Paginierungsseiten solltest Du die Indexierung und das Crawling unterbinden.

### Crawling

Wichtig ist, dass alle wichtigen Ressourcen gecrawlt und indexiert werden können. Das crawling kann stattfinden, wenn die Ressource in einem für Suchmaschinen lesbaren Format vorliegt. Bei Technologien wie Flash kann es zu Problemen kommen.

### Indexierung

Solange Du das Indexieren nicht explizit mit dem Meta-Tag “noindex” verbietest, wird die Suchmaschinen den Inhalt in seinen Index aufnehmen.

### Beeinflussung von Crawling & Indexierung

Unter Umständen sollen Inhalte nicht indexiert werden. Dies betrifft z.B. Seiten mit wenig Inhalten, Doppelte Inhalte wie Druckversionen oder auch Suchergebnisse und Paginierungsseiten (sehr häufig bei Blogs) usw.

### Crawling

### Die robots.txt

Diese Textdatei ist zuständig für die Steuerung des Crawling. Einfach im Root-Verzeichnis deiner Domain ablegen und sie gibt den Crawlern der Suchmaschinen einfache Anweisungen. Wenn Du sie nicht erstellst, werden Suchmaschinen ausnahmslos alles was lesbar ist crawlen.

### Beispiele für Anweisungen und deren Bedeutung

- 'User-Agent:*' Folgende Angabe gilt für alle Bots
- 'Disallow: /verzeichnisname/' Verhindert das Crawling des Verzeichnisses
- 'Disallow: *?parameter' Verhindert das Crawling von Seiten mit dem angegebenen Parameter
- 'Disallow: /bestimmte-datei.html' nur diese eine Datei wir nicht gecrawlt
- 'Disallow: /bilder/bild.jpg' nur dieses Bild wird nicht gecrawlt
- 'Disallow: /*.jpg$' Alle .jpg-Bilder werden vom Crawling ausgeschlossen
- 'Disallow: /bilder*/' alle Unterverzeichnisse, die mit “bilder” beginnen, werden nicht gecrawlt
- 'Disallow: /bilder/' alle Unterverzeichnisse, die “bilder” enthalten, werden nicht gecrawlt
- 'Allow: /bilder/opensource/' das Verzeichnis “opensource” darf gecrawlt werden (auch wenn der Ordner “bilder” ausgeschlossen wurde)

### Ein Beispiel könnte so aussehen:

```conf
User-agent: googlebot
Disallow: /verzeichnisname/
```

### Indexierung und Umgang mit Duplicate Content

Prinzipiell solltest Du duplicate-Content vermeiden. Lässt es sich beispielweise bei Kampagnen nicht vermeiden, verwende das Meta-Tag “canonical”.

```conf
# Beispiel
https://www.domain.com/verzeichnis
https://www.domain.com/verzeichnis?kampagne=4
```

Der Inhalt beider URLs ist identisch. Deshalb ist es sinnvoll, die zweite URL mit dem canonical-Tag auszuzeichnen.

```html
<link rel="canonical" href="https://www.domain.com/verzeichnis">
```

**Veraltete Inhalte und Seiten ohne Nutzen für den User**

Sollen Seiten erst gar nicht im Suchmaschinenindex landen oder ausgeschlossen werden, so lässt sich dies mit dem Meta-Tag “robots” einrichten.

```html
<meta name="robots" content="noindex, follow">
```

Bei veralteten Seiten hilft es, einen **301-Redirect** zur (wenn vorhanden) aktuellen Seite oder Verzeichnis zu setzen. Somit wird die Seite ebenfalls aus dem Index entfernt. Ist dies nicht möglich, so bieten sich der ein 404er oder 410er an - siehe Statuscodes.

Um einen aktuellen Status deiner indexierten Seiten zu bekommen, solltest Du die entsprechenden Tools der Suchmaschinen nutzen. Beispielsweise die [Google Search Console](https://search.google.com/search-console){:target="_blank" rel="nofollow"} oder auch die [Bing Webmaster Tools](https://www.bing.com/webmasters/homepage){:target="_blank" rel="nofollow"}.

### XML-Sitemap

Mithilfe einer XML-Sitemap kannst Du Seiten die gecrawlt und indexiert werden sollen, in einer Datei sammeln. Gerade bei großen und umfangreichen Seiten ist dies zu empfehlen. Hierbei solltest Du aber darauf achten, die XML-Sitemap immer zu aktualisieren, sobald Du relevante Seiten zu deiner Webseite hinzufügst. Die XML kannst Du nun bequem in den jeweiligen Tools der Suchmaschinen registrieren.