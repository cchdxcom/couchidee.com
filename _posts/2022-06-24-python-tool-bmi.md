---
categories: ['Programmierung', 'Python']
tags: ['Python', 'Tool']
title: 'Python BMI-Rechner'
---

Als kleine praktische Übung bietet sich ein simpler BMI-Rechner mit Python an.

```python
# Funktion definieren mit den Parametern Gewicht und Größe
def bmi_calc(gewicht, groesse):
    # speichern der input-Werte und ersetzen der Kommas durch Punkte (float-Werte)
    gewicht = gewicht.replace(",",".")
    groesse = groesse.replace(",",".")
    # Formel zur Berechnung des BMI
    bmi = float(gewicht) / float(groesse) ** 2
    # Rückgabe des Wertes
    return bmi

print("BMI-Rechner: ")
# Eingabe der Werte über Konsole
gewicht = input("Bitte gib dein Gewicht in KG ein: ")
groesse = input("Bitte gib deine Größe in Meter ein: ")

# Übergabe der Input-Werte an die Funktoin
bmi = bmi_calc(gewicht, groesse)

# Ausgabe des berechneten Wertes
print("Dein BMI ist: {0:.2f}".format(bmi))
```
