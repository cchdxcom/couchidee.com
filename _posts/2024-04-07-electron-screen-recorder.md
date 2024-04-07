---
categories: ['Programmierung']
tags: ['Electron', 'Screen-Recorder']
title: 'Electron Screen-Recorder / process-API'
---

## Einleitung

Electron bietet dir verschiedene Möglichkeiten, auf die System-Informationen und Ressourcen von dem gerade verwendeten Computer zuzugreifen.

Für die **System-Informationen** steht die dir `process-API` zur Verfügung:

[https://www.electronjs.org/docs/latest/api/process](https://www.electronjs.org/docs/latest/api/process){:target="_blank" rel="nofollow"}

Nützlich ist hier z.B.: `process.getSystemVersion()` um herauszufinden, auf welcher Plattform die Anwendung gerade ausgeführt wird. Das wird evtl. wichtig, wenn du je nach Betriebssystem, spezifische Funktionen du verwenden kannst / darfst / musst. :)

[https://www.electronjs.org/docs/latest/api/process#processgetsystemversion](https://www.electronjs.org/docs/latest/api/process#processgetsystemversion){:target="_blank" rel="nofollow"}

```html
<p>
<!-- https://www.electronjs.org/docs/latest/api/process#processgetsystemmemoryinfo -->
The version of the host operating system: 
<script>document.write(process.getSystemVersion())</script> <br />
      
<!-- https://www.electronjs.org/docs/latest/api/process#processgetsystemversion -->
The total amount of physical memory in Kilobytes available to the system: 
<script>document.write(process.getSystemMemoryInfo().total)</script> <br />
      
<!-- https://www.electronjs.org/docs/latest/api/process#processgetcpuusage | First call returns 0. Will always return 0 on Windows.-->
Percentage of CPU used since the last call to getCPUUsage: 
<script>document.write(process.getCPUUsage().percentCPUUsage)</script> <br />
</p>
```

Screen-Recorder (Screencapture) in Electron

Der folgende Screen-Recorder wurde unter Windows getestet.

Hilfreiche Links:

- desktop-capturer:
  [https://www.electronjs.org/de/docs/latest/api/desktop-capturer](https://www.electronjs.org/de/docs/latest/api/desktop-capturer){:target="_blank" rel="nofollow"}
  
- Änderungen in Electron 17.0:
  [https://www.electronjs.org/docs/latest/breaking-changes#planned-breaking-api-changes-170](https://www.electronjs.org/docs/latest/breaking-changes#planned-breaking-api-changes-170){:target="_blank" rel="nofollow"}
  
- MediaRecorder  
  [MediaRecorder - Web APIs | MDN](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder){:target="_blank" rel="nofollow"}
  

## index.hmtl

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <title>Screen-Recorder</title>
  </head>
  <body>
    <div class="form-check form-switch">
      <input class="form-check-input" type="checkbox" id="switch" onclick="checkVideo(this)">
    </div>
    <video></video>
    <hr>
    <button id="startBtn" type="button" class="btn btn-danger">Aufnahme starten</button>
    <button id="stopBtn" type="button" class="btn btn-success">Aufnahme stoppen</button>

    <script src="js/routing.js"></script>
  </body>
</html>

```

## main.js

```javascript

const { app, BrowserWindow, desktopCapturer, ipcMain} = require('electron')

ipcMain.handle(
    'DESKTOP_CAPTURER_GET_SOURCES',
    (event, opts) => desktopCapturer.getSources(opts)
)

function createWindow(){
    const win = new BrowserWindow({
      width: 1400,  
      height: 900,
      webPreferences: {
          nodeIntegration: true,
          enableRemoteModule: true,
          contextIsolation: false
      }  
    })
    win.loadFile('src/index.html')
    //win.webContents.openDevTools()
}

app.whenReady().then(createWindow)

app.on('window-all-closed', () =>{
    app.quit()
})

app.on('activate', ()=>{
    if (BrowserWindow.getAllWindows().length === 0){
        createWindow()
    }
})

```

## routing.js

```javascript

const { desktopCapturer, ipcRenderer } = require("electron");
// querySelector()-Methode durchsucht den Elementbaum nach dem Element 'video'
const video = document.querySelector('video');
// zuweisen des input-Elements 'switch'
const checkbox = document.getElementById('switch');
// Array für die Aufnahme
const aufnahme = []
let mediaRecorder

// Electron-Module initialisieren
const fs = require('fs')
const path = require('path')

// wenn 'switch' aktiv ist, wird die Funktion starteVorschau() aufgerufen
function checkVideo() {
  if (checkbox.checked) {
    starteVorschau();
  } else {
    video.srcObject = null;
  }
}

// Vorschau des Videos wird angezeigt
async function starteVorschau() {
  // Modul 'desktopCapturer' wird aufgerufen
  const desktopCapturer = {
    getSources: (opts) =>
      ipcRenderer.invoke("DESKTOP_CAPTURER_GET_SOURCES", opts),
  };

  // Stream
  const stream = await navigator.mediaDevices.getUserMedia({
    video: {
      mandatory: {
        chromeMediaSource: "desktop",
        minWidth: 1200,
        maxWidth: 1200,
        minHeight: 800,
        maxHeight: 800
      }
    }
  })

  video.srcObject = stream
  video.play()

  // Media Recorder
  const options = { MimeType: 'video/webm; codecs=vp9'}
  mediaRecorder = new MediaRecorder(stream, options)
  mediaRecorder.ondataavailable = verarbeiteAufnahme

  // bei stoppen der Aufnahme, soll das Video gespeichert werden
  mediaRecorder.onstop = dateiSpeichern
}

// Aufnahme verarbeiten
function verarbeiteAufnahme(e) {
  // die einzelnen Sequenzen werden in das Array gespeichert
  aufnahme.push(e.data)
}

// Buttons
const startBtn = document.getElementById('startBtn')
startBtn.onclick = e => {
  // https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder/start
  mediaRecorder.start()
  startBtn.innerText = 'Aufnahme'
}

const stopBtn = document.getElementById('stopBtn')
stopBtn.onclick = e => {
  // https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder/stop
  mediaRecorder.stop()
  startBtn.innerText = 'Start'
}

// Datei speichern
async function dateiSpeichern(e){


  const blob = new Blob(aufnahme, {
    type: 'video/webm; codecs=vp9'
  })
  // https://nodejs.org/api/buffer.html#static-method-bufferfromarray
  // https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer
  // https://developer.mozilla.org/en-US/docs/Web/API/Blob/arrayBuffer
  const buffer = Buffer.from(await blob.arrayBuffer())
  let datei = path.join(__dirname, "../video.webm")
  fs.writeFile(datei, buffer, () => console.log("Datei gespeichert"))
}
```