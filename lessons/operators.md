# Operatoren in C
{: .reading}

Operators in the C programming language ...
> are great, they allow you to perform functions on values of a certain type. If you know C programming, you will find this a very natural way of writing code . However, not everyone understands how C operators work , especially when it comes to function calls . We have the operator? to show that it is possible to create a function in C without any special understanding of C programming . You can think about it as the ability to write code that works on objects without using any complicated data structures ( e. g. arrays or trees ). [GPT-2]

# Was ist ein Operator
{: reading}

Ein Operator ist letztlich eine *Funktion unter anderem Namen* und *anderer Notation* welche ein Programm leserlicher macht. Die Werte die an einen Operator übergeben werden (die Parameter einer Funktion) werden *Operanden* genannt.

## Beispiel
- `assign(a, add(b, c))` wird zu `a = b + c`
- Die Funktion `assign` wird zum Operator `=`
- Die Funktion `add` wird zum Operator `+`

In C sind alle Operatoren **in der Sprache eingebaut** und können nicht vom Benutzer neu oder umdefiniert werden.

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
```
0.0
```
