---
categories: ['Webentwicklung']
tags: ['Jekyll', 'Static File CMS', 'Plugin']
title: 'Jekyll Admin-Plugin installieren'
---

Jekyll ist ziemlich minimalistisch und straightforward – deshalb mag ich es. Konfiguriationen müssen direkt im Code vorgenommen werden und auch sonst passiert nichts „verborgen“ im Hintergrund. Auf Komfort muss man daher weitestgehend verzichten. Ein wenig Abhilfe schafft hier das Admin-Plugin auf lokaler Ebene. Für mich ein nettes Feature um den Content bequemer zu erstellen und zu verwalten.

## Installation
Die Installation ist denkbar einfach und in wenigen Sekunden erledigt. Mir persönlich gefällt dieses Plugin bisher sehr, da es mich beim Verwalten des Contents gut unterstützt. Markdown ist zwar einfach, aber schneller geht es mit dem Admin-Plugin trotzdem. In meiner Jekyll-Instanz musste ich lediglich im ‚Gemfile‘ die Code-Zeile `gem jekyll-admin` einsetzen:

```
group :jekyll_plugins do
  [...]
  gem 'jekyll-admin'
end
und anschließend natürlich bundle install ausführen. Schon ist das Plugin unter ‚http://localhost:4000/admin‘ aktiv.
```

## Features:
- wysiwyg-Editor mit Markdown-Support
- einfaches hinzufügen von Metadaten
- Konfig im GUI-Modus * Link zur Vorschau
- Side-By-Side Vorschau Markdown -> Inhalt
- individuelle Bezeichnung der Collections möglich
- Mehr Infos gibt es wie gewohnt auf Github im Repository von Jekyll