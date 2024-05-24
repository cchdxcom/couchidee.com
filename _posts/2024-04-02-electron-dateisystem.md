---
categories: ['Programmierung', 'Electron']
tags: ['Electron', 'Dateien', 'Remote']
title: 'Electron Dateisystem'
---

## Einleitung

Ein einfaches Beispiel wie du in Electron Dateien speichern, öffnen und löschen kannst. Dabei wird beim speichern und löschen jeweils das fs-Modul und beim laden das remote-Modul genutzt. Ich habe den Code zum besseren Verständnis ausführlich kommentiert.

## index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <title>Dateien - save, load, delete</title>
  </head>
  <body>
    <form>
      <div class="form-group">
        <label for="fileName">Name</label>
        <input class="form-control" id="fileName" type="text"></input>
      </div>
      <div class="form-group">
        <label for="content">Inhalt</label>
        <textarea class="form-control" id="content" rows="6"></textarea>
      </div>
    </form>
    <button id="saveFile" type="button" class="btn btn-info">speichern</button>
    <button id="loadFile" type="button" class="btn btn-info">laden</button>
    <button id="deleteFile" type="button" class="btn btn-info">löschen</button>
    <script src="js/routing.js"></script>
  </body>
</html>

```

## main.js

```javascript
// Modules to control application life and create native browser window
const { app, BrowserWindow, dialog} = require("electron");
const { MenuItem } = require("electron/main");
const remote = require('@electron/remote/main')
remote.initialize()
const path = require("node:path");

function createWindow() {
  // Create the browser window.
  const mainWindow = new BrowserWindow({
    icon: "assets/icons/app_icon.png",
    width: 800,
    height: 600,
    webPreferences: {
      nodeIntegration: true,
      contextIsolation: false,
      enableRemoteModule: true
    },
  })

  remote.enable(mainWindow.webContents)
  mainWindow.loadFile("src/index.html");
}

app.whenReady().then(() => {
  createWindow();

  app.on("activate", function () {
    if (BrowserWindow.getAllWindows().length === 0) createWindow();
  });
});

app.on("window-all-closed", function () {
  if (process.platform !== "darwin") app.quit();
});
```

## routing.js

```javascript
const { app, BrowserWindow, ipcRenderer} = require('electron');

// Module importieren
const fs = require('fs')
const path = require('path')
const remote = require('@electron/remote')
const dialog = remote.dialog

// Definierten Pfad vorgeben
let pathName = path.join(__dirname, "/../assets")

// Verknüpfen der Buttons mit den Konstanten
const fileName = document.getElementById('fileName')
const content = document.getElementById('content')
const saveFile = document.getElementById('saveFile')
const loadFile = document.getElementById('loadFile')
const deleteFile = document.getElementById('deleteFile')

// Datei speichern mit dem fs-Modul
saveFile.addEventListener('click', function(){
    // Definition des Dateipfads (definierter Pfad + Dateiname aus Formular) 
    let file = path.join(pathName, fileName.value)
    // Dateiinhalt aus dem Feld in Variable speichern
    let contentFile = content.value
    // Speichervorgang mittels fs-Modul
    // Dateipfad inkl. Dateiname + Dateiinhalt + Fehlerbehandlung
    fs.writeFile(file, contentFile, function(err){
        if (err){
            console.log(err)
        }
        console.log("Datei wurde gespeichert!")
    })
})

// Datei laden mit dem remote-Modul
loadFile.addEventListener('click', function() {
    // Dialogbox (showOpenDialog) vom remote-Modul aufrufen
    dialog.showOpenDialog(remote.getCurrentWindow(),{
        properties: ["openFile"],
        // vorgeben der erlaubten Dateitypen
        filters: [{name: 'Texte', extensions: ['txt','md']}]
    }).then(result =>{
        // Abfrage, ob Vorgang abgebrochen wurde
        if (result.canceled === false){
            // result.filePaths gibt Array mit den Dateipfaden zurück
            let pathName = result.filePaths[0]
            
            // Datei einlesen
            fs.readFile(pathName, function(err, fileContent){
                if(err){
                    return console.log(err)
                }
                // mit den eingelesenen Daten die Felder im Formular füllen
                content.value = fileContent.toString()
                fileName.value = path.basename(result.filePaths[0])
            })
        }
    }).catch(err=>{
        console.log(err)
    })
})

// Datei löschen mit dem fs-Modul
deleteFile.addEventListener('click', function(){
    // Dateipfad definieren
    let file = path.join(pathName, fileName.value)
    
    // löscht Datei
    fs.unlink(file, function(err){
        if (err){
            console.log(err)
        }
        // leeren der Formulardaten
        fileName.value = ''
        content.value = ''
    })
})
```