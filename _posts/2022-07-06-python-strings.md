---
categories: ['Programmierung', 'Python']
tags: ['Python', 'Strings']
title: 'Python Strings Funktionen und Formatierung'
---

Unterschiedlichste Elemente lassen sich am einfachsten mit `str()` in einen String umwandeln.

```python
n = 5
print("Ich habe " + str(n) + " Vögel.")
print("I got " + str(n) + " birds.")
```

Lösung mit Dictionary

```python
n = 5
translations = {
"number_of_dogs" : "Ich habe XXX Hunde"
"number_of_cats" : "Ich habe XXX Katzen"
}
print(translations["number_of_dogs"].replace("XXX", str(n)))
print(translations["number_of_cats"].replace("XXX", str(n)))
```

Eine beliebte Lösung sind Platzhalter

```python
n = 5
translation = {
"number_of_dogs" : "Ich habe {0} Hunde"
"number_of_birds" : "Ich habe {0} Vögel"
}
print(translation["number_of_dogs"].format(n))
print(translation["number_of_birds"].format(n))
```

kurze Schreibweise:

```python
a = "Hunde"
n = 5
print("Ich habe {0} Hunde".format(n))
print("Ich habe {0} {1}".format(n,"Hunde"))
print("Ich habe {0} {1}".format(n,a))
# Zahlen gerunden ausgeben
print("Pi hat den Wert: {0:.3f}".format(3.141529))

print("Ich habe {number:.3f} {animal}".format(number = 5, animal = "Hunde"))
```

In diesem Beitrag schauen wir uns die verschiedenen Möglichkeiten der String-Funktionen an:

### .upper() und .lower()

```python
print("Hallo Welt".upper()) # HALLO WELT
print("Hallo Welt".lower()) # hallo welt
```

### auf Satzzeichen prüfen

```python
satz = "- Hallo Du?"
if satz[-1] == "?":
print("Der Satz enthält ein Fragezeichen!")

# prüft am Ende
if satz.endswith("?"):
print("Der Satz enthält ein Fragezeichen!")

# prüft am Anfang
if satz.startswith("-"):
print("Der Satz enthält einen Anstrich!")
```

### alle Leerzeichen entfernen

```python
word = " Test!! "
print(word.strip()) # Test!!
```

### definierte Zeichen mit .strip entfernen

```python
word2 = " . . Test!! $ "
print(word2.strip(" .!$")) # Test

# lstrip entfernt alle definierten Zeichen LINKS
word3 = "........Test....."
print(word3.lstrip(" .")) # Test.....

# lstrip entfern alle definierten Zeichen RECHTS
word3 = "........Test....."
print(word3.rstrip(" .")) # ........Test
```

### erste Position eines Zeichens finden

```python
s = "Dies ist ein kleiner Test."
print(s.find(".")) # = Position 25
print(s[25]) # . -> Wird ein Zeichen nicht gefunden = -1

# ersetzt Teil des Strings
print(s.replace("kleiner", "großer")) # Dies ist ein großer Test.
```