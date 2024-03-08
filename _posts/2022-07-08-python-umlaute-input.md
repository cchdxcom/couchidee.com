---
categories: ['Programmierung']
tags: ['Python', 'Input', 'Umlaute', 'Dateien']
title: 'Python Umlaute und Input'
---

Damit Python vernünftig mit Umlauten (in Dateien) umgeht, musst Du utf-8 nutzen.

```python
import os
filename = os.path.join(os.path.dirname(__file__), "umlaute.txt")

# Datei einlesen mit utf-8
with open (filename, "r", encoding="utf-8") as file:
    for line in file:
        print(line)
# Datei schreiben mit utf-8
filename_out = os.path.join(os.path.dirname(__file__), "umlaute_out.txt")
with open (filename_out, "w", encoding="utf-8") as file:
    file.write("Müller")
```

Um Konsolenprogramme ein wenig zum Leben zu erwecken, ist ein Eingabe- bzw. Input-Funktion ganz nützlich. Probieren wir ein einfaches Beispiel:

```python
age = input("Bitte gib dein alter ein: ")
age2 = input("Bitte gib das alter deines Partners ein: ")

print(age + ", " + age2)

sum = int(age) + float(age2)
print("Alter zusammen: " + str(sum))
```
