---
categories: ['Programmierung', 'Python']
tags: ['Python','Dateien', 'csv']
title: 'Python Dateien öffnen und einlesen'
---

Dateien lassen sich in Python mit `open()` öffnen. Je nach Anwendungsfall musst Du den entsprechenden Parameter setzen. Ein Nachteil von `open()` gegenüber `with open(…) as file` ist, dass Datei manuell geschlossen werden müssen. `with open(…) as file` schließt die Dateien selbstständig, wenn alles erledigt ist.

`r` = Datei zum Lesen öffnen. (Standard)  
`w` = Datei zum Schreiben öffnen. Erstellt eine neue Datei, wenn sie nicht existiert. Inhalt wird überschrieben.  
`x` = Öffnet eine Datei zur exklusiven Erstellung. Wenn die Datei bereits vorhanden ist, schlägt der Vorgang fehl.  
`a` = Öffnen zum Anhängen am Ende der Datei, ohne sie zu überschreiben. Erstellt eine neue Datei, falls sie nicht existiert.  
`t` = Im Textmodus öffnen. (Standard)  
`b` = Im Binärmodus öffnen.  
`+` = Öffnen einer Datei zum Aktualisieren (Lesen und Schreiben)

## Beispiel

Erstelle eine Datei (data.txt) mit irgendeinem Inhalt, bestenfalls über mindestens 2 Zeilen.

```python
# Beispiel
Du hast die Datei erfolgreich ausgelesen.
Glückwunsch!
```

Nun benötigst Du natürlich noch den eigentlichen Code.

```python
file = open("data.txt", "r") # Datei öffnen -> "r" = read
for line in file:
    # jede Zeile ausgeben, strip() entfernt Charakters wie Leerzeichen, Zeilumbrüche etc
    print(line.strip())
file.close()
```

Möchtest Du etwas in Dateien schreiben, beachte den entsprechenden Parameter (siehe oben)

```python
# in Datei schreiben -> w = write / überschreiben
file = open("write.txt", "w")
array = ["Thueringen", "Sachsen", "Bayern", "Niedersachsen"]
for i in array:
    # \n fügt Zeilumbruch zu jeder Zeile (i) hinzu
    file.write(i + "\n")
# Damit fehlerfrei gespreichert wird, sollte Datei immer geschlossen werden
file.close()
```

```python
file = open("write.txt", "a")
temp = "Hessen"
file.write(temp + "\n")
# Bei Fehlern wird close() nicht erreicht
file.close()
```

## with open(...) as file

```python
# with open(...) as file: schließt die Datei selbstständig
temp = "Sachsen-Anhalt"
with open("write.txt", "a") as file:
file.write(temp + "\n")
```

## Dateien einlesen und ausgeben

Mit dem folgenden kleinen Programm wird eine Datei eingelesen und in verschiedenen Formen wieder ausgegeben.

```python
# Klasse um Datei zu laden und 
class FileReader():
    # Initialisierung der Klasse
    def __init__(self, file):
        # Definition der Liste (gehört nur der Klasse)
        self.importedFile = []
        # Datei öffnen mit "with open" -> Datei wird automatisch geschlossen
        with open(file,"r") as openfile:
            # Zeile für Zeile durchgehen
            for line in openfile:
                # Zeileninhalt (ohne Steuerzeichen) nacheinander in die Liste einfügen
                self.importedFile.append(line.strip())

    # Methode zum abrufen der Liste
    def getfile(self):
        return self.importedFile

# Klasse um csv einzulesen
class CsvReader(FileReader):
    # Initialisierung der Klasse
    def __init__(self, file):
        # super() greift auf die überschriebenen geerbten Methoden der Klasse FileReader zu
        # super() wird in untergeordneten Klassen (mit Mehrfachvererbung) verwendet,
        # dadurch kann auf Funktionen der Klasse zugegriffen werden (z.B. getFile() ).
        super().__init__(file)
        # Aufruf der Methode
        self.transformToCsv()

    def transformToCsv(self):
        # neue Liste initialisieren
        csv = []
        # Zeile für Zeile durchgehen
        for line in self.importedFile:
            # jedes ELement in neue Liste
            entity = []
            # entfernen von Steuerzeichen und Trennung der Wörter beim Komma
            splitted = line.strip().split(",")
            # Variablen aus den Daten ziehen
            firstName = splitted[1][1:]
            surname = splitted[0]
            # Daten in die "untergeordnete" Element-Liste eintragen
            entity.append(firstName + ", " + surname)
            # Daten in die csv-Liste schreiben
            csv.append(entity)
            # Rückgabe der gesamten csv-Liste
        return csv

    def getfile(self):
        # Methode zum abrufen der csv-Liste
        return self.transformToCsv()

test = FileReader("testfile.txt").getfile()
print(test)
# Ausgabe: ['Nachname, Vorname', 'Meister, Ingo', 'Schuster, Manfred', 'Mueller, Hans', 'Schmidt, Klaus']
test2 = CsvReader("testfile.txt").getfile()
print(test2)
# Ausgabe: [['Vorname, Nachname'], ['Ingo, Meister'], ['Manfred, Schuster'], ['Hans, Mueller'], ['Klaus, Schmidt']]
```
