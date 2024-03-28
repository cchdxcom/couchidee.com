---
categories: ['Programmierung']
tags: ['Electron','Menü']
title: 'Electron App-Menü und Kontext-Menü'
---

## Menü Grundlagen

Jede Anwendung in Electron bringt bereits ein vordefiniertes Standard-Menü mit, solange du kein eigenes Menü erstellt hast.

[https://www.electronjs.org/de/docs/latest/api/menu](https://www.electronjs.org/de/docs/latest/api/menu)

Definiert wird das eigene Menü innerhalb der `function createWindow()`

Für Mac OSX muss zusätzlich die Plattform abgefragt werden: siehe [https://www.electronjs.org/de/docs/latest/api/menu#beispiele](https://www.electronjs.org/de/docs/latest/api/menu#beispiele)

## Eigenes App-Menü erstellen

Um eine eigenes Menü verwenden zu können, musst du zuerst das Paket `Menu` importieren. Das könnte z.B.: so aussehen:

`const { app, Menu } = require("electron");`

Ein einfaches Grundgerüst wäre:

```javascript
// in einem Array werden die einzelnen Menüpunkte 
// als einzelne Objekte angelegt
const menuTemplate = [ /* Hier muss das Menü rein*/]

// Anwendungsmenü wird mit dem Inhalt des Templates erstellt
const menu = Menu.buildFromTemplate(menuTemplate);

// eigenes Menü wird als Standard festgelegt 
//und überschreibt das default-Menu von Electron
Menu.setApplicationMenu(menu);
```

## Beispielcode

Nachfolgend nun ein Beispielmenü. Daran wird deutlich, wie das Grundgerüst aufgebaut ist.

```javascript
// eigenes Menu
  const menuTemplate = [
    {
      label: "Menü 1",
      submenu: [
        {
          label: "Log-Meldung ausgeben",
          click(){
            console.log("Menü1 - DropDown 1 wurde gedrückt");
          },
        },
        {
          label: "Dokumentation zum Menü aufrufen",
          // kürzere Form des Click-Events
          click(){
            // Shell wird in der Regel automatisch importiert, sobald es verwendet wird
            shell.openExternal(
              "https://www.electronjs.org/de/docs/latest/api/menu"
            );
          },
        },
        // MenuItem(options) - Verwendung von type
        { type: "separator" },
        // Standard-Keyword mit vordefinierter Funktion
        {
          label: "Programm schließen",
          click(){
            app.quit();
          }
        }
      ]
    },
    {
      label: "Bearbeiten",
      submenu: [
        { role: "toggleDevTools", label: "DevTools öffnen" }
      ]
    }
  ]
```

### Hinweise zu roles, type und options

Electron bietet dir für die Menüs häufig genutzte Funktionen als `role` (mit vordefiniertem Verhalten) an. z.B.: `copy`, `paste`, `quit` und viele mehr... Um sie zu nutzen muss nur das jeweilige Schlüsselwort verwendet werden.

Siehe im Beispiel oben:

`{ role: "toggleDevTools", label: "DevTools öffnen" }`

Auch unter `MenuItem` findest du bereits vordefinierte Typen ( `type` = normal, separator, checkbox usw.) oder auch Tooltips, Submenüs usw.

Siehe im Beispiel oben:

`{ type: "separator" }`

Mehr Informationen findest du unter:

https://www.electronjs.org/de/docs/latest/api/menu-item

## Kontextmenu

Um ein eigenes Kontextmenü zu erstellen benütigst du wieder zuerst einen entsprechenden Import von `MenuItem`:

`const { app, Menu, MenuItem } = require("electron");`

Identisch zum App-Menü wird das Kontextmenu in der Funktion `function createWindow()` definiert.

Um das Kontextmenu nun dem rechtsklick-Event hinzuzufügen, benötigst du die Web-Content-Eigenschaften vom `BrowserWindow`

## Beispielcode

```javascript
 const kontextMenu = new Menu();
  kontextMenu.append(
    new MenuItem({
      label: "Klick",
      click(){
         console.log("Klick registriert...") 
      }
    })
  );
  // Verwendung von type
  kontextMenu.append(new MenuItem({type: "separator"}))

  // Verwendung von role
  kontextMenu.append(new MenuItem({role: "selectAll", label: "alles markieren"}))

  mainWindow.webContents.on("context-menu", function (e, params) {
    // params.x / params.y geben die Koordinaten des Mauszeigers zurück
  kontextMenu.popup(mainWindow, params.x, params.y);
  });
```