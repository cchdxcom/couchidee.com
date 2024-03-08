---
categories: ['Programmierung']
tags: ['Python', 'Tool']
title: 'Python Lottozahlen Generator'
---

Als kleine praktische Übung bietet sich ein einfacher Lottozahlen-Generator mit Python an.

```python
import random
zahl_1 = [1,2,3,4,5,6,7,8,9]
zahl_2 = [1,2,3,4,5,6,7,8,9]
zahl_3 = [1,2,3,4,5,6,7,8,9]
zahl_4 = [1,2,3,4,5,6,7,8,9]
zahl_5 = [1,2,3,4,5,6,7,8,9]
zahl_6 = [1,2,3,4,5,6,7,8,9]
zahl_7 = [1,2,3,4,5,6,7,8,9]
lottozahlen = [zahl_1,zahl_2,zahl_3,zahl_4,zahl_5,zahl_6,zahl_7]

lottozahlen_print = []

for zahl in lottozahlen:
    # Zufallszahlen aus einer Liste
    r = random.randint(0,len(zahl)-1)
    # einfügen der auserwählten Zahl in die lottozahlen_print-Liste
    lottozahlen_print.append(str(zahl[r]))
 # print("Die Lottozahlen lauten: " + " " + str(lottozahlen_print))
# .join fasst alle durchlaufenen Werte im lottozahlen_print zu einem String zusammen
print("Die Lottozahlen lauten: " + " ".join(lottozahlen_print))
```
