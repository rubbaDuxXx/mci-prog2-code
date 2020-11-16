# Vergleichsoperatoren
{: .reading}

Vergleichsoperatoren dienen zum Wertevergleich zweier Variablen oder Ausdrücke.
- ``a == b`` . . . Wahr wenn a und b **gleich** sind
- ``a != b`` . . . Wahr wenn a und b **ungleich** sind
- ``a < b `` &nbsp;. . . Wahr wenn a **kleiner** als b ist
- ``a > b `` &nbsp;. . . Wahr wenn a **größer** als b ist
- ``a <= b`` . . . Wahr wenn a **kleiner gleich** b ist
- ``a >= b`` . . . Wahr wenn a **größer gleich** b ist

Die Werte werden verglichen und je nach Resultat wird die Zahl ``0`` (für Falsch) oder `1` (für Wahr) zurück gegeben.

Beispiele
````cpp
int a = 12 > 5 // a enthält 1
````
````cpp
int b = 5 <= 4 // b enthält 0
````

## Boolsche Werte in C
In C gibt es **keinen speziellen Datentyp** um Boolsche Werte (Wahrheitswerte) zu speichern und zu verarbeiten.

Es wird einfach jedes Bitmuster das nur ``0`` enthält als **Falsch** interpretiert.

Jedes Bitmuster welches an irgendeiner Stelle eine ``1`` enthält wird als **Wahr** interpretiert.

> **Üblicherweise** wird ein ``int`` verwendet um Wahrheitswerte zu speichern / verarbeiten.

Beispiele:
````cpp
0 // Falsch
````
````cpp
0.0 // Falsch
````
````cpp
1 // Wahr
````
````cpp
-23456 // Wahr
````
````cpp
12.456 // Wahr
````

## Das Problem mit ``=`` und ``==``

In den meisten Fällen kann man ``=`` statt ``==`` schreiben und man wird **keine Fehlermeldung** bekommen, aber **die Anweisung macht nicht was man eigentlich will**.

### Vergleich ``a == 12``
- Überprueft ob ``a`` **gleich** ``12`` ist
- Falls **ja**, wird ``1`` als Ergebnis zurück geliefert
- Falls **nein**, wird ``0`` als Ergebnis zurück geliefert

### Zuweisung ``a = 12``
- Weist ``a`` den Wert ``12`` zu
- Gibt aber gleichzeitig den zugewiesenen Wert (``12``) zurück (um Zuweisungen wie ``a = b = 12`` zu ermöglichen)
- ``12`` gilt in C aber als Wahr. Der Ausdruck ``a = 12`` **ist also immer Wahr**.

# Logische Operatoren

Wie in der Aussagenlogik der Mathematik lassen sich auch in C mehrere Ausdrücke mittels logischer Operatoren zu einem Gesamt-Ausdruck kombinieren. Wir müssen einzelne Vergleichsoperatoren verknüpfen um zB zu entscheiden ob ``a > 2`` **und** ``a < 5`` ist (also ob ``a`` die Werte 2, 3, 4 oder 5 enthält).

Wir benötigen also einen Weg um Beziehungen wie **und** und **oder** abzubilden. Zusätzlich soll ein Wahrheitswert oder ein Ausdruck **negiert** werden können. Die Operatoren dafür in C sind:
- ``&&`` . . . und
- ``||`` . . . oder
- &nbsp;``! `` . . . negation

Das ``!`` als logisches **Nicht** bezieht sich auf den unmittelbar rechts stehenden Ausdruck und kehrt dabei den Wahrheitswert des Ausdrucks um. Die anderen beiden Operatoren ``&&`` und ``||`` verknüpfen den unmittelbar links und den unmittelbar rechts stehenden Ausdruck zu einer Gesamt-Aussage. Eine **Und**-Verknüpfung ist genau dann wahr, wenn beide Teil-Ausdrücke wahr sind. Eine **Oder**-Verknüpfung ist wahr, wenn mindestens einer der beiden Ausdrücke wahr ist.

## Wahrheitstabelle **Und**

| a | b | a && b |
|:---:|:---:|:------:|
| 0 | 0 | 0      |
| 0 | 1 | 0      |
| 1 | 0 | 0      |
| 1 | 1 | 1      |



## Wahrheitstabelle **Oder**

| a | b |a \|\| b|
|:-:|:-:|:----:|
| 0 | 0 |   0  |
| 0 | 1 |   1  |
| 1 | 0 |   1  |
| 1 | 1 |   1  |

## Wahrheitstabelle **Negation**

| a |!a |
|:-:|:-:|
| 0 | 1 |
| 1 | 0 |

## Beispiel 1
*Ist ``a`` kleiner als ``4`` und ``b`` entweder größer als ``8`` oder gleich ``3``?*
````cpp
a < 4 && (b > 8 || b == 3) // Korrekte Klammerung beachten
````
## Beispiel 2
*Ist ``a`` kleiner als ``4`` oder größer als ``6``?*

**Nicht gültig**: 
````cpp
a < 4 || > 6 // UNGÜLTIG
````

Der Operator ``>`` braucht zwei Operanden, aber nur einer (``6``) ist gegeben! **Korrekt**:
````cpp
a < 4 || a > 6
````

# Binäre Operatoren
Hin uns wieder ist es notwendig die Bit einer Variable direkt zu manipulieren. Binäre Operatoren erlauben dies. Allerdings sind diese nur auf Ganzzahlen (``char``, ``int``, ``long int``, ...) anwendbar.

## Bitweise Operatoren
Bitweise Operatoren führen logische Operationen (und, oder, ...) auf Bit-ebene aus. Es werden also nicht die Zahlen an sich verwendet, sondern deren **binäre Representation im Speicher**.

### **AND** - Bitweises Und
Bei der bitweisen UND-Verknüpfung ``&`` hat das Ergebnis an den Stellen eine ``1``, an denen beide Vergleichswerte eine ``1`` besitzen.

````cpp
int a=10, b=6, c;
c = a & b;
printf("c: %d\n", c);
````
````plaintext
c: 2
````
Zugehörige Rechnung der UND-Verknüpfung
~~~
a: 10 dezimal => 1010 binär
b:  6 dezimal => 0110 binär

      1010
 UND  0110
-----------
      0010 

c: 0010 binär => 2 dezimal
~~~

### **OR** - Bitweises Oder
Bei der bitweisen ODER-Verknüpfung ``|`` hat das Ergebnis an den Stellen eine ``1``, an denen mindestens einer der beiden Vergleichswerte eine ``1`` besitzt.

````cpp
int a=10, b=6, c;
c = a | b;
printf("c: %d\n", c);
````
````plaintext
c: 14
````
Zugehörige Rechnung der ODER-Verknüpfung
~~~
a: 10 dezimal => 1010 binär
b:  6 dezimal => 0110 binär

      1010
ODER  0110
-----------
      1110 

c: 1110 binär => 14 dezimal
~~~

### **XOR** - Bitweises Exklusives Oder
Bei der bitweisen XOR Verknüpfung ``^``hat das Ergebnis an den Stellen eine ``1``, an denen **entweder** der eine oder der andere Vergleichswert eine ``1`` besitzt.

````cpp
int a=10, b=6, c;
c = a ^ b;
printf("c: %d\n", c);
````
````plaintext
c: 12
````
Zugehörige Rechnung der XOR-Verknüpfung
~~~
a: 10 dezimal => 1010 binär
b:  6 dezimal => 0110 binär

      1010
 XOR  0110
-----------
      1100 

c: 1100 binär => 12 dezimal
~~~

### **NOT** - Bitweise Negation
Bei der bitweisen Negation ``~`` wird jedes Bit umgekehrt: aus ``0`` wird ``1`` und aus ``1`` wird ``0``.

## Bit-Verschiebung
Die Bits eines Wertes können nach links oder rechts verschoben werden (engl. bit shift). Die Bits am Rand fallen raus, die Stellen auf der anderen Seite werden mit Nullen aufgefüllt. Die Linksverschiebung geht mit ``<<,`` die Rechtsverschiebung mit ``>>.``

**Beispiel**: Hier wird der Wert ``5`` jeweils nach links und rechts um eine Stelle verschoben:
````cpp
int b=5, c, d;
c = b << 1;
d = b >> 1;
printf("c: %d, d: %d\n", c, d);
````
````plaintext
c: 10, d: 2
````
Erklärung der Bit-Verschiebung
~~~
b:  5 dezimal => 0101 binär

c:  0101 << 1 => 1010 binär => 10 dezimal
d:  0101 >> 1 => 0010 binär =>  2 dezimal
~~~