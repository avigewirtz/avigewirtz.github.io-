# Identifying Build Errors

In this section, we'll go over some exercises to sharpen your ability to spot the cause of build errors. For each code snippet, identify the stage where the build would fail: preprocessing, compilation, linking, or neither (i.e., builds successfully). We are not including assembly stage errors, as such errors are only relevant if you're coding directly in assembly. Also note that these questions focus solely on build errors, not runtime errors or bugs. Thus, if a code snippet will build successfully but contains a runtime issue, the answer would be "neither".

#### Exercises

{% hint style="info" %}
For the following exercises, assume C99 Standard, where calls to undeclared functions are not allowed.&#x20;
{% endhint %}

1.

```c
#include <stdio.h>

int main() {

    int arg1 = 10;
    double arg2 = 20.5;
    
    double result = nonExistentFunction(arg1, arg2);

    printf("Result: %f\n", result);

    return 0;
}
```

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

2.

```c
#include <stdio.h>

double nonExistentFunction(int arg1, double rg2);

int main() {

    int arg1 = 10;
    double arg2 = 20.5;
    
    double result = nonExistentFunction(arg1, arg2);

    printf("Result: %f\n", result);

    return 0;
}
```

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

3.

```c
#include <stdio.h>

int hello() {
    printf("Hello, World!\n");
    return 0;
}
```

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

4. gcc217 testadd.c - preprocessing error. gcc217 testadd.c add.c. still preprocessing error.

{% tabs %}
{% tab title="testadd.c" %}
```c
#include <stdio.h>

int main() {
    printf("%d\n", add(2, 3));
    return 0;
}

```
{% endtab %}

{% tab title="add.c" %}
```c
int add(int a, int b){
    return a + b;
}
```
{% endtab %}
{% endtabs %}

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

5. `gcc217 testadd.c`

{% tabs %}
{% tab title="testadd.c" %}
```c
#include <stdio.h>
#include "add.c"

int main() {
    printf("%d\n", add(2, 3));
    return 0;
}
```
{% endtab %}

{% tab title="add.c" %}
```c
int add(int a, int b){
    return a + b;
}
```
{% endtab %}
{% endtabs %}

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

`gcc217 testadd.c add.c.`

* A) Preprocessing
* B) Compilation
* C) Linking&#x20;
* D) Neither

6. `gcc217 circumfrence.c diameter.c`

{% tabs %}
{% tab title="circumfrence.c" %}
```c
#include <stdio.h>
double calculateDiameter(double radius);

int main() {

    double radius = 5.2;
    double diameter = calculateDiameter(radius);
    double circumfrence = PI * diameter;
    
    printf("%f\n",circumfrence);
    return 0;
}
```
{% endtab %}

{% tab title="diameter.c" %}
```c
#define PI 3.14159

double calculateDiameter(double radius) {
    return 2 * radius;
}
```
{% endtab %}
{% endtabs %}

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

7.

```c
#include <stdio.h>
int processNumber(int num);

int main() {
    double result = processNumber(3.14);

    printf("Result: %f\n", result);

    return 0;
}

int processNumber(int num) {
    return num;
}
```

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

8.

```c
#include <stdio.h>
int processNumber(double num);

int main() {
    int result = processNumber(3);

    printf("Result: %f\n", result);

    return 0;
}

int processNumber(int num) {
    return num;
}
```

* A) Preprocessing
* B) Compilation
* C) Linking
* D) Neither

<details>

<summary>Answers</summary>

1. A
2. C
3. C
4. A
5. C. 5.2 = D
6. B
7. D
8. B

</details>
