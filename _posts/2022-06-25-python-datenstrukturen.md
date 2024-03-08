---
categories: ['Programmierung']
tags: ['Python', 'Datenstrukturen']
title: 'Python Datenstrukturen'
---

Liste = [ … ] - Eine Eigenschaft bei Listen ist es, dass sie Ihre Sortierung beibehalten, wenn wir Daten aus ihr abrufen.

```python
language = ["Python", "PHP", "Java", "Go"]
user = ['6517', '5987', '8932', '1382']
temp = zip(language, user)
print(dict(temp))
# Ausgabe: {'Python': '6517', 'PHP': '5987', 'Java': '8932', 'Go': '1382'}
```

## Tupel = ( … )

Tupel werden verwendet, wenn Daten unveränderbar gespeichert werden sollen. Tupel können alle Arten von Elementen speichern.

```python
tupel = ("Python", "PHP", "Java", "Go")
print (tupel)
```

## Set = { … }

Bei Sets kann es passieren, dass die Sortierung verloren geht. Beim erstellen eines Sets ist es ebenfalls wichtig, darauf zu achten, dass jeder Wert nur 1x im Set enthalten sein. Wenn die Position nicht wichtig ist, kann überprüft werden, ob der jeweilige Wert im Set enthalten ist. Im Übrigen sind Set auf die Suche von Werten optimiert.

```python
set = {"Python", "Java"}
set.add("Python")
```

### Set in Variable

```python
content = "Dies Demo ist Demo ein Demo Text Demo" # Demo wird nur 1x im Set aufgenommen
words = set()
for word in content.split(" "):
words.add(word)
print(words)
print(len(words))
```

## Queue -> Warteschlange

Werte in Queue zu speichern ist dann sinnvoll, wenn Du eine die Daten nach dem `first in- / first out`-Prinzip abrufen möchtest.

```python
import queue
q = queue.Queue()

# Eintrag hinzufügen

q.put("Python")
q.put("PHP")
q.put("Java")
q.put("Ruby")
q.put("Javascript")
q.put("C++")

# .get gibt das erste Element wieder aus
print(q.get())
print(q.get())
```

### Queue leeren -> Elemente ausgeben

```python
while not q.empty():
    element = q.get()
    print(element)
print("Noch ein Wert da? -> " + q.get()) -> keine Ausgabe
```

### Priority Queue -> Warteschlange die automatisch sortiert

```python
import queue
pq = queue.PriorityQueue()

pq.put([1, "Gaaaanz Wichtig"])
pq.put([5, "Wichtig"])
pq.put([15, "Nicht so wichtig"])

print(pq.get())

pqm = queue.PriorityQueue()

# Absteigende Sortierung
pqm.put([-1, "Gaaaanz Wichtig"])
pqm.put([-5, "Wichtig"])
pqm.put([-15, "Nicht so wichtig"])

print(pqm.get())
```

Priority Queues können natürlich auch verwendet werden um berechnete / gezählte Werte direkt sortiert abzuspeichern.

```python
text = "A A A A A A A B B B B B B C C C C D D D D D D D D E E E E E F F G H H H"
d = {}
for word in text.split(" "):
if word in d:
d[word] = d[word] + 1
else:
d[word] = 1

pql = queue.PriorityQueue()
for word, number in d.items():
pql.put([number, word])

while not pql.empty():
element = pql.get()
print(element)
```