# Operatoren in C
{: .reading}

Mit einem Operator werden üblicherweise **Ausdrücke** miteinander verknüpft. Ein Ausdruck ist eine Kombination aus Variablen, Konstanten, Operatoren und Rückgabewerten von Funktionen. Die Auswertung eines Ausdrucks ergibt einen Wert. 

**Beispiele von Ausdrücken:**
````cpp
x
3*y
pow(2)
x + 3*y + pow(3)
````

# Was ist ein Operator
{: reading}

Den Operator ``=`` haben wir bereits kennengelernt, er setzt (engl. assign) eine Variable auf einen bestimmten Wert.

Ein **Operator** ist letztlich eine *Funktion unter anderem Namen* und *anderer Notation* welche ein Programm leserlicher macht. Die Werte die an einen Operator übergeben werden (die Parameter einer Funktion) werden **Operanden** genannt.

**Beispiel**
- `assign(a, add(b, c))` wird zu `a = b + c`
- Die Funktion `assign` wird zum Operator `=`
- Die Funktion `add` wird zum Operator `+`

In C sind alle Operatoren **in der Sprache eingebaut** und können nicht vom Benutzer neu oder umdefiniert werden.

# Zuweisungsoperator

Mit dem Operator ``=`` können Werte zugewiesen werden. Der Zuweisungsoperator hat zwei Operanden. Als erstes wird der Ausdruck auf der rechten Seite berechnet, anschließend wird der berechnete Wert im linken Operanden gespeichert.

**Beispiele**
````cpp
i = d + 10;
````
````cpp
counter = counter + 1;
````
````cpp
squaremeter = length * length;
````

Die erste Zuweisung an eine Variable bezeichnet man als **Initialisierung** dieser Variable. Idealerweise sollte das **gleichzeitig mit der Deklaration** der Variable geschehen.

**Beispiele**
````cpp
int i = 0;
````
````cpp
double d = 0.0;
````
````cpp
int max_height = 245;
````

> Nicht initialisierte Variablen haben **keinen definierten Wert** in C!

# Arithmetische Operatoren

Die Gruppe der arithmetischen Operatoren bilden die üblichen Rechenoperationen ab die man kennt:
- Addition: ``a + b``
- Subtraktion: ``a - b``
- Multiplikation: ``a * b``
- Division: ``a / b``
- Modulo (Rest einer Division): ``a % b``

> Achtung: Das Symbol ``^`` entspricht **nicht** der Potenzierfunktion.

Alle arithmetischen Operatoren, außer dem Modulo-Operator, können sowohl auf Ganzzahlen als auch auf Gleitkommazahlen angewandt werden. Arithmetische Operatoren haben immer zwei Operanden.

## Besonderheiten der Division

Der Divisionsoperator kann zu **unerwarteten Ergebnissen** führen.

### Division durch 0
Eine **Division durch 0** liefert ein undefiniertes Ergebnis wenn eine Integerdivision ausgeführt wird und normalerweise hat dies den Absturz des Programms zur Folge. Bei einer Fließkommadivision ist eine Division durch 0 generell eine gültige Rechnung und man bekommt entweder +inf/-inf wenn eine beliebige positive oder negative Zahl durch 0.0 dividiert wird bzw. nan (not a number) wenn man 0.0, oder inf durch 0.0 dividiert.

### Integerdivision
Wenn beide Operanden Ganzzahlen sind (``char`` oder ``int``) dann wird eine **Integerdivision** durchgeführt. Bei einer Integerdivision werden **Kommastellen gar nicht erst berücksichtigt**. Im Endeffekt wird eine **Division mit Rest** durchgeführt wie man sie von der Schule her kennt und der Rest verworfen. Den Rest der Division bekommt man mit dem Modulo Operator ``%``.

**Beispiel**
```cpp
#include <stdio.h>
int main()
{
  int a = 2;
  int b = 3;
  double c = a / b;
  printf("%f\n", c);
}
```
```plaintext
0.0
```

> Das Ergebnis ist zwar vom Typ  ``double``, aber die linke Seite der Zuweisung wird erst ausgeführt, nachdem der Ausdruck auf der rechten Seite berechnet wurde.
> Die Werte ``2`` und ``3`` sind Integer, das Ergebis des Ausdrucks ist also die Integerdivision ``2 / 3`` welche als Ergebnis ``0`` (mit 2 Rest) liefert.
> Erst jetzt passiert die Zuweisung an die Fließkommavariable ``double c = 0`` und wird dabei zu ``0.0`` konvertiert.

Diese Problem kann gelöst werden, indem einer der Operanden vorher in ein ``double`` konvertiert (gecastet) wird:
```cpp
#include <stdio.h>
int main()
{
  int a = 2;
  int b = 3;
  double c = (double)a / b;
  printf("%f\n", c);
}
```
```plaintext
0.666667
```
# Inkrement/Dekrement Operator
Nachdem das addieren/subtrahieren von eins zu/von einer Variable oft benötigt wird gibt es eigene Operatoren dafür, ``++`` und ``--``. Häufig gibt es dafür auch spezielle Befehle in der CPU.

Inkrement
````cpp
a++; // a = a + 1
````
Dekrement
````cpp
a--; // a = a - 1
````
