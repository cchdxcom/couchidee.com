---
categories: ['Programmierung', 'Python']
tags: ['Python', 'Funktionen', 'matplotlib']
title: 'Python Funktionen'
---

Eine ganz einfache Funktion, der Du einen Wert übergeben kannst, sieht so aus:

```python
def greets(name):
    # str() wandelt in String, falls z.B. eine Zahl eingegeben wird
    print("Hallo " + str(name))

greets("Christian")
```

In Funktionen können natürlich auch weitere Funktionen oder Loops definieren sein. Probieren wir es mit einem einfachen for-loop:

```python
def test(name, count):
    for i in range(0,count):
        print("Dies ist der " + str(i+1) + ". Test von " + name)

test("Max Mustermann", 2)
```

Ein weiteres Beispiel einer Funktion mit if/else:

```python
def max(a, b):
    if a > b:
        return a
    else:
        return b

testvar = max(234,872)
print(testvar)
```

Auch Listen oder Sonstiges kann direkt an Funktionen übergeben werden. Ein Beispiel:

```python
cart_prices = [10, 1.55, 14.49, 18.49, 3.79, 17.29]
def list_sum(l):
    summe = 0
    for price in l:
        summe = summe + price
    print(summe)

list_sum(cart_prices)
```

Erstellen wir uns eine weitere Funktion und berechnen mal, wieviel 1 – 10 Artikel eines beliebigen Artikels kosten:

```python
def preisliste(name, preis):
    array = []
    for i in range(1,11):
        zs = i*preis
        array.append(str(i) + "x: " + name + ": " + str(zs))
    return array

print(preisliste("Chips", 0.79))
```

## Funktionen und Parameter

Standardparameter erlauben es, Funktionen ohne Parameter aufzurufen

```python
def own_print(content = "Müller", count= 5, sign = "Max "):
    for i in range(0, count):
    print(sign + content)

own_print("Mustermann", 7, "Peter ")
own_print(count = 2)
```

### Funktion mit primitiven Datentypen

```python
a = 5
def f(x):
print(x)

print(a)
f(a)
```

### Übergeben von Datenstrukturen an Funktionen

```python
l = ["Test","Muster"]
def f2(x):
    x.append("!")
    print(x)
f(l)
print(l)
```

```python
l = ["Test","Muster"]
def f2(x):
    # neue Liste
    x = ["Test","Muster", "!!!!"]
print(x)
f2(l)
print(l)
```

Eine weitere Möglichkeit Listen an Funktionen übergeben

```python
liste = [12,23,34]
def f3(a,b,c,):
    print(a)
    print(b)
    print(c)
# Stern(*) bedeutet Liste
f3(*liste)
```

### Variable Anzahl an Parametern übergeben

```python
zahlen = [1,2,3,4,5,5,6,7,8,9,0]

# Parameter werden als Tupel gespeichert
def calculate_max(current_max, *params):
    for item in params:
        if item > current_max:
            current_max = item
    return current_max

max = calculate_max(*zahlen)
print("Die größte Zahl ist: " + str(max))
```

### Dictionary übergeben

```python
def f5(**args):
    print(args)

f5(key="value", param="parameter")
```

```python
def f6(**args):
    print(args)
d = {"key": "Schlüssel", "param":"Parameter"}
# f6(key=d[key], param=d[param])
f6(**d)
```

### Beispiel mit MatPlotLib

```python
import matplotlib.pyplot as plt
def create_plot(**plot_params):
    plt.plot([1,2,3,3,4], [7,8,8,9,9], **plot_params)
    plt.show()

create_plot(color="r",linewidth=10, linestyle="dotted")
```
