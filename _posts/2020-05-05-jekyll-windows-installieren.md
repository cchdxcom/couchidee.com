---
categories: ['Webentwicklung']
tags: ['Jekyll', 'Static File CMS', 'install', 'Windows']
title: 'Jekyll unter Windows installieren'
---

Um Jekyll unter Windows zu installieren, benötigst Du im ersten Schritt Ruby. Also einfach den aktuellen Installer mit DevKit von  [rubyinstaller.org](https://rubyinstaller.org/downloads/){:target="_blank" rel="nofollow"} downloaden.

Nun benötigst Du noch RubyGems. RubyGems ist im Grunde nur ein Paketmanager für Ruby. Einmal die aktuellste Version unter  [rubygems.org](https://rubygems.org/pages/download){:target="_blank" rel="nofollow"} downloaden, entpacken und wiefolgt installieren.

``` shell
$ gem update --system
$ gem install rubygems-update
$ update_rubygems
$ ruby setup.rb
```

Nachdem alle Vorbereitungen getroffen wurden kannst Du das Jekyll-Gem nun installieren. Optional mit  `bundler`.

``` shell
$ gem install jekyll bundler
```

Nutzt Du ein bestehendes Repository, solltest nach dem Klonen das ‚bundle install‘ nicht vergessen. Bekommst Du hier einen Fehler kann es gut sein, dass Versionskonflikte in der Datei ‚Gemfile.lock‘ existieren. Die Datei kannst Du aber ohne Probleme löschen.
