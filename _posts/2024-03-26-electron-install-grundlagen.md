---
categories: ['Programmierung', 'Electron']
tags: ['Electron', 'install']
title: 'Electron installieren und Grundlagen'
---

## Grundlagen

Electron ist dafür ausgelegt, Cross-Plattform-Apps mittels `JavaScript`, `HTML` und `CSS` zu erstellen. Grundlagen in den jeweiligen Bereichen sind von Vorteil.

- Electron Dokumentation
  [https://www.electronjs.org/de/docs/latest/](https://www.electronjs.org/de/docs/latest/){:target="_blank" rel="nofollow"}
  

Mit Electron können Desktop-Apps für Windows, OSX und Linux entwickelt werden. Als Basis dient die OpenSource Laufzeitumgebung Node.js (die wie der Name schon verrät auf JavaScript basiert). Node.js ermöglicht es dir, JavaScript außerhalb eines Browsers auszuführen. Ein Webserver kann ebenfalls mit Node.js betrieben werden.

[https://nodejs.org/en](https://nodejs.org/en){:target="_blank" rel="nofollow"}

[https://nodejs.org/docs/latest/api/](https://nodejs.org/docs/latest/api/){:target="_blank" rel="nofollow"}

Node.js bietet eine Ressourcen-sparende Architektur und ermöglicht dir Zugriff auf das Netzwerk und das Dateisystem deines Computers. Für Node.js gibt es bereits unzählige Module welche über den Paketmanager `npm` verwaltet werden.

[https://www.npmjs.com/](https://www.npmjs.com/){:target="_blank" rel="nofollow"}

Ähnliche Paketmanager sind z.B.

- pip [https://pypi.org/](https://pypi.org/){:target="_blank" rel="nofollow"} für Python
  
- oder composer [https://packagist.org/](https://packagist.org/){:target="_blank" rel="nofollow"}
  

Als IDE eignet sich z.B. -> [https://vscodium.com/](https://vscodium.com/){:target="_blank" rel="nofollow"} / VSCode / Atom usw.

## Installation

1. Node.js installieren -> [https://nodejs.org/en/download](https://nodejs.org/en/download){:target="_blank" rel="nofollow"} -> Installer auswählen
  
2. `npm` -> wurde bereits mit node.js automatisch mit installiert
  

-> testen mit `node -v` und `npm -v` -> Anzeige der Version

3. optional: `npm install--save -dev electron`

## Grundstruktur

Die Grundstruktur einer Minimalen Electron-Anwendung besteht aus 3 Files:

- `package.json` -> enthält Informationen zu allen benötigen Modulen der App + alle Meta-Daten
  
  - Scripte die ausgeführt werden können um Aufgaben in der App zu automatisieren
    
  - Definiert Einstiegspunkt der App z.B.
    `"main":"main.js"`
    
  - die Datei `package.json` wird automatisch mit `npm init` angelegt
    

- `main.js` -> 1 x main-Prozess
  - wird als main-Prozess bezeichnet und enthält die Programmierlogik in JavaScript und erstellt min. eine Instanz eines Browserfensters. Der Name ist egal - es muss nur eine js-Datei sein .
  - Da Electron auf node.js basiert, ermöglicht es dir Zugriff auf Funktionen des Betriebssystems, auf die normale Browseranwendungen keinen Zugriff haben.

- `index.html` -> 1-n x render-Prozess
  - Frontend der Anwendung und rendert die Inhalte im Anwendungsfenster
  - Name egal - muss eine html-Datei sein.
  - jeder render-prozess ist eine eigene Ansicht/Fenster im Frontend
    - jeder render-prozess ist eine eigene Instanz eines Chromium-Webbrowser

## erste Anwendung erstellen

```shell
# Clone dir zuerst folgendes Repository: https://github.com/electron/electron-quick-start
# Clone this repository
git clone https://github.com/electron/electron-quick-start

# Go into the repository
cd electron-quick-start

# Install dependencies
npm install

# Run the app
npm start
```

Wenn du wie ich mit dem Boilerplate deine ersten Tests mit electron umsetzen willst, solltest du etwas beachten. Am anfang probierst du vielleicht gleich mal ein schnelles Inline-Script wie z.B.

```html
<p>System-Version <script>document.write(process.getSystemVersion())</script></p>
```
siehe [https://www.electronjs.org/docs/latest/api/process](https://www.electronjs.org/docs/latest/api/process){:target="_blank" rel="nofollow"}

Damit das Ganze mit dem Boilerplate auch funktioniert musst du zuerst im '<head>' folgende Zeit auskommentieren, da dir deine Anwendung sonst aufgrund der Content-Security-Policy eine Fehlermeldung ausgibt.

```html
<!-- <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'"> -->
```

Es gibt zwar Node.js Module für Hot-Reload [https://www.npmjs.com/package/electron-reload](https://www.npmjs.com/package/electron-reload){:target="_blank" rel="nofollow"}. Diese funktionieren jedoch nicht immer zuverlässig. Alternativ kannst du auch folgendes im `<head>` eintragen:

```html
<!-- aktualisiert den Inhalt alle 2 Sekunden -->
<meta http-equiv="refresh" content="2">
```

