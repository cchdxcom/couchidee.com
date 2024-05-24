---
categories: ['Programmierung', 'Python']
tags: ['Listen']
title: 'Python Listen'
---

Ein Array bzw. eine Liste wird erstellt, indem man rechteckige Klammern `[...]` verwendet. Eine befüllte Liste könnte nun so aussehen:

```python
language = ["PHP","C", "C++", "Java", "Ruby"]
```

## .pop()

mit `.pop()` kannst Du den letzten Eintrag entfernen

```python
languagePop = language.pop()
```

In der neuen Variable sollte nun der letzte Eintrag, also „Ruby“ gespeichert sein.
Überprüfe kannst Du dies mit:

```python
print(languagePop)
# Ausgabe = Ruby
```

Die neue Liste kannst nun natürlich auch überprüfen mit:

```python
print(language)
# Ausgabe = ['PHP', 'C', 'C++', 'Java']
```

## .append()

mit `.append()` kannst Du eine Liste erweitern bzw. ein neues Element anhängen.

```python
language.append(languagePop)
print(language)
# Ausgabe ['PHP', 'C', 'C++', 'Java', 'Ruby']
```

Mehrere Listen können durch `+` einfach zusammengefügt werden. Erstelle zum Test eine zweite, neue Liste mit mehreren Elementen.

```python
languageAppend = ["JavaScript", "Go", "R"]
language = language + languageAppend
print(language)
# Ausgabe = ['PHP', 'C', 'C++', 'Java', 'Ruby', 'JavaScript', 'Go', 'R', 'HTML']
```

## del

mit `del` kannst Du einen bestimmten index einer Liste löschen
Da ein Array bzw. eine Liste wie immer beim Index 0 beginnt, wird nun das 3. Element „Java“ entfernt.
Element 0 = PHP -> Element 1 = C -> Element 2 = C++ -> Element 3 = Java …

```python
del language[3]
print(language)
# Ausgabe = ['PHP', 'C', 'C++', 'Ruby', 'JavaScript', 'Go', 'R', 'HTML']
```

## remove

Mit `remove` kannst Du Elemente mittels „Bezeichnung“ löschen

```python
language.remove("PHP")
print(language)
# Ausgabe = 'C', 'C++', 'Ruby', 'JavaScript', 'Go', 'R', 'HTML']
```

Manchmal ist es notwendig, dass letzte Element nochmal aufzurufen, oder Du möchtest einfach gesagt, von hinten auf das Array zugreifen. Dafür gibt es die Minus-Schreibweise:

```python
last_entry = language[-1]
print(last_entry)
# Ausgabe = HTML
t = "Test"
print(t[-1])
# Ausgabe =  ergibt 't
```

## von:bis

Du kannst natürlich auch eine Teilkopie einer Liste erstellen mit `[von:bis]`

```python
language_copy = language[2:5] # language[2:-1] vorletztes Element | language[2:]
print(language_copy)
# Ausgabe = ['Ruby', 'JavaScript', 'Go']
```

Das gleich funktioniert auch beim slicing von Strings mit `[von:bis]`

```python
temp = "JavaScript"
slice = temp[0:4] # oder auch "JavaScript"[0:4] wäre möglich
print(slice)
# Ausgabe = Java
slice2 = temp[-6:]
print(slice2)
# Ausgabe: Script
```

## List Comprehension

Listen-Abstraktion (`List Comprehension`) kannst Du im Grunde als vollständigen Ersatz für den Lambda-Operator, sowie die Funktionen `map`, `filter` und `reduce` ansehen.

```python
xs = [1, 2, 3, 4, 5, 6, 7, 8]
ys = [x * x for x in xs]
print(xs)
print(ys)
# Ausgabe: [1, 2, 3, 4, 5, 6, 7, 8]
# Ausgabe: [1, 4, 9, 16, 25, 36, 49, 64]
```

siehe [https://docs.python.org/3.8/tutorial/datastructures.html](https://docs.python.org/3.8/tutorial/datastructures.html).

## Listen verschachteln

Ein Liste, gefüllt mit weiteren Listen:

```python
lists = [
    ["Python", "PHP", "Ruby", "C", "C++", "C#"],
    ["SQL", "PLSQL", "NoSQL", "MariaDB", "MongoDB"]
]
print(lists[0][0]) # Python
print(lists[1][3]) # Maria DB
```

Auch ein Dictionary lässt sich mit weiteren Listen befüllen:

```python
students = {
    "Klasse_1": ["Max", "Peter", "Ralf", "Edgar"],
    "Klasse_2": ["Franz", "Petra", "Klaus", "Monika"]
}


print(students["Klasse_1"]) # ['Max', 'Peter', 'Ralf', 'Edgar']
```

Das Abrufen von Werten aus verschachtelten Listen ist relativ einfach. Mit entsprechenden Loops könnten wir einfach der Reihe nach alle Listen durchlaufen und die Daten verarbeiten.