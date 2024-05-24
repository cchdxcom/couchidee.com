---
categories: ['Programmierung', 'Python']
tags: ['Python', 'Exceptions', 'Dateien']
title: 'Python Exceptions'
---

Auch in Python lassen sich natürlich Fehler ordentlich abfangen. `try / except`  werden folgendermaßen eingesetzt:

```python
try:
    print(5/0)
except ZeroDivisionError:
    print("Teilen durch 0 ist nicht erlaubt")
```

Sinn und Zweck von `try / except` erkennst Du, wenn Du die Berechnung innerhalb des `print()` einfach ohne `try/except` ausführst.

```python
try:
    with open ("datei.xyz", "r") as file:
    print(file)
except FileNotFoundError:
    print("Die Datei konnte nicht geöffnet werden.")
```

## mehrere exceptions abfangen

```python
try:
    print(5/0)
    with open ("datei.xyz", "r") as file:
        print(file)
except FileNotFoundError:
    print("Die Datei konnte nicht geöffnet werden.")
except ZeroDivisionError:
    print("Teilen durch 0 ist nicht erlaubt")
```

## eigene exceptions

Eigene Fehlerklassen lassen sich ebenfalls definieren. Hierbei ist der Klassenname von besonderer Bedeutung – Inhalt muss nicht zwingend vorhanden sein. In dem Fall reicht ein einfaches `pass`.

```python
class InvalidEmailError(Exception):
    pass
```

Testen wir nun eine eigene Fehlerklasse, indem wir einen Fehler provozieren:

```python
def send_mail(email, subject, content):
    if not "@" in email:
        raise InvalidEmailError("Kein @-Zeichen vorhanden.")
# raise nur bei seltenen (kritischen) Fehlern verwenden
try:
    send_mail("Hallo.email.com", "Betreff", "Inhalt")
except InvalidEmailError:
    print("Bitte gültige Email einfügen")
```

## finally

Um nicht jeden möglichen Fehler abfangen zu müssen, führt `finally` am Ende die angegebene Anweisung IMMER aus. Im Beispiel wird einfach die Datei geschlossen, die unter `try` geöffnet wird.

```python
try:
    file = open("../data.txt", "r")
    print(file)
    print(20/x)
except FileNotFoundError:
    print("Datei nicht gefunden!")
finally:
    print("Die Datei wurde geschlossen...")
    file.close()
```
