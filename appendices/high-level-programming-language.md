# High Level Programming Language









{% code lineNumbers="true" %}
```c
#include <stdio.h>

int main() {
    int num1, num2, product;

    printf("Enter the first integer: ");
    scanf("%d", &num1);

    printf("Enter the second integer: ");
    scanf("%d", &num2);

    product = num1 * num2;

    printf("The product of the two integers is: %d\n", product);

    return 0;
}

```
{% endcode %}

We don't have to be familiar with architecture at all, such as registers or memory&#x20;

we have a much more rich set of instructions can perform complex tasks. For example

```
 product = num1 * num2     LOOP:
                                brz r10, END  
                                add r12, r12, r11
                                sub r10, r10, r1 
                                jmpr LOOP   
```
