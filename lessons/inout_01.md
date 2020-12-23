# Ein-/Ausgabe
{: .reading}

# Ein- Ausgabe am Bildschirm

## Ausgabe von Werten
Wir kennen bereits den Befehl `printf` um Text auf dem Bildschirm auszugeben. Die generalisierte Form sieht so aus

````cpp
printf(Formatstring, Wert1, Wert2, ...)
````

* **Formatstring** - Ein String mit *Platzhaltern* für Werte.\
Platzhalter beginnen immer mit einem Prozentzeichen ``%``
* **Werte** - Üblicherweise Variablen dessen Werte in die *Platzhalter* eingesetzt werden sollen.\
In der gleichen Reihenfolge wie die *Platzhalter*.
* **Platzhalter**
Definieren welcher Datentyp an welcher Stelle ausgegeben
werden soll. \
Erlauben oft weitere Formatierungsoptionen (z.B. wie viele
Nachkommastellen ausgegeben werden sollen etc.)

### Platzhalter
Wir müssen bei Platzhaltern angeben welcher Datentyp ausgegeben werden soll.
> Achtung: Wenn Platzhalter und Variable nicht zusammen passen werden passiert kein Fehler, sondern es werden falsche Werte ausgegeben.

Häufigste Platzhalter
* ``%d`` - int oder kleiner
* ``%f`` - float und double
* ``%s`` - String

Weitere Platzhalter
* ``%c`` - char als Zeichen
* ``%u`` - unsigned int oder kleiner
* ``%ld``, ``%lu`` - long int, unsigned long int
* ``%lld``, ``%llu`` - long long int, long long unsigned int
* ``%p`` - Adresse/Zeiger

Hier einige Beispiele 
````cpp
#include <stdio.h>

int main() {
    int i = -34;
    unsigned int ui = 3456211340;
    double pi = 355.0 / 113.0;
    char c = 'X';
    char str[] = "Hello World!";

    printf("Korrekt: i = %d, ui = %u\n", i, ui);
    printf("Falsch: i = %u, ui = %d\n", i, ui);
    printf("Korrekt: pi approx = %f\n", pi);
    printf("Falsch: pi approx = %u\n", pi);
    printf("Adresse von pi = %p\n", &pi);
    printf("Zeichen in c = %c, Zahl in c = %d\n", c, c);
    printf("Inhalt von str = %s\n", str);
}
````
````plaintext
Korrekt: i = -34, ui = 3456211340
Falsch: i = 4294967262, ui = -838755956
Korrekt: pi approx = 3.141593
Falsch: pi approx = 2117304402
Adresse von pi = 0x7ffcecf711d0
Zeichen in c = X, Zahl in c = 88
Inhalt von str = Hello World!
````

[>Try it yourself<](https://repl.it/@m0stlyharmless/MCIProg2ExPrintf#main.c){:target="_blank"}


## Eingabe von Werten
Für das Einlesen von Werten kann der Befehl `scanf` verwendet werden. In der generalisierten Form sieht dieser so aus:

````cpp
scanf("Formatstring", &Variable)
````

* **Formatstring**
Üblicherweise ein Formatplatzhalter der angibt welcher Datentyp
eingelesen werden soll.\
Es gelten dieselben Platzhalter wie für ``printf``. (Unterschied: Um einen **double** einzulesen muss ``%lf`` angegeben werden statt ``%f``)
* **Variable**
Variable in die der eingegebene Wert gespeichert wird.\
*Muss als Adresse übergeben werden*

### Einlesen von Strings

Der Platzhalter ``%s`` zum Einlesen eines Strings liest **nur ein
Wort** ein (bis zum nächsten Leerzeichen). Für das Einlesen von ganzen Sätzen kann stattdessen die die Funktion ``gets`` verwendet werden.

``scanf`` ist nützlich um zum Testen ein paar Werte einzugeben,
ist aber nicht wirklich dafür gedacht komplexere
Eingabesysteme zu erzeugen. Für komplexere Eingabesysteme
auf der Konsole verwendet man z.B. die Bibliothek [PDCurses](https://pdcurses.org/).

Beispiel für die Verwendung von ``scanf``
````cpp
#include <stdio.h>

int main() {
    int number = 0;

    printf("Bitte geben Sie eine Nummer ein: ");
    scanf("%d", &number);

    printf("Ihre Nummer mal 2 = %d\n", number * 2);
}
````
> Zu beachten ist die Verwendung der Adresse der Variable in die der Wert eingelesen werden soll.

[>Try it yourself<](https://repl.it/@m0stlyharmless/MCIProg2ExScanf#main.c){:target="_blank"}