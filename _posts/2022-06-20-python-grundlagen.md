---
categories: ['Programmierung', 'Python']
tags: ['Python']
title: 'Python Grundlagen Tutorial'
---

Die absoluten Basics beginnen damit, dass Du weißt, das Kommentare mit dem `#`-Symbol gekennzeichnet werden und mit der Funktion `print()` Inhalte auf der Python-Konsole ausgibt.
```python

print("Dies ist der erste Test.")
```

Wie Du siehst, wird in Python kein Semikolon oder ähnliches benötigt. Ein einfacher Zeilenumbruch reich aus, um einen neuen Befehl anzugeben. Geben wir nun eine Reihe von kleinen Berechnungen aus.

```python
print(10)
print(5+5)
print(2*5)
print(10/2)
```

Kommazahlen werden, wie in anderen Programmiersprachen auch, immer mit `.` statt `,` angegeben. Bei der Verwendung von Ganzzahlen oder Kommazahlen musst Du keine Unterscheidung beachten, anders als z.B. in C. Python-intern werden die Zahlen aber natürlich unterschiedlich gewertet.

```python
print(10+2.5)
print((3+3)*3)
```

Wenn Du ausschließlich Zahlen ausgibst, funktioniert die Ausgabe problemlos. Jedoch darfst Du auch in Python Zahlen und Text, also Strings nicht ohne Weiteres miteinander mischen. Die folgende Ausgabe wird daher einen Fehler hervorrufen.

```python
print("Das ist die Zahl: " + 5)
```

Abhilfe schafft hier die Funktion `str()` – Damit wird die Zahl 5 nicht mehr als Wert sondern als Zeichkette (String) ausgegeben.

```python
print("Das ist die Zahl: " + str(5))
```

Im obigen Beispiel wird das `+` nicht zum addieren verwendet, sondern dient zum verketten von Werten.

## Variablen

um Werte zwischen zu speichern gibt es wie überall natürlich auch in Python Variablen. Ein einfaches Beispiel mit Zahlen:

```python
a = 5 + 5 # 10
b = 2 + 2 # 4
c = a + b # 14
print(c) 
# Ausgabe = 14
print(c * c) 
# Ausgabe = 196
print("Die Summe von a und b = " + str(c)) 
# Ausgabe = Die Summe von a und b = 14
```

und noch ein weiteres Beispiel:

```python
wert_1 = 123
wert_2 = 345
wert_3 = 789
avg = (wert_1 + wert_2 + wert_3) / 3
print("Der Durchschnittwert beträgt: " + str(avg))
# Ausgabe = Der Durchschnittwert beträgt: 419.0
```

**Ein einfaches Beispiel mit Strings:**
Strings (Zeichenketten) müssen immer in `„…“` oder `‚…‘` eingefasst werden. Die ist zur Trennung der einzelnen Datentypen (z.B. Strings, Zahlen) notwendig.

```python
name = "Christian"
print("Mein Name ist: " + name)
# Ausgabe = Mein Name ist: Christian
```

## Listen

Listen (ähnlich dem klassischen Array) ermöglichen Dir eine Vereinfachung, wenn Du mehrere Werte verwenden möchtest. Statt zu jedem Wert eine Variable zu definieren, kannst Du eine wie folgt einfach eine Liste erstellen.

```python
programmiersprache_1 = "PHP"
programmiersprache_2 = "Python"
programmiersprache_3 = "C++"
programmiersprache_4 = "Java"
```

Du siehst, das ist relativ viel Tipperei, einfacher ist die Liste:

```python
programmiersprachen = ["PHP", "Python", "C++", "Java"]
print(programmiersprachen)
print("Ich lese grade einen Blog zum Thema " + programmiersprachen[1])
# Ausgabe: Ich lese grade einen Blog zum Thema Python
```

Das Feld „Python“ wird mit der `programmiersprachen[1]` abgerufen, da Python Listen und Arrays **IMMER** bei 0 starten. Dies ist grundsätzlich in allen Programmiersprachen so – nicht nur in Python. `programmiersprachen[0]` wäre also „PHP“.

### Anzahl der Elemenente in der Liste ausgeben = `len()`

```python
print("In der Liste 'programmiersprachen' befinden sich " + str(len(programmiersprachen)) + " Elemente.")
# Ausgabe: In der Liste 'programmiersprachen' befinden sich 4 Elemente.
```

Halt, HTML ist nur eine Auszeichnungssprache und keine echte Programmiersprache. Also entfernen wir einfach den letzten Eintrag mit `.pop()` aus unserer Liste und erstellen eine neue Liste mit Auszeichnungssprachen. Dazu kann die Funktion `.pop()` den Wert an eine Variable zurückgeben (`return`).

```python
temp = programmiersprachen.pop()
auszeichnungssprachen = [temp]
print("Programmiersprachen: " + str(programmiersprachen))
print("Auszeichnungssprachen: " + str(auszeichnungssprachen)

# Ausgabe = Programmiersprachen: ['PHP', 'Python', 'C++']
# Ausgabe = Auszeichnungssprachen: ['Java']

print("Nun befinden sich in der Liste 'programmiersprachen' nur noch " + str(len(programmiersprachen)) + " Elemente.")
# Ausgabe = Nun befinden sich in der Liste 'programmiersprachen' nur noch 3 Elemente.
```

Möchten wir nun auch C++ aus der Mitte der Liste löschen, setzt Du den entsprechenden Zähler ein.

```python
programmiersprachen.pop(2)
print("Programmiersprachen: " + str(programmiersprachen))
# Ausgabe = Programmiersprachen: ['PHP', 'Python']
```

## Daten umwandeln

Das Ergebnis von `print( 9 + „9“)` wäre ein Fehler. Also müssen wir den zweiten Wert, also „9“ von einem String in eine Zahl umwandeln. Mit der Funktion `int()` wird aus einem String eine (GANZE) Zahl. Ebenso wie `str()` aus Zahlen einen String erstellt. Übrigens würde `int(„9.5“)` nicht funktionieren, da die Funktion `int()` für Integer (ganzen Zahlen) steht. Für Kommazahlen gilt `float()`.

### String in Zahl

```python
print(9 + int("9"))
```

### String in Kommazahl

```python
a = "3"
b = "4.9"
print(int(a)+float(b))
```

### Zahl in String

```python
alter = 1980
print("Max Mustermann wurde " + str(alter) + " geboren." )
```

### Liste in String

```python
programmiersprachen = ["PHP", "Python", "C++", "Java"]
print(", ".join(programmiersprachen))
# Ausgabe = PHP, Python, C++, Java
programmiersprachen_string = ", ".join(programmiersprachen)
print("Wir kennen bereits die Programmiersprachen " + programmiersprachen_string)
# Ausgabe = Wir kennen bereits die Programmiersprachen PHP, Python, C++, Java
```

### String in Liste

Mit `.split` kannst Du eine Zeichenkette / String anhand eines von Dir definierten Zeichens trennen. Mit `abc.split(„, „)` geben wir an, dass immer beim Komma getrennt werden soll.

```python
bundeslaender_string = "Thueringen, Sachsen, Bayern, Niedersachsen"
bundeslaender_liste = bundeslaender_string.split(", ")
print(bundeslaender_liste)
# Ausgabe = ['Thueringen', 'Sachsen', 'Bayern', 'Niedersachsen']
```

Möchten wir beispielsweise aus einer E-mail wie `Max-Mustermann@posteo.de` nur den Namen extrahieren, können wir folgendes tun:

```python
mailadresse = "Max-Mustermann@posteo.de"
n_names = mailadresse.split("@")[0].split("-")
print("Hallo " + " ".join(n_names))
# Ausgabe = Max Mustermann
```

#### Zur Erklärung:

mit `[0]` greifen wir auf das erste Element der Liste zu, die `.split()` erstellt
das Element aus `.split(„@“)[0]` ist („Max-Mustermann„), dieses splitten wir gleich nochmal, nämlich am Bindestrich `.split("-")`
Möchten wir nur die Domain extrahieren, sieht das so aus:

```python
mailadresse = "info@mustermann.com"
domain = mailadresse.split("@")[1].split(".")[0]
fullDomain = mailadresse.split("@")[1]
print("Domain: " + domain)
print("Domain: " + fullDomain)
```

#### Beispiel: Anzahl der Wörter (Elemente) mit len() ermitteln

```python
text_string = "Lorem ipsum dolor sit amet, consetetur sadipscing elitr, sed diam nonumy eirmod tempor invidunt ut labore et dolore magna aliquyam erat, sed diam voluptua."
text_liste = text_string.split(" ")
print("Die Wortanzahl beträgt: " + str(len(text_liste)) + " Wörter.")
# Ausgabe = Die Wortanzahl beträgt: 24 Wörter.
```

Wir können natürlich auch mit `.join()` verschiedene Zeichenketten wieder zusammen setzen: Am Beispiel E-Mail könnte es so aussehen:

```python
mailParts = ["Mustermann", "google.com"]
neueMail = "@".join(mailParts)
print(neueMail)
```

## if / else

Damit wir auf Basis von Werten oder Variablen Entscheidungen treffen können, benötigen wir `if / else`.
Ein einfaches Beispiel:

```python
zahl = 30
if zahl < 20:
    print("Zahl kleiner 20")
else:
    print("Zahl größer 20")

print(10 > 20) # ergibt false
print(10 < 20) # ergibt true
print(10 == 10) # == prüft auf Gleichheit (inkl. Datentyp) -> True
print(10 != 10) # != prüft auf Ungleichheit (inkl. Datentyp) -> False
```

Übrigens werden Boolean (boolische Werte) in Python immer groß begonnen:

```python
temp = False
```

### if / else verschachteln

```python
bmi = 22.5
    if bmi >= 18.5:
        if bmi <= 24.9:
           print("Der BMI ist normal")
    else:
        print("Der BMI zeigt auf Übergewicht")
else:
    print("Der BMI zeigt Untergewicht")

if bmi >= 18.5 and bmi <= 24.9:
    print("Der BMI ist normal")
# or
bmi = 33
if bmi <= 18.5 or bmi >= 24.9:
    print("Der BMI ist nicht optimal")
```

### if / else verknüpfen
Verknüpfungen Werte lassen sich einfach mittels Klammern bewerkstelligen:

```python
land = "DE"
alter = 18

if (land == "DE" and alter <= 21) or (land != "DE" and alter >= 21):
    print("wird ausgeführt")
```

### if / else vergleichen
Natürlich können wir für unsere `if`-Abfrage auch vergleichen, ob sich ein bestimmter Wert in einer Liste befindet:

```python
pr_lang = ["Python", "PHP", "Java", "C++"]
pr_lang_input = "HTML"
if pr_lang_input in pr_lang:
    print("Dein gewählte Sprache '" + pr_lang_input + "' ist eine Programmiersprache.")
else:
    print("Dein gewählte Sprache '" + pr_lang_input + "' ist keine Programmiersprache.")
```

### if / else suche in Variable
Suchen in Variablen und eine entsprechende Reaktion und Aktion ist ebenso möglich:

```python
content = "Dies ist der erste Beispielsatz. Und hier der zweite von zwei Bespielsätzen."
if "ä" in content:
    print("Es ist ein Umlaut vorhanden. Umlaut wird ersetzt...")
# .replace ersetzt z.B Zeichen in Zeichenketten

new_content = content.replace('ä', 'ae')
print("Der neue Text lautet: " + new_content)
```

Genauso wie wir suchen können, ob ein Wert vorkommt (`if wert in string`), können wir auch fragen, ob ein Wert explizit nicht vorkommt (`if wert not in string`).

```python
blocked_user = ["User_123", "User 0238", "User_349", "Player_026"]
user_name_input = "Player_222"
if user_name_input not in blocked_user:
    print("Der Benutzer ist verfügbar!")
```

### if -> elif -> else
Die `elif`-Abrage ähnelt der `if`-Abfrage. Jedoch wird `elif` immer nur nach `if` notiert und nur aufgerufen, wenn die `if`-Abfrage nicht `True` war.

```python
wert = 4
if wert == 1:
    print("Der Wert ist 1")
elif wert == 2:
    print("Der Wert ist 2")
elif wert == 3:
    print("Der Wert ist 3")
else:
    print("Der Wert ist größer 3")
```

## Schleifen und Loops

### while-Loop
solange die Bedingung wahr ist, wird die `while`-Schleife ausgeführt.

```python
z = 0
while z < 5:
    print(z)
    z = z + 1
```

### for-Loop
Mit der `for`-Schleife kannst Du alles innerhalb dieser Schleife so oft wiederholen, bis zum Beispiel eine Liste abgearbeitet ist. Siehe Beispiel:

```python
language = ["Python", "PHP", "Java", "C++"]
for i in language:
    if i == "Python":
        print(i + " ist eine Programmiersprache und ich lerne sie gerade")
    else:
        print(i + " ist eine Programmiersprache")
```

### continue
Mit `continue` wird die Schleife direkt ohne eventuelle Folgeanweisungen fortgeführt

```python
for j in range(1,4):
    if j == 2:
        continue
    print(j)
```

### break
Bei `break` wird die aktuelle Schleife abgebrochen

```python
for j in range(1,4):
    if j == 2:
        break
    print(j)

list = [1,2,3,4,5,6]
summe = 0
for element in list:
summe = summe + element
    if summe >= 9:
        print("Die Summe ist: " + str(summe))
        break
```
