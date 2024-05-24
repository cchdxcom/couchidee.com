---
categories: ['Programmierung', 'Python']
tags: ['Python','Dictionary', 'Dateien', 'csv']
title: 'Python Dictionaries'
---


Dictionaries ermöglichen Dir ein nachträgliches verändern, entfernen und hinzufügen von Daten. Der Key kann z.B. ein Tupel, String, Int oder Float sein.

**Beispiel:**

```python
dictionary = {
    "vorname":"Max",
    "nachname":"Mustermann",
    "stadt":"Beispielhausen",
    "plz":"01234"
}
dictionary["telefon"] = "0123456789"
```

## iterieren und auslesen

Nachdem wir nun ein einfaches Dictionary erstellt haben, wollen durch iterieren und es auslesen

```python
for key in dictionary:
    value = dictionary[key]
    print(key + " -> " + value)
```

## Zugriff über .items()
Zugriff über  **.items()**  -> Liste von Tupeln

```python
print(dictionary.items())
for key, value in dictionary.items():
    print(key + " : " + value)
```

## get-Abfrage

Eine  `get-Abfrage`  beim Dictionary wirft keinen Error, wenn Eintrag nicht vorhanden ist. Stattdessen wird `None` zurückgegeben.

```python
if dictionary["vorname"] == "Max":
    print(dictionary["stadt"])
    print(dictionary.get("telefon")) 
```

```python
if "stadt" in dictionary:
print("Stadt ist enthalten")
```

## Daten löschen

Möchtest Du Einträge aus einem Dictionary löschen, steht Dir  `del`  zur Verfügung.

```python
del dictionary["plz"]
print(dictionary)
```

## Dictionary -> .csv auslesen

Es folgt ein kleines Programm, welches uns den häufigsten Namen aus einer csv-Datei sucht. Dazu kopiere Dir den folgen Code in ein leeres File und nenne es bspw. `n.csv` – der Einfachheit halber hab ich die Datei im gleichen Verzeichnis belassen. Ansonsten kannst Du statt `open(„n.csv“)` auch `open(„../data/n.csv“)` schreiben wenn das File eine Orderebene darüber und in einem separaten Verzeichnis liegt.

Die `n.csv:`

```python
ID,Name,Anzahl,Jahrgang
1,Christian,12,2022
2,Max,9,2022
3,Peter,10,2022
4,Thomas,8,2022
5,Andreas,7,2022
6,Torsten,3,2022
7,Martin,10,2022
8,Christian,13,2021
9,Max,2,2021
10,Peter,14,2021
11,Thomas,3,2021
12,Andreas,2,2021
13,Torsten,9,2021
14,Martin,7,2021
```

Nun benötigst Du noch das eigentliche Programm:

```python
# Dictionary definieren
d = {}

with open("n.csv") as file: # Datei öffnen
    for line in file: # jede Zeile loopen
        splitted = line.strip().split(",") # zerlegen in Elemente
        name = splitted[1] # Namen ziehen
        if name == "Name": # Wenn name = "Name" <- Bezeichnung -> erste Zeile
            continue # überspringe Zeile
        else:
            count = int(splitted[2]) # Setze Zähler (Anzahl Vergebungen)
        if name in d: # wenn Name bereits vorhanden
            d[name] = int(d[name]) + int(count) # addiere Anzahl zusammen
        else:
            d[name] = count # ansonsten setze neuen Eintrag
mostName = max(d, key=d.get) # Filtere Namen mit höchstem Wert
value = d[mostName] # Anzahl = Eintrag aus Dictionary
print("Häufigster Name: " + mostName + " -> " + str(value))
```

Der Vorteil von `with open(„../data/names.csv“) as file:` ist, dass das File nach dem auslesen direkt wieder geschlossen wird.

In einem anderen Artikel erfährst du mehr über das [Öffnen von Dateien in Python]({% post_url 2022-06-30-python-dateien-oeffnen-einlesen %})
