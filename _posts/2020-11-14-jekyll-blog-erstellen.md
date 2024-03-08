---
categories: ['Webentwicklung']
tags: ['Jekyll', 'Static File CMS', 'Blog']
title: 'Jekyll Blog erstellen'
---

Schon bei der Grundinstallation legt Jekyll einen  `_posts`-Ordner an. Alle Markdown-Dateien werden entsprechend als Blogartikel geparst.

Erstelle dir am Besten zuerst einen kleinen Demo-Artikel. Ein einfaches Beispiel, wie ein Blogartikel bei Jekyll von mir aussieht:

```conf
---
layout: post
title: Titel des Blogs
date: 2019-12-15 08:00:00 + 0100
author: Max Mustermann
categories: Webentwicklung
robots: index, follow
description: Hier steht eine Beschreibung.
---
## Beispielüberschrift

Hier könnte dein Text stehen...
```
**WICHTIG**
Du musst die Markdown-Files immer mit einem Datum versehen. Der Aufbau sieht z.B. wiefolgt aus: `2020-11-14-jekyll-blog-erstellen.md`. Würdest du deine Beiträge nur mit Namen wie z.B. `jekyll-blog-erstellen.md` benennen, werden deine angelegten Dateien nicht angezeigt.

Im obigen Beispiel siehst Du  `layout:post`. Im Parameter layout gibst Du an, welches Layout verwendet werden soll. In diesem Fall natürlich das Blogpost-Layout, kurz  `post`. Wenn also  `post.html`  unter  `_layouts`  deines Jekyll-Projekts noch nicht vorhanden ist, so lege es an. Das Design deines Blogbeitrags richtet sich nach deinem Template. Um den Blogbeitrag anzuzeigen benötigst Du nur:

```liquid
{% raw %}
Content-Tag: {{ content }}
{% endraw %}
```

## Blogseite mit Artikelliste

Nachdem Du nun erstmal einen Testbeitrag und das zugehörige Layout erstellt hast , fehlt nun noch eine Blog-Seite die alle Beiträge auflistet. Hierzu hab ich mir im  `root`Verzeichnis einfach einen Ordner namens  `blog`  angelegt und eine  `index.html`  darin erstellt. Das Layout richtet sich natürlich wieder nach deinem Template, aber eine grundlegende Funktionalität erreichst Du mit folgendem Code.

```liquid
{% raw %}
{% for post in paginator.posts %}

<h1>{{ post.title }}</h1>
<p>{{ post.date | date_to_string }}</p>
<p>{{ post.author }}</p>
<p>{{ post.description }}</p>
<a href="{{ post.url }}">weiterlesen</a>

{% endfor %}
{% endraw %}
```

Mit  **_page.title_,  _page.date_**  usw. kannst Du auch hinterlegte Parameter aus deinem Blogbeitrag (YAML-Header [z.B.  _title: Titel des Blogs_]) direkt an passende Stelle anzeigen.

**Info:**  Mit  `site` anstatt  `page` kannst Du einen  **globalen Parameter**  aus der  `config.yml`  aufrufen. z.B.  `site.author`.

## Pagination

Damit `paginator.posts`  funktioniert, benötigst Du das Plugin  [jekyll-paginate](https://github.com/sverrirs/jekyll-paginate-v2 "Pagination für Jekyll"){:target="_blank" rel="nofollow"}. In dem GitHub-Repo findest Du  [praktische Beispiele](https://github.com/sverrirs/jekyll-paginate-v2/tree/master/examples "Praxisbeispiele"){:target="_blank" rel="nofollow"}  für die Implementierung.

## Webseite generieren

Nachdem Du nun erstmal das Grundgerüst erstellt hast ist es Zeit, kannst Du testen ob auch die Generierung funktioniert.  
Dazu musst Du nur mit der Konsole in das `root`-Verzeichnis deines Jekyll-Projekts navigieren und Folgendes in die Konsole tippen:

```conf
JEKYLL_ENV=production bundle exec jekyll build --trace
```
