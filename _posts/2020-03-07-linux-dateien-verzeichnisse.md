---
categories: ['Linux']
tags: ['Linux', 'Dateien', 'Verzeichnisse']
title: 'Linux Dateien und Verzeichnisse'
---

Sollen Dateien mit Windows getauscht werden bzw. unter Windows lesbar sein, solltest Du dich auf die üblichen Zeichen beschränken.

`A-Z a-z 0-9+-.=[]";,$#&@!()-{}~^ *`

Dateien die zwischen verschiedenen System ausgetauscht werden sollten bestenfalls nur die folgenden Zeichen enthalten:  `A-Z a-z 0-9+-._*`

Verwendest Du die Datei nur unter Linux, könntest Du auch folgende Zeichen verwenden:  `*:?"<>|*`

**Beachte:**  Unter Windows ist es Groß- und Kleinschreibung egal. Unter Linux nicht. Beispiel:  `Text.txt`  und  `text.txt`  werden unter Linux als unterschiedliche Dateien behandelt. Weiterhin müssen Dateien unter Linux nicht durch eine Dateiendung charakterisiert werden. Hilfreich ist es dennoch.

**Versteckte Dateien:**  mit einem  `.`  vor einem Dateinamen (z.B:  `.htaccess`) wird die Datei standardmäßig versteckt. Mit wenigen Klicks lässt sich eine solche Datei aber unter jedem Betriebssystem schnell anzeigen.

### erlaubte Dateinamen

Grundsätzlich sind alle üblichen Dateibezeichnungen gültig, wenn sie nicht mit einem Sonderzeichen (z.B:  `-`) beginnen oder verbotene Zeichen wie  `/`  enthalten. Übrigens, mit  `./programm`  startest Du eine Datei als Programm.

## Verzeichnisse

- wechseln kann man zwischen Verzeichnissen durch  `cd /home/beispielordner`
- oder eine Ebene höher durch  `cd ..`
- absoluter Pfadname des aktuellen Verzeichnisses angeben:  `pwd`  – print working directory
- Die Tilde  `~`  steht für das Home-Verzeichnis des aktuellen Benutzers

### Auflistung von Inhalten

Oft benötigt man eine schnelle Übersicht der Dateien in einem Ordner, dafür gibt es das Kommando  `ls`. Führt man  `ls`  ohne weitere Parameter aus, erscheint ein einfache Aufzählung aller sichtbaren Inhalte (Dateien und Ordner).

### Auswahl an Optionen für ls

- `-a`  oder  `- all`  – versteckte Dateien anzeigen
- `-i`  oder  `--inode`  gibt die eindeutige Dateinummer aus
- `-l`  oder  `--format=long`  zeigt zusätzliche Informationen an
- `--color=no`  verzichtet auf die Farbcodierung
- `-p`  oder  `-F`  markiert Dateityp durch angehängte Sonderzeichen
- `-r`  oder  `--reverse`  Sortierreihenfolge umkehren
- `-R`  oder  `--recursive`  durchsucht auch Unterverzeichnisse
- `-S`  oder  `--sort=size`  sortiert Dateien nach Größe (größte zuerst)
- `-t`  oder  `--sort=time`  sortiert Dateien nach Zeit (neueste zuerst)
- `-X`  oder  `--sort=extension`  sortiert Dateien nach Dateityp

### Verzeichnisse anlegen und löschen

Natürlich lassen sich auch über die Konsole Ordner erstellen und löschen. mit  `mkdir ordner`  kann ein einzelner Ordner erstellt werden. Mit der Option  `p`  können verschachtelte Unterverzeichnisse angelegt werden  `mkdir -p coding/project`. Leere Ordner können mit  `rmdir projekt/`  und leere Unterverzeichnisse mit  `rmdir -p coding/project`.

## Dateien - verschieben, kopieren und löschen

### Dateien kopieren

Kopiert wird mit dem Kommando  `cp`  (copy). Um welche Daten es sich dabei handelt spielt keine Rolle. Beispiel:  `cp datei datei2`  oder zum kopieren in andere Verzeichnisse  `cp Downloads/text.txt Dokumente/`– zu beachten ist aber, dass die Methode bereits existierende Datei einfach überschreibt. Möchtest Du eine Warnung, wenn Dateien bereits existieren, dann kannst Du die Option  `-i`  nutzen.

Weiterhin besteht die Möglichkeit, dass Du sogenannte Links/Verweise auf die Originalen Dateien anlegst, anstatt sie zu kopieren. Mit  `cp -l`. Beispiel:  `cp -l ein/langer/pfad/test.txt /Schreibtisch/test.txt`

### Optionen bei  `CP`

- `b`  (backup) erstellt Sicherungskopien von existierenden Zieldateien
- `-f`  (force) Zieldateien werden ohne Warnung überschrieben
- `-i`  (interactive) Warnung wenn Dateien bereits existieren
- `-p`  (preserve) soweit möglich, werden alle Dateiattribute beibehalten
- `-R`  (recursive) kopiert auch Unterverzeichnisse + Dateien
- `-u`  (update) kopert nur, wenn Zieldatei älter ist oder noch nicht existiert
- `-v`  (verbose) zeigt alle Aktivitäten an

### Dateien verschieben

Verschieben kannst Du Dateien und Verzeichnisse mittels  `mv`  (move). Es verhält sich wie  `cp`. Optionen wie  `-b`  ,  `-f`  ,  `-i`  ,  `-u`  und  `-v`  können auch problemlos auf  `mv`  angewandt werden. Das  **Umbenennen**  einer Datei ist ziemlich einfach mit  `mv dateiname neuerdateiname`  erledigt.

### Dateien löschen

Mit  `rm`  (remove) können Dateien gelöscht werden. Erforderlich ist, dass entsprechende Schreibrechte vorhanden sind. Standardmäßg agiert  `rm`  genauso wie  `cp`  und  `mv`, Dateien werden ohne Warnung sofort gelöscht. Rekursives löschen funktioniert wie gewohnt mit  `rm -r`. Um größerem Schaden vorzubeugen, macht es Sinn sich die Option  `-i`  anzugewöhnen. 

## Dateien verknüpfen / verlinken

Um einen Verweis auf eine Datei zu erstellen, bietet Linux das Kommando  `ln`  (feste Verknüpfungen). Für Verzeichnisse lassen sich mit  `ln`  keine Links erstellen. Als Beispiel:  `ln datei1 datei2`. Die neue Datei2 exisitiert im eigentlichen Sinne nicht, denn sie ist nur ein Verweis auf die originale Datei (`datei1`). Änderst Du in Datei1 den Inhalt, wird der neue Inhalt auch in Datei2 vorhanden sein, denn es handelt sich im die selbe Datei. Lediglich ein weiterer Name wurde vergeben. Um Links im Nachhinein zu identifizieren genügt ein  `ls -i`. In der Ausgabe, z.B.:  `123456 datei1 123456 datei2`  erkennst Du anhand der Inode-Nummer, dass es sich um die selbe Datei handelt. Die Inode-Nummer identifiziert eindeutig jede Datei – denn sie ist einmalig in deinem Dateisystem. Daher funktioniert die Verlinkung nur in demselben physikalischen Dateisystem. Übrigens ist es auch nicht möglich, bei mehreren Namen herauszufinden, welcher Name das Original ist.

Neben den „festen Verknüpfungen“ gibt es auch symbolische Links (weiche Verknüpfungen) . Wie gerade geschrieben, ist es nicht möglich, herauszufinden ob weitere feste Verknüpfungen im Dateisystem irgendwo bestehen. Möchtest Du z.B. den htdocs-Ordner deines lokalen Webservers einfach an einer anderen Stelle verfügbar machen, kannst Du die Option  `-s`  nutzen. Beispiel:  `ln -s /opt/lampp/htdocs Localserver`. Mit  `ls -lL verzeichnis`  bzw.  `ls -lH verzeichnis`  werden eventuell vorhandene Symlinks direkt aufgelöst und angezeigt .  `-L`  löst symbolische Links immer auf und  `-H`  löst nur direkt eingegebene Links auf.