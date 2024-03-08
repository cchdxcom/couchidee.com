---
categories: ['Webentwicklung']
tags: ['Jekyll', 'Static File CMS', 'install', 'Linux', 'Projekt']
title: 'Jekyll unter Linux installieren und Projekt anlegen'
---

Um Jekyll nutzen zu können benötigst Du auf deinem Rechner Ruby.  
Unter Ubuntu / Linux installierst Du Ruby so:

```shell
sudo apt-get install ruby-full build-essential zlib1g-dev
```

Anschließend fehlt nur noch die korrekte Konfiguration. Öffne dazu einfach ein Terminal führe folgende Eingaben aus:

``` shell
echo "# Install Ruby Gems to ~/gems" >> ~/.bashrc
echo "export GEM_HOME="$HOME/gems" >> ~/.bashrc
echo "export PATH="$HOME/gems/bin:$PATH" >> ~/.bashrc
source ~/.bashrc
```

Nachdem Ruby nun ordentlich installiert und konfiguriert ist, kannst Du endlich auch Jekyll installieren.

``` shell
gem install jekyll bundler
```

_Update:  
In einem anderen Artikel habe ich die Jekyll-Installation unter Windows kurz zusammengefasst._

Ich persönlich habe ein separates Coding-Verzeichnis unter dem ich alle Webprojekte erstelle und pflege.  
Navigiere nun zu deinem übergeordneten Projektordner. (z.B.:  `/home/christian/Coding`) und führe folgenden Befehl aus:

## Neues Projekt mit Jekyll anlegen

``` shell
jekyll new neuesProjekt
```

Wenn Du nun in den neuen Ordner  _neuesProjekt_  wechselst und folgendes ausführst startest Du einen Live-Server den Du anschließend unter  _[http://localhost:4000](http://localhost:4000/)_  erreichst. Alle Änderungen die Du vornimmst und speicherst, werden nach erneutem Laden der Webseite sichtbar.

## Live-Server starten

``` shell
bundle exec jekyll serve
```

Dies ist auch ein Punkt, den ich an Jekyll sehr schätze. Man benötigt nämlich keinen eigenen bzw. lokalen Webserver auf dem z.B. verschiedenste PHP-Versionen gepflegt werden müssen.
