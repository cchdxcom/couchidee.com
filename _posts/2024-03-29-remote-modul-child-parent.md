---
categories: ['Programmierung']
tags: ['Electron', 'Remote', 'Fenster']
title: 'Electron Remote-Modul (+ parent / child)'
---

## Remote-Modul verwenden

**Das Remote-Modul ermöglicht die indirekte Nutzung von IPC-Objekten - empfohlen wird jedoch die direkte Nutzung. Die direkte Nutzung von IPC-Objekten bietet mehr Kontrolle und viele weitere Möglichkeiten.**

Du kannst in Electron beliebig viele Renderprozesse anlegen / starten. Jeder Render-Prozess besteht im Grunde nur aus einer neuen HTML-Datei und optional einer neuen JavaScript-Datei, die den jeweiligen Render-Prozess starten soll.

## js-Dateien einbinden

Um deinen Code besser zu strukturieren, empfiehlt es sich je nach Aufgabe die Dateien zu sortieren bzw. sie in Unterordnern zu trennen. Dies gibt dir einen wesentlich besseren Überblick.

Dazu benötigst du (wie auf Webseiten) einfach folgende Schreibweise:

```html
<script src="src/js/routing.js"></script>
```

## @electron/remote

`@electron/remote` ist ein Electron-Modul, das JavaScript-Objekte vom Hauptprozess zum Renderer-Prozess überbrückt. Dadurch kannst du auf Objekte, die nur im Hauptprozess verfügbar sind, so zugreifen, als ob sie im Renderer-Prozess verfügbar wären.

siehe [https://www.npmjs.com/package/@electron/remote](https://www.npmjs.com/package/@electron/remote){:target="_blank" rel="nofollow"}

Um ein weiteres Fenster per remote zu deiner Electron-App hinzuzufügen, kannst du beispielsweise folgendes tun: füge der `main.js` folgendes hinzu:

```html
<h2>weitere Ansicht starten</h2>
<button id="view2" type="button" class="btn btn-info">View 2 starten</button>
<script src="js/routing.js"></script>
```

Das Remote-Modul musst du übrigens separat mit folgendem Befehl installieren:

```shell
npm i @electron/remote
```

Anschließend musst du noch das Remote-Modul in deiner `main.js` aktivieren:

```javascript
// laden des Moduls
const remote = require('@electron/remote/main')

// initialisieren des Moduls
remote.initialize()

function createWindow() {
  const mainWindow = new BrowserWindow({
    icon: "assets/icons/app_icon.png",
    width: 800, height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,

      // aktivieren des Moduls
      enableRemoteModule: true
    },
  });
  // Webcontents aktivieren
  remote.enable(win.webContents)
}
```

In der `routing.js` kann ich die einzelnen Views angeben die bei einem bestimmten Event geladen werden sollen:

```javascript
const view2 = document.getElementById('view2')
view2.addEventListener('click', function (event){
    const {BrowserWindow} = require('@electron/remote')

    // lässt du die Abmessungen weg, wird die Standardgröße für Fenster verwendet (800px x 600px) 
    const window2 = new BrowserWindow({
        width:400, height: 400,

        // gibst du max.-Werte ein, kann das Fenster nicht weiter vergrößert werden
        maxWidth: 500,
        maxHeight: 500,

        // Farben anpassen
        backgroundColor: '#000000',
        // Rahmen und Menü deaktivieren
        frame: false
    })
    window2.loadFile('src/view2.html')
})
```

## child / parent

Ein Fenster wird als `child`-Fenster definiert, wenn du als Parameter einen `parent` angibst. Dann bleibt das `child`-Fenster immer im Vordergrund. Zudem werden alle `child`-Fenster geschlossen, wenn das `parent`-Fenster geschlossen wird. Zumindest, wenn du nicht `modal` aktiviert hast -> siehe unten.

```javascript
function createWindow() {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    icon: "assets/icons/app_icon.png",
    width: 800, height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,
      enableRemoteModule: true
    },
  });

  remote.enable(mainWindow.webContents)

  mainWindow.loadFile("src/index.html");

  // Im Fenster wird die URL von Couchidee aufgerufen - das child-Fenster bleibt immer im Vordergrund
  const couchideeBrowser= new BrowserWindow({width: 1000,height: 800, parent: mainWindow})
  couchideeBrowser.loadURL("https://www.couchidee.com")
}
```

## once / show / modal

Um ein Fenster erst anzuzeigen, wenn der Inhalt fertig geladen ist, benötigst du folgende Schreibweise:

```javascript
const couchideeBrowser = new BrowserWindow({show: false, width: 1000,height: 800, parent: mainWindow, modal: true})
couchideeBrowser.loadURL("https://www.couchidee.com")
couchideeBrowser.once('ready-to-show', () => {
    couchideeBrowser.show()
})

```

Die Kombination aus `parent: mainWindow, modal: true` verbietet es, solange das `child`-Fenster aktiv ist, irgendetwas im `parent`-Fenster zu tun.

weitere Informationen findest du unter: [https://www.electronjs.org/de/docs/latest/api/browser-window](https://www.electronjs.org/de/docs/latest/api/browser-window){:target="_blank" rel="nofollow"}