---
categories: ['Programmierung', 'Python']
tags: ['Python', 'OOP', 'Vererbung']
title: 'Python Objektorientierung'
---

Eine Klasse wird mit `class` definiert. Nachfolgend wirst Du häufiger das Wort Methode statt Funktion lesen. Das kommt daher, dass eine Funktion innerhalb einer Klasse Methode genannt wird. Die Möglichkeiten und die Deklaration sind identisch. Zu beachten ist bei den Klassen: um auf Attribute des Objekts zugreifen zu können, muss  self  übergeben werden.

```python
class Tree():
    def getInfo(self):
    print(self.name + " ist ein " + self.art + " aus " + self.land + ".")

class Car():
    def getInfo(self):
    print(self.name + " ist ein " + self.art + " aus " + self.land + ".")
```

Um nun ein Objekt zu erstellen, reicht ein  `x = Methode()`. Um das Objekt mit Leben zu füllen, schreibst Du  `x.eigenschaft = „Eigenschaft“`.

```python
bmw = Car()
bmw.name = "BMW"
bmw.art = "Kraftfahrzeug"
bmw.land = "Deutschland"

birke = Tree()
birke.name = "Birke"
birke.art = "Laubbaum"
birke.groesse = "30m"
birke.land = "Deutschland"

zeder = Tree()
zeder.name = "Zeder"
zeder.art = "Nadelbaum"
zeder.groesse = "50m"
zeder.land = "USA"
```

Um nun unsere Methode aufzurufen, notieren wir:

```python
birke.getInfo() # Birke ist ein Laubbaum aus Deutschland.
zeder.getInfo() # Zeder ist ein Nadelbaum aus USA.
```

Außenstehende Funktionen lassen sich für alle Objekte mit vorhandener Methode ausführen. Beispiel:

```python
def doubleInfo(l):
l.getInfo()
l.getInfo()

doubleInfo(birke)
doubleInfo(bmw)
```

## weiteres Beispiel

```python
class Teacher():
    def __init__(self, firstname, lastname):
        self.firstname = firstname
        self.lastname = lastname
        # Namenskonvention -> auf Variablen mit einem Unterstrich soll nicht direkt zugegriffen werden -> nur über Methode
        self._classes = 0

        # __var = 2 vorangestellte Unterstriche = PRIVATE Variable -> Zugriff verboten
        self.__year = 0

    def getName(self):
        name = self.firstname + " " + self.lastname
        return name

    def getClasses(self):
        return self._classes

    def setClasses(self, classes):
        self._classes = classes

    def getYear(self):
        return self.__year

    def setYear(self, year):
        self.__year = year

    def __privateMethode(self):
        print("Diese Methode ist privat.")
```

Testen wir nun unsere Klasse:

```python
schroedinger = Teacher("Harald", "Schrödinger")
schroedinger.setClasses("3")
schroedinger.setYear("1963")
# schroedinger.__year = 1987 würde fehlschlagen

print(schroedinger.getName() + " (Jahrgang: " + schroedinger.getYear() + ")" + " betreut " + str(schroedinger.getClasses()) + " Klassen.")
```

## Beispiel Würfel

Wir erstellen eine Klasse Würfel, mit der wir einen Würfel modellieren. Die Klasse soll als Eigenschaft die Länge einer Seite besitzen und darüber hinaus soll die Klasse auch zwei Methoden haben:

- `volumen()`  berechnet das Volumen und gibt es aus,
- `oberflaeche()`  berechnet die Oberfläche und gibt sie aus.

```python
class Wuerfel():
    def __init__(self, l):
        self.l = l

def volumen(self):
    volumen = self.l * self.l * self.l # oder self.l ** 3
    return print( "Würfel: Volumen -> " + str(volumen))

def oberflaeche(self):
    oberflaeche = (self.l * self.l) * 6 # self.l ** 2 * 6
    return print( "Würfel: Oberfläche -> " + str(oberflaeche))
```

Zum testen benötigen wir Folgendes:

```python
# Instanz der Klasse erzeugen
a = Wuerfel(3)

# und testen die Methoden
a.oberflaeche() # 54
a.volumen() # 27
```

## Konto-Beispiel

Das folgende Beispiel lässt sich gut um Input-Eingabe erweitern:

```python
class Account():
    def __init__(self, k, pin):
        self.__k = k
        self.__pin = pin

def display(self):
    print("Kontostand: " + str(self.__k))

def pay_in(self, pay_in):
    self.__k = self.__k + pay_in


def withdraw(self, withdraw, pin):
    if self.__pin == pin:
        if withdraw > self.__k:
            print("Vorgang nicht möglich. Das Guthaben beträgt nur: " + str(self.__k) + "€")
        else:
            self.__k = self.__k - withdraw
    else:
        print("Vorgang nicht möglich, falsche PIN!")

Kunde111 = Account(500, "1234")
Kunde111.display()
Kunde111.pay_in(40)
Kunde111.display()
Kunde111.withdraw(25, "1234")
Kunde111.display()
Kunde111.withdraw(600, "12345")
```

## Bus-Übung

Die nächste Übung ist etwas komplizierter:

Wir erstellen uns eine Bus-Route. Bei `route` handelt es sich um eine Liste mit den Bushaltestellen.  `position` steht für den Index der Haltestelle aus der Liste, an dem sich der Bus gerade befindet bzw. von dem er zuletzt abgefahren ist. Die Methode `zeigeHaltestelle()` soll der Name dieses Bahnhofs ausgegeben werden.

```python
class Bus():
    def __init__(self, route, position):
        self.route = route
        self.position = position

    def zeigeHaltestelle(self):
        print("Der Bus befindet sich in: " + self.route[self.position])
        if self.position == len(self.route) - 1:
            print("Endstation! Alle aussteigen")

    def fahre(self):
        if self.position < len(self.route)-1:
            self.position = self.position + 1
        else:
            print("Der Bus ist bereits am Ziel angekommen!")

    def fahreZurueck(self):
        if self.position > 0:
            self.position = self.position - 1
        else:
            print("Der Zug befindet sich bereits am Startpunkt!")
```

### testen wir unsere Bus-Route

```python
Dtour = Train(["H1", "H2", "H3", "H4"], 0)
Dtour.zeigeHaltestelle()
Dtour.fahre()
Dtour.zeigeHaltestelle()
Dtour.fahre()
Dtour.zeigeHaltestelle()
Dtour.fahre()
Dtour.zeigeHaltestelle()
Dtour.fahre()
Dtour.fahreZurueck()
Dtour.zeigeHaltestelle()
```

Im nächsten Beispiel wird auch näher auf die Objekttypen eingegangen.

```python
class Teacher():
    def __init__(self, fn, sn):
        self.fn = fn
        self.sn = sn

def name(self):
    return self.fn + " " + self.sn

class VHSTeacher(Teacher):
    def __init__(self, fn, sn, vhs):
        super().__init__(fn,sn)
        self.vhs = vhs

def name(self):
    return self.fn + " " + self.sn + " leitet die Kurse: " + self.vhs

teacher1 = Teacher("Peter", "Müller")
teacher2 = VHSTeacher("Klaus", "Schulze", "Informatik")

print(type(teacher1)) # type zeigt die Klasse an
print(type(teacher2))

if type(teacher1) == Teacher:
    print("Wird nur angezeigt, wenn type == Student")

if isinstance(teacher1, VHSTeacher):
    print("Wird angezeigt für VHS-Lehrer")

if isinstance(teacher2, Teacher):
    print("Wird für alle Lehrer (inkl. Vererbung) angezeigt")

teachers = [
    Teacher("Peter", "Müller"),
    VHSTeacher("Klaus", "Schulze", "Informatik"),
    Teacher("Harals", "Maier"),
    VHSTeacher("Petra", "Schmidt", "BWL")
]

for teacher in teachers:
    if isinstance(teacher, VHSTeacher):
        print(teacher.fn + " " + teacher.sn + " leitet den Kurs: " + teacher.vhs)
```

## Übung Vererbung

```python
class Student:
def __init__(self, firstname, surname):
    self.firstname = firstname
    self.surname = surname

def getName(self):
    return self.firstname + " " + self.surname


class WorkingStudent(Student):
    # bei def __init__ wird self immer übergeben + delegierte Parameter
    def __init__(self, firstname, surname, company):
        # bei Vererbung wird kein self übergeben
        super().__init__(firstname, surname)
        self.company = company

# Methoden können überschrieben werden
def getName(self):
    # return print("WorkingStudent: " + self.firstname + " " + self.surname + " -> " + self.company)
    return super().getName() + " " + self.company + " "


max = Student("Steve", "Mustermann")
dom = WorkingStudent("Steve", "Mustermann", "ABCDEF AG")

students = [
    WorkingStudent("Steve", "Mustermann", "Google Inc."),
    Student("Shawn", "Müller"),
    Student("Dave", "Vogel"),
    WorkingStudent("Martin", "Schmidt", "Alphabet AG")
]

for student in students:
    print(student.getName())

print(max.getName())
print(dom.getName())
```
