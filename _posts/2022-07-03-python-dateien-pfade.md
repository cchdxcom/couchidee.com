---
categories: ['Programmierung', 'Python']
tags: ['Python','Dateien']
title: 'Python Dateien und Pfade'
---

Im folgenden Beitrag beschäftigen wir uns mit Dateien und Pfad-Angaben.

Die Punkt-Schreibweise bezieht sich immer auf den aktuellen Ordner, von dem aus das Script gestartet wird. Alle Dateien eines Ordners aufrufen:

```python
import os
# übergeordneter Ordner
print(os.listdir(".."))
# aktueller Ordner
print(os.listdir("."))
# System-Root
print(os.listdir("/"))
```

Wird der Aufruf ohne weitere Konstanten oder Methoden durchgeführt, muss die Datei im selben Verzeichnis liegen, wovon das Script gestartet wurde.

```python
# with open ("parameter.txt", "r") as file:
# oder mit absoluter Pfadangabe
with open ("C:/Users/christian/learning-python/parameter.txt", "r") as file:
    for line in file:
        print(line)
```

Mittels der Konstante `__file__` kannst Du Dir den Pfad inklusive der aktuellen Datei abrufen:

```python
print("__file__: " + __file__)
```

Möchtest Du nur den Ordner sehen, in dem Du dich gerade befindest, nutze:

```python
import os
print("os.path.dirname(__file__): " + os.path.dirname(__file__))
```

Mit `join` können Formatprobleme umgangen werden (z.B.: Slash / Backslash).

```python
import os
with open (os.path.join(os.path.dirname(__file__), "parameter.txt"), "r") as file:
    for line in file:
        print(line)
        print(os.listdir(".."))
```

Pfade mit `join` zusammenbauen funktioniert natürlich auch mit übergeordneten Ordnern.

```python
import os
folder = os.path.join(os.path.dirname(__file__), "../..")
print(folder)
print(os.listdir(folder))
```

Manchmal ist es ziemlich praktisch zu wissen, wo man sich im System gerade befindet. Demnach sollten wir Infos darüber bekommen, ob die in der jeweiligen Ordnerstruktur nur weitere Unterordner sind, oder sich auch Dateien darunter befinden. Also ist der nächste Schritt, Dateien in übergeordnetem Ordner aufzurufen und zu analysieren:

```python
import os 
folder = os.path.join(os.path.dirname(__file__), "..")
# print(os.listdir(folder)) <- liefert Liste zurück

for file in os.listdir(folder):
    file_path = os.path.join(folder, file)
    if os.path.isdir(file_path):
        print(file + " ist eine Ordner")
    else:
        print(file + " ist eine Datei")
```

Für die nächste Übung wollen wir den `os.path.dirname` mit weiteren Parametern bestücken. Erstelle Dir dazu einen Ordner im gleichen Verzeichnis, wo auch dein auszuführendes Script liegt. In diesem Ordner legst Du eine Datei ab. Im Beispiel heißt der Ordner einfach „ordner“ und die darin enthaltene Datei `pw.txt`.

```python
import os
# mehrere Parameter durch Komma trennen
fn = os.path.join(os.path.dirname(__file__), ".", "ordner", "pw.txt")
print(fn)
with open(fn, "r") as file:
    for line in file:
        print(line)
```
