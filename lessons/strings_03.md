# String Funktionen
{: .reading}

Dieser Abschnitt stellt einige nützliche Funktionen zum Arbeiten mit Strings vor.
> Hinweis: Für alle String-Funktionen muss die String-Bibliothek mit ``#include<string.h>`` eingebunden werden.

## Länge eines Strings

Die Funktion `strlen` liefert die Länge eines Strings zurück, d.h. die Anzahl der Symbole bis zum `'\0'`.
````cpp
strlen(string)
````

> Achtung: ``strlen`` entspricht **nicht** der Größe des Arrays in dem der String gespeichert ist.

Beispiele:
````cpp
#include <stdio.h>
#include <string.h>

int main(void) {
  char str[] = "Hello World";

  printf("array length  = %ld\n", sizeof(str)/sizeof(*str));
  printf("string length = %ld\n", strlen(str));
}
````
````plaintext
array length  = 12
string length = 11
````

````cpp
#include <stdio.h>
#include <string.h>

int main(void) {
  char str[100] = "Hello World";

  printf("array length  = %ld\n", sizeof(str)/sizeof(*str));
  printf("string length = %ld\n", strlen(str));
}
````
````plaintext
array length  = 100
string length = 11
````

## Vergleichen von Strings

Die Funktion `strcmp` vergleicht zwei Strings

````cpp
strcmp(string1, string2);
````

 und liefert als Ergebnis:
- ` 0` wenn die Strings **gleich** sind
- `<0` wenn ``string1`` alphabetisch **vor** `string2` kommt
- `>0` wenn ``string1`` alphabetisch **nach** `string2` kommt

Beispiel:
````cpp
#include <stdio.h>
#include <string.h>

int main(void) {
  char str1[] = "A Beautiful Mind";
  char str2[] = "Batman";
  char str3[] = "Clockwork Orange";
  char str4[] = "Batman";

  printf("strcmp(str2, str4) -> %d\n", strcmp(str2, str4));
  printf("strcmp(str1, str2) -> %d\n", strcmp(str1, str2));
  printf("strcmp(str2, str1) -> %d\n", strcmp(str2, str1));
  printf("strcmp(str1, str3) -> %d\n", strcmp(str1, str3));
}
````
````plaintext
strcmp(str2, str4) -> 0
strcmp(str1, str2) -> -1
strcmp(str2, str1) -> 1
strcmp(str1, str3) -> -2
````

## Kopieren von Strings

Die Funktion `strcpy` kopiert den Quellstring in den Zielstring:

````cpp
strcpy(ziel, quelle)
````
> **Achtung:** Wir müssen uns selbst darum kümmern, dass im Ziel
genug Platz ist!

## Aneinanderhängen von Strings

Die Funktion `strcat` hängt den Quellstring an den Zielstring an:

````cpp
strcat(ziel, quelle)
````
> **Achtung:** Ziel und Quelle darf nicht derselbe String sein. Wir müssen uns selbst darum kümmern, dass im Ziel genug Platz ist!

Beispiel:
````cpp
#include <stdio.h>
#include <string.h>

int main(void) {
  char str1[] = "Hello ";
  char str2[] = "World!"; 

  // empty string
  char result[20] = "";

  printf("%s\n", result);
  strcat(result, str1);
  printf("%s\n", result);
  strcat(result, str2);
  printf("%s\n", result);
}
````

````plaintext

Hello 
Hello World!
````
