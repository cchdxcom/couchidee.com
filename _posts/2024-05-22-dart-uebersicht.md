---
categories: ['Programmierung', 'Dart']
tags: ['Dart', 'Übersicht']
title: 'Dart Grundlagen Übersicht'
---

## Einleitung
Dart ist eine objektorientierte Programmiersprache, die von Google entwickelt wurde. Sie wurde erstmals 2011 vorgestellt und ist speziell darauf ausgelegt, sowohl Client- als auch Serveranwendungen zu erstellen. Dart wird besonders häufig in Kombination mit dem Framework Flutter verwendet, um plattformübergreifende mobile und Web-Anwendungen zu entwickeln.

### Merkmale von Dart

- **Einfach und modern:** Dart ist einfach zu erlernen und bietet moderne Sprachmerkmale wie optionale Typen, Futures und Streams.
- **Hohe Leistung:** Dart-Code wird zu nativen Maschineninstruktionen kompiliert, was eine hohe Ausführungsleistung ermöglicht.
- **Plattformübergreifend:** Dart unterstützt die Entwicklung für verschiedene Plattformen, darunter Mobile (iOS und Android), Web und Desktop.

### Hauptanwendungsgebiete

1. **Mobile App-Entwicklung (Flutter):**
Dart ist die Hauptsprache für [Flutter](https://flutter.dev/){:target="_blank" rel="nofollow"}, ein beliebtes Open-Source-Framework von Google zur Entwicklung von nativ kompilierten Anwendungen für mobile, webbasierte und Desktop-Plattformen aus einer einzigen Codebasis. Mit Flutter und Dart können Entwickler schnell leistungsstarke, plattformübergreifende Apps erstellen.

2. **Webentwicklung:**
Dart kann direkt in JavaScript transpiliert werden, wodurch es möglich ist, Dart für Webanwendungen zu verwenden. Dies wird durch das Webdev-Tooling und das AngularDart-Framework unterstützt.

3. **Serverseitige Entwicklung:**
Dart kann auch für serverseitige Anwendungen verwendet werden. Mit Paketen wie Aqueduct oder Shelf können Entwickler Web-APIs und Backend-Dienste erstellen.

4. **Desktop-Anwendungen:**
Mit der Erweiterung von Flutter für den Desktop können Anwendungen für Windows, macOS und Linux entwickelt werden. Dies ermöglicht die Erstellung von Anwendungen mit einer einzigen Codebasis, die auf verschiedenen Desktop-Betriebssystemen laufen.

## Programmiereigenschaften

Dart ist eine vielseitige und moderne Programmiersprache, die mehrere Eigenschaften bietet, um die Entwicklung effizienter und robuster Anwendungen zu unterstützen. Hier sind einige der wichtigsten Programmiereigenschaften von Dart:

### Objektorientiert
Dart ist eine objektorientierte Sprache, was bedeutet, dass alles in Dart als ein Objekt betrachtet wird, inklusive Funktionen und Typen. Dies fördert die Wiederverwendbarkeit und Modularität des Codes.

### Statische und dynamische Typisierung

Dart unterstützt sowohl statische als auch dynamische Typisierung. Standardmäßig verwendet Dart eine starke statische Typisierung, die viele Fehler schon zur Kompilierzeit erkennt. Gleichzeitig kann man jedoch durch das Verwenden des Schlüsselworts var oder durch explizite Typdeklarationen wie dynamic dynamisch typisierte Variablen nutzen.

```dart
int number = 42; // statisch typisiert
var text = "Hello"; // der Compiler leitet den Typ als String ab
dynamic anything = 5; // dynamisch typisiert, Typ kann sich ändern
```

### Optionale Typen

Dart unterstützt optionale Typen, was bedeutet, dass Typannotationen nicht zwingend erforderlich sind, aber verwendet werden können, um den Code klarer und sicherer zu machen.

### Null-Safety

Dart bietet [Null-Sicherheit](https://dart.dev/null-safety){:target="_blank" rel="nofollow"}, was bedeutet, dass Variablen standardmäßig keine Null-Werte annehmen können, es sei denn, sie sind explizit als nullable deklariert. Dies hilft, viele häufige Fehler wie Nullreferenzausnahmen zu vermeiden.

```dart
int? nullableNumber; // nullable
int nonNullableNumber = 42; // non-nullable
```

### Asynchrone Programmierung

Dart hat eingebaute Unterstützung für asynchrone Programmierung mittels [async und await](#async--await-erklärung) Schlüsselwörtern sowie Future- und Stream-APIs. Dies erleichtert die Handhabung von zeitaufwändigen Operationen wie I/O-Operationen oder Netzwerkanfragen.

```dart
Future<void> fetchData() async {
  var data = await http.get('https://www.couchidee.com/data');
  print(data.body);
}
```

### Sprachkonstrukte und -features
Dart bietet verschiedene Sprachkonstrukte und Features, die die Programmierung erleichtern:

- **Klassendefinitionen und Vererbung:** Unterstützung für objektorientierte Paradigmen wie Klassen, Vererbung und Mixins.
- **Generics:** Ermöglicht die Erstellung von wiederverwendbarem Code durch Typ-Parameter.
- **Lambdas und Closures:** Unterstützung für anonyme Funktionen und Closures. -> siehe [Lambda](#lambda-funktionen-arrow-funktion)

### Bibliotheken und Pakete

Dart hat ein robustes Paketverwaltungssystem namens [Pub](https://pub.dev/){:target="_blank" rel="nofollow"}, das eine große Anzahl von Bibliotheken und Paketen enthält, um die Entwicklung zu unterstützen. Diese Pakete können leicht in Projekten integriert werden.

### Plattformübergreifende Entwicklung

Mit Flutter können Anwendungen mit einer einzigen Codebasis für verschiedene Plattformen wie iOS, Android, Web und Desktop entwickelt werden. Dies ist einer der Hauptvorteile von Dart und Flutter.

### Hot Reload

In Verbindung mit Flutter unterstützt Dart das `Hot Reload` Feature, welches Entwicklern erlaubt, Änderungen im Code sofort in der laufenden Anwendung zu sehen, ohne dass die Anwendung neu gestartet werden muss. Dies beschleunigt die Entwicklungs- und Debugging-Prozesse erheblich.

## Grundlagen

### Variablen

```dart
int number = 12;
double x = 1.23456;
String name = "Mustermann";
bool wahrFalsch = true;
const konstante = 42;
var whatever;
dynamic blablubb;
```

### null / nullable

```dart
double? a = null; // darf null sein
int? koennteJaNullSein; // darf null sein
a ??= 4; // wenn a null, wird 4 zugewiesen
```

### if, else if, else

```dart
if (name == "Mustermann") {
  ...
} else if (x < y) {
  ...
} else {
  ...
}
```

### Switch Case

```dart
switch (userInput) {
    case "Beispiel": 
      ...
      break; 
    case "Mustermann": 
      ...
      break; 
    default:
      ...
  }
```

### for-Loop

```dart
for (int i = 0; i < 100;) {i++;}
for (int x = 100; x > 0; x--) {...}
```

### foreach

```dart
List<int> list = [1, 2, 3, 4];
List<String> list2 = ["eins", "zwei", "drei", "vier"];
Map<int, String> map = {1: "one", 2: "two", 3: "three"};

list2.forEach((element) {...});
map.forEach((key, value) {...});
```

### for-in

```dart
List<int> list = [1, 3, 5, 7];
for (int x in list) {
  print(x);
}
```

### while-Loop

```dart
while (i <= 10) {...}
```

### Logische Operatoren & Modulo

```dart
if (fall1 && fall2) {...}
if (fall3 || fall4) {...}
if (fall1 && (fall2 || x == 1)) {}
if (i % 2 == 1) {...} // Modulo
```

### Funktionen

```dart
void main() {
  String name = "blablubb";
  print(Vorname(name));
}

String Vorname(name) {
  String value = "Hallo " + name;
  return value;
}
```

### Lambda Funktionen (Arrow-Funktion)

Lambda-Funktionen sind nützlich, wenn Du eine kurze, einmalige Funktionalität benötigst, ohne eine separate benannte Funktion zu definieren. Sie werden häufig als Callbacks oder für funktionale Programmierung verwendet. Die Arrow-Syntax `=>` macht Lambda-Funktionen in Dart kompakt und lesbar.

```dart
// Reguläre Funktion
int addNumbers(int a, int b) {
  return a + b;
}

void main() {
  // Lambda-Funktion zuweisen an eine Variablen
  var sumLambda = (int a, int b) => a + b;

  print(addNumbers(2, 3)); // Ausgabe: 5
  print(sumLambda(2, 3)); // Ausgabe: 5

  // Lambda direkt als Argument übergeben
  var numbers = [1, 2, 3, 4, 5];
  numbers.forEach((num) => print(num * 2)); // Ausgabe: 2, 4, 6, 8, 10
}
```

### Try Catch

```dart
try {
    int? x = null;
    int? y = 3;
    int ergebnis = x! + y; // ! sicher, dass variable kein null ist
  } catch (exception) { // bei Fehler, landet man im catch-Block
    print(exception);
  } finally { // finally wird IMMER ausgeführt
    ...
  }
```

### Map

Eine Map ist eine ungeordnete Sammlung von Schlüssel-Wert-Paaren. Jeder Schlüssel ist einzigartig und mit einem Wert verknüpft. Maps eignen sich gut, um Daten nach bestimmten Kriterien (Schlüsseln) zu organisieren und abzurufen.

- Maps speichern Schlüssel-Wert-Paare, z.B. `{'name': 'John', 'age': 30}`
- Schlüssel müssen eindeutig sein, Werte können dupliziert werden
- Der Zugriff auf Werte erfolgt über die Schlüssel
- Maps sind ungeordnet, die Reihenfolge der Elemente ist nicht garantiert

```dart
Map<String, int> map = {"eins": 1, "zwei": 2, "drei": 3};
// in eine Map können auch weitere Maps als Key eingefügt werden
// ebenso sind Objekte, Listen usw. möglich

map["zwei"] = 8; // Manipulieren
map.remove("drei"); // löschen

Map<N, S> map = new Map<String, Sportart>();
map["Fussball"] = new Customer("Fussball", 11);
map["Volleyball"] = new Customer("Volleyball", 5);
map["Handball"] = new Customer("Handball", 6);
```

### List

Eine List ist eine geordnete Gruppe von Objekten. Die Elemente in einer Liste haben eine feste, numerische Position, über die auf sie zugegriffen werden kann.

- Listen speichern Objekte in einer bestimmten Reihenfolge, z.B. `[1][2][3]`
- Elemente werden über einen Index (Position) abgerufen
- Listen sind geordnet, die Reihenfolge der Elemente bleibt erhalten
- Duplikate sind erlaubt

```dart
List<int> list = [1, 3, 5];

list.add(7); // hinzufügen
list.remove(3); // entfernen
list[0] = 2; // manipulieren
list.insert(2, 6); // einfügen an bestimmtem Index
list.removeAt(2); // enfernen an bestimmten Index
list.removeAt(list.length - 1);

List<String> vereine = ["Volleyball", "Fussball"];
vereine.add("Handball");
```

### Queue - (First in first out)

```dart
Queue<T> queue = new Queue<Bestellung>();
queue.add(new Bestellung("AMD Ryzen"));
queue.add(new Bestellung("BeQuiet Gehäuse"));
queue.add(new Bestellung("MSI Mainboard"));
```

### Set

- Sets sind ungeordnete Sammlungen von eindeutigen Elementen
- Jedes Element kommt nur einmal vor, Duplikate sind nicht erlaubt
- Der Zugriff auf Elemente erfolgt nicht über einen Index, sondern durch Iteration
- Beispiel: `var set = {'a', 'b', 'c'}; set.add('a');` -> `...add('a');` wird ignoriert, da `a` bereits vorhanden

```dart
var vereine = {'Volleyball', 'Fussball', 'Handball'};
// oder
var vereine = <String>{};
// Entspricht: Set<String> vereine = {};
// oder
Set<T> set = new Set<Verein>();
set.add(new Verein("Volleyball"));
set.add(new Verein("Fussball"));
set.add(new Verein("Handball"));
```

### Enum

Enum steht für `enumerated type` oder `enumerierter Datentyp`. Enums werden verwendet, um eine Gruppe zusammengehöriger Konstanten zu definieren.


```dart
Nutzer nutzer1 = Nutzer();
if (nutzer1.geschlecht == Geschlecht.Maennlich) { // Vergleich
  ...
}

class Nutzer {
  late String name;
  late Geschlecht geschlecht = Geschlecht.Maennlich; 
}

enum Geschlecht { Maennlich, Weiblich, Divers, keineAngabe } // enum definieren
```

### var, Final, const

```dart
var a;
a = 2;
a = "Christian";
a = true;

var b = 2; // var INITIALISIEREN führt zu Typisierung
// b = "bla"; -> Fehler

final c;
c = 9; // c = 0; -> // Fehler
// final darf 1x (EIN MAL!) zur Laufzeit gesetzt werden
// darf aber nur deklariert und musss zur Laufzeit gesetzt werden

const d = 3; // const muss sofort initialisiert werden (kann nicht wieder geändert werden)
```

### extension

```dart
// extension = erweitert Klassen usw.
// -> geeignet für z.B.: Libraries, da der originale Code nicht verändert wird
extension drittel on int {
  double eindrittel() {
    double drittel = this / 3;
    return drittel;
  }
}
```

### async Future

Das Schlüsselwort `async` wird verwendet, um eine asynchrone Funktion zu kennzeichnen. Eine asynchrone Funktion kann die Ausführung anhalten und auf eine asynchrone Operation wie z.B. eine Netzwerkanfrage oder Dateioperationen warten, ohne den gesamten Programmfluss zu blockieren.

**Hier die wichtigsten Punkte zu async in Dart:**

- `async` definiert eine Funktion als asynchron.
- Innerhalb einer async Funktion kann das Schlüsselwort `await` verwendet werden, um auf die Fertigstellung einer asynchronen Operation zu warten, bevor der Code fortfährt.
- Eine **async Funktion gibt immer ein Future-Objekt zurück**, das den eventuellen Wert der Funktion repräsentiert.
- async und await ermöglichen es, asynchronen Code in einem ähnlichen Stil wie synchronen Code zu schreiben, was die Lesbarkeit und Wartbarkeit verbessert.
- async Funktionen können verwendet werden, um Streams mit `await for` zu verarbeiten.

```dart
// async definieren
void main() async {
  print("Erste Ausgabe");
  var result = await multiple(3, 3); // await - wartet, bis Funktion abgeschlossen ist
  print("Zweite Ausgabe");
}

Future<void> multiple(int a, int b) {
  int c = a * b;
  print("Ausgabe der Funktion...");
  return Future.delayed(Duration(seconds: 2)); // Duration verzögert den Abschluss der Aufgabe
}
```

#### weiteres async Beispiel

```dart
import 'dart:convert';
import 'dart:io';

Future<void> main() async {
  var client = HttpClient();
  var request = await client.getUrl(Uri.parse('https://www.google.com/'));
  var response = await request.close();

  if (response.statusCode == HttpStatus.ok) {
    print("Response Code successful");
  } else {
    print("Response Code error");
  }
  client.close();
}
```

### async / await Erklärung

#### async

- Das Schlüsselwort `async` wird verwendet, um eine Funktion als asynchron zu kennzeichnen.
- Eine async-Funktion führt Operationen aus, die eine gewisse Zeit in Anspruch nehmen können, z.B. Netzwerkanfragen oder Dateioperationen.
- Anstatt den Programmfluss zu blockieren, gibt eine async-Funktion sofort ein Future-Objekt zurück, das den eventuellen Wert der Funktion repräsentiert.
- Beispiel: `Future<String> getData() async { ... }`

#### await

- Das Schlüsselwort await kann nur innerhalb einer async-Funktion verwendet werden.
- `await` pausiert die Ausführung der async-Funktion, bis das angegebene Future-Objekt abgeschlossen ist und einen Wert liefert.
- Mit await kann asynchroner Code geschrieben werden, der wie synchroner Code aussieht, was die Lesbarkeit erhöht.
- Beispiel: `String data = await getData();`

#### Hauptunterschied

- `async` definiert eine Funktion als asynchron und gibt ein Future zurück.
- `await` wartet innerhalb einer async-Funktion auf die Fertigstellung eines Future-Objekts

### Stream

In Dart ist ein Stream eine Sequenz von asynchronen Ereignissen (Events). Es ist wie eine asynchrone Iteration, bei der die Ereignisse empfangen werden, sobald sie bereit sind, anstatt dass man nach dem nächsten Ereignis fragt.
Ein einfaches Beispiel:
```dart
import 'dart:async';

void main() {
  // Erstelle einen Stream von Zahlen
  Stream<int> zahlenStream = Stream.fromIterable([1, 2, 3, 4, 5]);

  // Höre auf den Stream und gib jedes Ereignis aus
  zahlenStream.listen((zahl) {
    print(zahl); // Ausgabe: 1, 2, 3, 4, 5
  });
}
```

Streams sind nützlich, wenn Du mit asynchronen Daten arbeitest, die nach und nach eintreffen, wie z.B. Benutzereingaben, Netzwerkantworten oder Inhalte aus Dateien. Anstatt auf alle Daten zu warten, kannst du mit Streams jedes Ereignis verarbeiten, sobald es eintrifft.

**Weitere Möglichkeiten mit Streams:**

- Streams transformieren mit map, where etc.
- Fehlerbehandlung mit handleError
- Broadcast-Streams für mehrere Listener
- Async-Funktionen wie await for zum Iterieren über Streams
- Streams sind ein leistungsfähiges Konzept in Dart für die reaktive, asynchrone Programmierung