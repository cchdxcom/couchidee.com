---
categories: ['Programmierung']
tags: ['Electron', 'sync', 'IPC']
title: 'Electron IPC - async / sync'
---

## IPC Interproesskommunikation

Eine Electron-App hat immer einen Main-Prozess und kann unendlich viele Render-Prozesse besitzen. Zugriff auf die nativen Desktop-APIs (z.B.: Dateisystem) hat aber aus Sicherheitsgründen nur der Main-Prozess. Damit man aber dennoch (auch mit den Render-Prozessen) sicher auf die APIs "zugreifen" kann, nutzt Electron das IPC-Modell mit den IPC-Objekten um Informationen zwischen dem Main- und den Render-Prozessen austauschen zu können.

## Synchrones IPC / Asyncron IPC

**Synchrones IPC** blockt andere Systemoperationen solange bis es selbst seine Aufgabe komplett beendet hat. **Asynchrones IPC hingegen, lässt andere Prozesse gewähren und sollte daher bevorzugt verwendet werden.**

Das [remote-Modul](https://www.couchidee.com/posts/electron-remote-modul-child-parent/) arbeitet immer syncron und kann daher zu prozessualen Problemen und eingeschränkter Performance führen.

## Webpreferences

Wenn du in den `webPreferences` die Option `nodeIntegration: true` gewählt hast, kannst du alle beliebigen Node-Module und nativen Desktop-APIs im Frontend deiner Anwendung nutzen.

## Beispiel

Nun ein Beispiel (asynchrones IPC):

In der `main.js` musst du das `ipcMain`-Modul hinzufügen:

```javascript
const { app, BrowserWindow, ipcMain} = require("electron");
```

in der `routing.js` musst du das `ipcRenderer`-Modul hinzufügen:

```javascript
const { app, BrowserWindow, ipcRenderer} = require("electron");
```

Der Renderprozess soll nun auf ein Klick-Event reagieren und eine IPC-Anfrage an den Main-Prozess senden. Dazu muss in die `main.js` folgende `const` deklariert werden:

```javascript
const error = document.getElementById('error')

error.addEventListener('click', function (event){
    ipcRenderer.send('mitteilung')
})
```

Damit der main-Prozess die Mitteilung auch empfangen kann, musst du folgendes in die main.js einfügen:

```javascript
ipcMain.on('mitteilung', function(event){
  dialog.showErrorBox('IPC Error', 'Mitteilung erhalten!')
})
```

Damit kannst du das IPC-Modell schon auf einfachste Art ausprobieren.

Um nun aber eine Nachricht vom Main-Prozess an den Renderprozess schicken zu können, musst du folgendes in der `ipcMain.on(...)` von oben ergänzen:

```javascript
ipcMain.on('mitteilung', function(event){
  dialog.showErrorBox('IPC Error', 'Mitteilung erhalten!')                        

  event.sender.send('mitteilung 2', 'Main-Prozess hat die Nachricht erhalten!')
})
```

Damit du das Event auch abfangen kannst, musst du noch im Render-Prozess auf die eingehende Nachricht (`'mitteilung 2'`) auf dem Event-Kanal achten. 

Dazu musst du in der routing.js nun noch folgende Funktion zum Anzeigen der Nachricht hinzufügen:

```javascript
ipcRenderer.on('mitteilung 2', function(event, arg){
    document.write("<p>"+arg+"</p>")
})
```

## Kurz-Beispiel sync/async (kompletter Code)

`index.html`

```html
<!DOCTYPE html>
<html>
  <head>
    meta charset="UTF-8">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <title>ASYNC / SYNC</title>
  </head>
  <body>
    <h1>IPC-Modell</h1>
    <button id="asyncButton" type="button" class="btn btn-info">asyncButton</button>
    <button id="syncButton" type="button" class="btn btn-info">syncButton</button>
    <script src="js/routing.js"></script>
  </body>
</html>
```

`routing.js`

```javascript
const {app, BrowserWindow, ipcRenderer} = require('electron');
const asyncButton = document.getElementById('asyncButton')
const syncButton = document.getElementById('syncButton')

asyncButton.addEventListener('click', function (event){
    console.log('sync1')
    ipcRenderer.send('async-mitteilung')
    console.log('sync2')
})

syncButton.addEventListener('click', function (event){
    console.log('sync1')
    console.log(ipcRenderer.sendSync('sync-mitteilung'))
    console.log('sync2')
})

ipcRenderer.on('async-antwort', function(event, arg){
    console.log(arg)
})
```

`main.js`

```javascript
const { app, BrowserWindow, ipcMain, dialog} = require("electron");
const { MenuItem } = require("electron/main");
const remote = require('@electron/remote/main')
remote.initialize()
const path = require("node:path");

function createWindow() {
  const mainWindow = new BrowserWindow({
    icon: "assets/icons/app_icon.png",
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,
      enableRemoteModule: true
    },
  });
  mainWindow.loadFile("src/index.html");
}

// ASYNC
ipcMain.on('async-mitteilung', function(event){
  event.sender.send('async-antwort', 'Main-Prozess hat die Nachricht erhalten!')
})

// SYNC
ipcMain.on('sync-mitteilung', function(event){
  event.returnValue = "Sync Antwort!!"
})

app.whenReady().then(() => {
  createWindow();

  app.on("activate", function () {
    if (BrowserWindow.getAllWindows().length === 0) createWindow();
  });
});

app.on("window-all-closed", function () {
  if (process.platform !== "darwin") app.quit();
});atform !== "darwin") app.quit();
});
```