---
categories: ['Programmierung']
tags: ['Python', 'Queue', 'Priority Queue', 'csv', 'Dateien', 'Datenstrukturen']
title: 'Python Queue und Priority Queue'
---

Die priority queue ist eine lineare Datenstruktur, in der die Daten nach dem „first in – first out“ (FIFO-) Prinzip verwaltet werden. Das erste eingefügte Element wird auch wieder als erstes entfernt. Andere Elemente können nicht entfernt werden.

csv Beispiel (`file.csv`)

```python
Name;Alter;Wohnort
Christian;35;Musterstadt
Harald;42;Beispielhausen
Tom;32;Beispielstadt
Anne;39;Musterhausen
```

In dem folgenden Beispiel verwenden wir  queue.PriorityQueue(). Dieses erzeugt eine priorisierte (sortierte) Warteschlange.

```python
import csv
names = {}

# csv einlesen
with open("file.csv") as file:
    reader = csv.reader(file, delimiter=';', quotechar='"')
    counter = 0
    for line in reader:
        if counter != 0:
            number = int(line[1])
            name = line[0]
            names[name] = number
        counter = counter + 1

import queue
pq = queue.PriorityQueue()

for name, number in names.items():
    pq.put([number, name])

for i in range(0, 4):
    print(pq.get())
```

Eine normale Warteschlange ohne Sortierung erzeugst Du mit  `queue = []`  und  `.append()`.

```python
queue = []
# hinzufügen von Elementen
queue.append('a')
queue.append('b')
queue.append('c')
print(queue)

# entfernen von Elementen
print(queue.pop(0))
print(queue.pop(0))
print(queue.pop(0))

print(queue)
```

