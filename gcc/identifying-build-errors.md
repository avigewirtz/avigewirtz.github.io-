# Exercises: Identifying Build Errors

In this section we'll go over some exercises to determine, Assume C99, where function declarations are required.&#x20;

* If error would be caused at multiple stages, mention first
* Assume C99, where calls to undeclared functions is not allowed

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

* A) Preprocessing - answer is A
* B) Compilation
* C) Assembly
* D) Linking
* E) Neither

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
* C) Assembly
* D) Linking - Correct answer is D
* E) Neither

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
* C) Assembly
* D) Linking - Correct answer is D
* E) Neither

4. gcc217 testadd.c - preprocessing error. gcc217 testadd.c add.c. still preprocessing error.&#x20;

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

* A) Preprocessing - A
* B) Compilation
* C) Assembly
* D) Linking&#x20;
* E) Neither&#x20;

5. `gcc217 testadd.c none. gcc217 testadd.c add.c. linking error. duplicate.`&#x20;

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

* A) Preprocessing&#x20;
* B) Compilation
* C) Assembly
* D) Linking&#x20;
* E) Neither - E





* preprocessor maro (like PI) used in testcircle.c, where it isn't defined



Preprocessor errors



* incorrect prototype
