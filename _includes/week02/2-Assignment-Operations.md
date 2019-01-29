<!-- 2 was 2.2 -->
### 2.2.3 Assignment operations

Because changing the value of a variable is a very common operation, Java has special assignment operations for it.

```java
int length = 100;

length += 10;  // same as length = length + 10;
length -= 50;  // same as length = length - 50;
```

When performing the assignment operation on an existing variable, it is written as `variable operation= change`, for example `variable += 5`. Note that a variable must be defined before you can assign a value to it. Defining a variable is done by specifying the variable type and the name of the variable.

The following example will not work because the type of the variable `length` has not been defined.

```java
length = length + 100;  // error!
length += 100;          // error!
```

When the type is defined, the operations will also work.

```java
int length = 0;
length = length + 100;
length += 100;

// the variable length now holds the value 200
```

There are also other assignment operations:

```java
int length = 100;

length *= 10;   // same as length = length * 10;
length /= 100;  // same as length = length / 100;
length %= 3;    // same as length = length % 3;

// the variable length now holds the value 1
```

 This abbreviated notation is often used in loops (see 4.1.5 in week 2).