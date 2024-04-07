---
categories: ['Programmierung']
tags: ['Electron', 'Notification']
title: 'Electron Notifications'
---

## Einleitung

Ein einfaches Beispiel für eine Benachrichtigung in Electron. In den Code-Beispielen befinden sich noch ein paar Kommentare - damit der Code evtl. besser verständlich ist.

## index.hmtl

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
    <title>Notification</title>
  </head>
  <body>
    <!-- input-Felder für Zeitangabe -->
    <input type="text" id="hour" value="Stunde">
    <input type="text" id="minute" value="Minute">
    <input type="text" id="notification" value="Benachrichtigung">
    <!-- Buttons zum Aufruf der Funktionen -->
    <button id ="start" type="button" class="btn btn-info" onclick="startAlarm()">Start</button>
    <button id ="stop" type="button" class="btn btn-info" onclick="stopAlarm()">Stop</button>
    
    <script src="js/routing.js"></script>
  </body>
</html>
```

## main.js

```javascript
const { app, BrowserWindow, ipcMain} = require('electron')

function createWindow(){
    const win = new BrowserWindow({
      width: 800,  
      height: 600,
      webPreferences: {
          nodeIntegration: true,
          enableRemoteModule: true,
          contextIsolation: false
      }  
    })
    win.loadFile('src/index.html')
    win.webContents.openDevTools()
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
// einfache Benachrichtigung die sofort beim öffnen der App aufgerufen wird.
const notification = new Notification("I`m a notification", {
  body: "Notification from render process",
});

// alert() auslösen, wenn auf die Benachrichtigung geklickt wurde.
notification.onclick = () => {
  alert("clicked")
};

let timer;

function startAlarm() {
  // setInterval(function, Interval) Hinweis: (1000ms = 1 Sekunde)
  timer = setInterval(alarm, 1000)
}

function alarm() {
  const alarmHour = document.getElementById("hour")
  const alarmMinute = document.getElementById("minute")
  const alarmNotification = document.getElementById("notification")

  // aktuelle Zeit
  let time = new Date();
  let currentHour = time.getHours()
  let currentMinute = time.getMinutes()
  let currentSecond = time.getSeconds()

  console.log(currentHour + ":" + currentMinute + ":" + currentSecond);

  // wenn aktuelle Zeit und die eingestellte Zeit übereinstimmen, 
  // löst die Benachrichtigung aus
  if (currentMinute == alarmMinute.value && currentHour == alarmHour.value) {
    const notification = new Notification("Alarm notification", {
        body: alarmNotification.value
      });
    // reset des Interval
    clearInterval(timer)
  }
}

// stop-Funktion des Interval
function stopAlarm(){
    clearInterval(timer)
}
```