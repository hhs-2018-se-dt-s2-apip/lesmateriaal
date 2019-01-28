<!-- 4.2 was 2.2 -->
## 4.2 Assignment operations in loops

Often during a loop, the value of a variable is calculated based on repetition. The following program calculates 3*4 somewhat clumsily as the sum 3+3+3+3:

```java
int result = 0;

int i = 0;
while (i < 4) {
   result = result + 3;
   i++;  // means the same as i = i + 1;
}
```

In the beginning `result = 0`. During the loop, the value of the variable is incremented by 3 on each iteration. Because there are 4 iterations, the value of the variable is 3*4 in the end.

Using the assignment operator introduced above, we can achieve the same behavior as follows:

```java
int result = 0;

int i = 0;
while (i < 4) {
   result += 3;  // this is the same as result = result + 3;
   i++;          // means the same as i = i+1;
}
```

{% include week02/exercise/010.md %}
{% include week02/exercise/011.md %}
{% include week02/exercise/012.md %}
{% include week02/exercise/013.md %}
{: .exercises }
