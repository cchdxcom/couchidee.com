---
categories: ['Webentwicklung']
tags: ['Jekyll', 'Static File CMS', 'Template', 'Webseite']
title: 'Jekyll Webseite und Template einrichten'
---

Jekyll nutzt die Template-Sprache  [Liquid](https://shopify.github.io/liquid/){:target="_blank" rel="nofollow"}. Dadurch wird es nun relativ einfach, jedes HTML-Template mit Jekyll zu verbinden. Ein Standard-Layout könnte so aussehen:

```html
{% raw %}
<!doctype html>
<html lang="de">
{% include metadaten/head.html %}

<body>
    {% include header.html %}
    {{ content }}
    {% include footer.html %}
</body>

</html>
{% endraw %}
```

In diesem Beispiel sind der `header`, `footer` etc. komplett ausgelagert. Ob man alle `includes` im root-Ordner (`_includes`) oder in Unterordnern (z.B.  `_includes/metadaten`) speichert, bleibt Dir überlassen. Am Ende solltest Du einfach den Überblick behalten können.

## Head-Bereich

Schauen wir uns den Head-Bereich gleich mal an, wo wir doch gerade darüber sprechen. Sonderlich kompliziert ist das nicht, aber ein paar kleine Hinweise sind sicher ganz nett. Hier also nun ein Ausschnitt mit Kommentaren.

```html
<head>
    ...
    <!-- damit Verlinkungen von internen Ressourcen immer funktionieren, solltest Du absolute_url angeben -->
    <link rel="shortcut icon" type="image/png" href="{{ 'assets/img/favicon.ico' | absolute_url  }}">

    <!-- Beispiel für die Einbindung von CSS (und JS) -->
    <link rel="stylesheet" href="{{ 'assets/css/bootstrap.min.css' | absolute_url }}">

    <!-- auch hier kannst Du mit page.* und site.* auf Seitenparameter zugreifen. -->
    <title>{{ page.title }}</title>
    ...
</head>
```

Die restlichen „includes“ funktionieren nach dem gleichen Prinzip. Nur anstelle des Content-Tags wird dann der jeweilige Inhalt gerendert. Welche Seite, welches Layout bekommen soll, legst Du im `YAML`-Header jeder Seite fest. Aber dazu später mehr.

## Navigation

Im Header-Bereich der Webseite befindet sich in aller Regel die Navigation. Bei meinem Beispiel sieht ein Ausschnitt des Headers so aus:

```html
{% raw %}
<div class="main-menu">
    <ul>
        {% include navigation.html %}
    </ul>
</div>
{% endraw %}
```

Im `include` von `navigation.html`  befindet sich folgender Code:

```liquid
{% raw %}
{% for item in site.data.navigation %}
<li>
    <a href="{{ item.link | relative_url  }}" 
        {% if page.url == item.link %}class="current"
        {% endif %}>{{ item.name }}
    </a>
</li>
{% endfor %}
{% endraw %}
```

Hier siehst Du wieder eine neue Möglichkeit, Jekyll ganz entspannt und einfach mit Daten zu versorgen. Um möglichst wenig Pflegeaufand bei Änderungen der Navigation zu haben, nutze ich `YAML`-Dateien im  `_data`-Ordner. Daher auch der Zugriff auf `site.data.navigation`.

In der entsprechenden `navigation.yml` im `_data`-Ordner steht:

```conf
- name: Home
  link: /
- name: Blog
  link: blog/index.html
- name: Couchwiki
  link: wiki/index.html
```

Sollte ich nun einen weiteren Punkt in der Navigation benötigen, so ergänze ich ganz einfach nur einen weiteren Anstrich. Für ein Wiki lässt sich diese Art und Weise der Linkstrukturierung ebenfalls wunderbar nutzen.

```conf
- name: Linkname
  desc: Linkbeschreibung
  link: Linkpfad
  icon: Link Iconname
```