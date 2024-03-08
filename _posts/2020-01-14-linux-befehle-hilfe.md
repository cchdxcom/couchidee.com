---
categories: ['Linux']
tags: ['Linux', 'Befehle', 'Hilfe']
title: 'Linux Befehle und Hilfe verwenden'
---

- `sudo`  – sollte aus Sicherheitsgründen nur über den direkten Pfad  `/bin/su`  aufgerufen werden.
- `exit`  – Beendet eine Shell
- `id`  – Gibt UID und GIDs eines Benutzers aus
- `kdesu`  – Startet unter KDE ein Programm als anderer Benutzer
- `logout`  – Beendet eine Sitzung ( Abmelden“)
- `su`  – Startet eine Shell unter der Identität eines anderen Benutzers
- `sudo`  – Erlaubt normalen Benutzern das Aufrufen bestimmter Kommandos mit Administratorprivilegien

## wenn verschiedene Shells zur Verfügung stehen

- `sh`  – klassische Bourne-Shell
- `bash`  – »Bourne-Again-Shell« (Bash)
- `ksh`  – Korn-Shell
- `csh`  – C-Shell
- `tcsh`  – »Tenex-C-Shell«

## Kommandos -> Parameter

Grundsätzlich ist alles unter Linux case sensitive und unterscheidet deshalb zwischen Groß- und Kleinschreibung.  `Muster.txt`  ist eine andere Datei als  `muster.txt`. Ebenso verhält es sich bei Kommandos, Parametern usw.  `A != a`.

Info: Zeilentrenner – Befehl auf 2 Zeilen mittels

### Optionen

sind Parameter mit einem Minuszeichen  `-`, die meistens nicht zwingend angegeben werden müssen. Mehrere Optionen können zusammengefasst werden. Beispiel: anstatt  `-l -i -N`  genügt ein  `-liN`

Optionen können auch länger als ein Zeichen sein, weshalb auch  **long Options**  gibt, welche mit  `--`  (2x Minus) eingeleitet werden. Long Options dürfen nicht zusammengefasst werden werden.

### Argumente

sind Parameter  **ohne**  einleitendes Minuszeichen. Argumente sind z.B. Namen von Dateien.

**Beispiel**  einer Kombination aus Optionen und einem Argument:`ls -gloRF --dired`

### Befehlsstruktur

`Kommando -Option --LangeOption Argumente`

**Kommando-Arten:**  mithilfe von  `type`  kann der Kommando-Typ bestimmt werden. Unterschieden wird grundsätzlich zwischen internen (z.B. Kommandos der Bash) und externen Kommandos.

### Sonstiges

soll z.B. ein Dateiname angegeben werden, der  `neue Liste.json`  heißt müssen wir den Dateinamen in Hochkomma stellen, da er ein Leerzeichen beinhaltet. Also  `nano` neue Liste.json  oder auch  `touch` neue Liste.json. Neben dem Leerzeichen müssen auch folgende Zeichen besonders behandelt werden.

`$&;(){}[]?!<>«*`

**Beispiel:**  `nano +2,5 neue liste.txt`  = (nano +line,column  `new filename`)

## Help und Handbuchseiten

Genauere Beschreibungen von integrierten Kommandos werden mit–help`,*-h`,  `?`  abgerufen.  
Viele Tools nutzen die Option  `--help`  oder auch  `-h`  um Details zur Syntax, sowie der Parameter zu liefern.

- `NAME`  – Kommandoname mit kurzer Funktionsbeschreibung
- `SYNOPSIS`  – Befehlssyntax
- `DESCRIPTION`  – Ausführliche Beschreibung
- `OPTIONS`  – mögliche Optionen
- `ARGUMENTS`  – mögliche Argumente
- `FILES`  – benötigte Dateien
- `EXAMPLES`  – Beispiele
- `SEE ALSO`  – Querverweise zu verwandten Themen
- `DIAGNOSTICS`  – Fehlermeldungen
- `*COPYRIGHT`  – Autor(en)
- `BUGS`  – bekannte Fehler
- Ein wichtiges Hilfsmittel sind auch die sogenannten  **Manpages**, welche über  `man`  aufgerufen werden können. Beispiel:  `man ls`. Um Manpages aufzulisten, welche ein bestimmtes Keyword beinhalten, kann  `apropos`  genutzt werden. Beispiel:  `apropos pgp`. Zur druckreifen Aufbereitung von Texten hilft  `groff`. Das Kommando  `info`  zeigt GNU-Info-Seiten auf einem Textterminal an und  
    `less`  zeigt Texte (etwa Handbuchseiten) seitenweise an.

Für Neueinsteiger ist auch  `man -f`  oder einfacher  `whatis`  interessant. Damit wird die Beschreibung der Handbuchseite angezeigt. Beispiel:  `whatis ls`.