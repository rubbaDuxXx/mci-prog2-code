# Ein-Ausgabe in Dateien
{: .reading}

## Arbeiten mit Dateien

Die generelle Vorgehensweise beim Arbeiten mit Dateien ist:
1) Die Datei wird mittels ``fopen`` **geöffnet** und kann dann mit
einem von der Funktion zurückgegebenem FILE-Zeiger
angesprochen werden.
2) Daten werden aus der Datei **gelesen/geschrieben**
3) Die Datei wird mit ``fclose`` wieder **geschlossen**

> **Lesen und Schreiben**\
> Von den meisten Funktionen zur Ein- und Ausgabe (``printf``,
``scanf``, ``gets``, ... ) gibt es spezielle Versionen welche die gleichen Operationen auf Dateien ausführen (``fprintf``, ``fscanf``, ``fgets``, ... )

### Dateien öffnen

Dateien müssen zuerst geöffnet werden, bevor man damit arbeiten kann. Dafür gibt es die Funktion `fopen`. Diese sieht in ihrer generalisierten Version wie folgt aus:

````cpp
FILE* bla = fopen(Dateiname, Modus)
````
**Dateiname**\
Der Name oder Pfad der Datei

**Modus**
* ``"r"`` - Öffnet eine Datei zum **Lesen**.
* ``"w"`` - Öffnet eine Datei zum **Schreiben**. Falls die Datei schon
existiert wird diese zuerst **gelöscht**.
* ``"a"`` - Öffnet eine Datei zum **Schreiben**. Falls die Datei schon
existiert werden Daten an die bestehende Datei **angehängt**.

**Fehler**
Im Fehlerfall, also wenn das Öffnen der Datei nicht funktioniert hat, wird bei ``fopen`` der Wert ``NULL`` zurückgegeben.

### Dateien schließen

Die Aufgabe des Programmieres ist es, Dateien die geöffnet wurde auch wieder zu schließen. Der Grund dafür ist, dass durch das Öffnen  begrenzte Ressourcen vom Betriebssystem angefordert werden. Wenn diese Ressourcen nicht mehr freigegeben werden (durch das Schließen) entsteht ein sogenanntes Ressourcenleck [Resource Leak (engl.)]([https://link](https://en.wikipedia.org/wiki/Resource_leak)).


> Nachdem wir die Datei nicht mehr benötigen sollte sie mit ``fclose(FILE
Zeiger)`` wieder geschlossen werden.
Es kann sein, dass Daten die in eine Datei geschrieben worden sind erst
mit ``fclose`` wirklich auf der Festplatte/SSD landen

Schreibend öffnen
````cpp
#include <stdio.h>

int main() {
    FILE* file = fopen("newfile.txt", "w");
    if (file != NULL) {
        // Daten Schreiben z.B. mit fprintf
    }
    fclose(file);
}
````

Lesend öffnen
````cpp
#include <stdio.h>

int main() {
    FILE* file = fopen("newfile.txt", "r");
    if (file != NULL) {
        // Daten Lesen z.B. mit fgets
    }
    fclose(file);
}
````
[>Try it yourself<](https://repl.it/@m0stlyharmless/MCIProg2ExFopen#main.c){:target="_blank"}

## Schreiben und Lesen

### fprintf

````cpp
fprintf(FILE*, Formatstring, Wert1, Wert2, ...)
````

Funktioniert wie ``printf`` mit dem Unterschied, dass als erster
Parameter ein FILE-Zeiger übergeben wird

**Beispiel**:
Wir schreiben das Ergebnis von 1/i für i 2 [1,9] in eine Datei:

````cpp
#include <stdio.h>

int main() {
    FILE *file = fopen("./newfile.txt", "w");
    if (file != NULL) {
        for (int i = 1; i < 10; i++) {
            fprintf(file, "%f\n", 1.0 / i);
        }
    } else {
        printf("Fehler beim Öffnen der Datei!\n");
    }
    fclose(file);
}
````


### fscanf
````cpp
fscanf(FILE*, "Formatstring", &Variable)
````

Funktioniert wie ``scanf`` mit dem Unterschied, dass als erster
Parameter ein FILE-Zeiger übergeben wird

**Beispiel**
````cpp
#include <stdio.h>

int main() {
    double values[1024];
    int nbvalues = 0;
    FILE* file = fopen("./newfile.txt", "r");
    if (file != NULL) {
        while (feof(file) == 0) {
            fscanf(file, "%lf\n", &values[nbvalues]);
            nbvalues = nbvalues + 1;
        }
        printf("%d Werte eingelesen\n\n", nbvalues);
    } else {
        printf("Fehler beim öffnen der Datei!\n");
    }
    fclose(file);
    for (int i = 0; i < nbvalues; i++) {
        printf("%lf\n", values[i]);
    }
}
````

### feof
````cpp
feof(FILE*)
````

Für den Fall, dass die Datei zum Lesen geöffnet wurde.
Gibt einen Wert ungleich 0 zurück wenn wir das Ende der
Datei erreicht haben.



## Beispiel Lesen aus einer csv Datei

````cpp
#include <stdio.h>

int main() {
    FILE *file = fopen("test.csv", "r");
    if (file != NULL) {
        while (feof(file) == 0) {
        int i;
        double a;
        double b;
        fscanf(file, "%d;%lf;%lf\n", &i, &a, &b);
        printf("%d: %f, %f\n", i, a, b);
        }
    } else {
        printf("Fehler beim öffnen der Datei!\n");
    }
    fclose(file);
}
```

Inhalt der Datei
````csv
1;0.234;0.123
2;23.456;-23453.45
3;3231.345;1.234
````