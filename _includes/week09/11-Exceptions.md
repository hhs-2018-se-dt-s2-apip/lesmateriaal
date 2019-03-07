## 7. Input/output and exception handling
### 7.1 Exceptions

Exceptions are such situations where the program executions is different from our expectations. For instance, the program may have called a method of a *null*  reference, in which case the user is thrown a `NullPointerException`. If we try to retrieve a index outside a table, the user is *thrown* a `IndexOutOfBoundsException`. All of them are a type of `Exception`.

Exceptions are often caused by unexpected situations that occur when handling input and output of a program. For example: users can easily frustrate a program by entering input in an unexpected format.

We deal with exceptions by using the block `try { } catch (Exception e) { }`. The code contained within the brackets which follows the keyword `try` will not crash when an exception occurs in this part of the code. The code within the brackets which follow the keyword `catch` defines what should happen when the try-code throws an exception. We also define the type of the exception we want to catch (`catch (Exception e)`).

```java
try {
    // code which can throw an exception
} catch (Exception e) {
    // code which is executed in case of exception
}
```

The [parseInt](http://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html#parseInt(java.lang.String)) method of class `Integer` which turns a string into a number can throw a `NumberFormatException` if its string parameter cannot be turned into a number. Now we implement a program that turns a user input String to a number.

```java
Scanner reader = new Scanner(System.in);
System.out.print("Write a number: ");

int num = Integer.parseInt(reader.nextLine());
```

```output
Write a number: ~~tatti~~
~~Exception in thread "..." java.lang.NumberFormatException: For input string: "tatti"~~
```

The program above throws an exception because the user digits an erroneous number. The program execution ends up with a malfunction, and it cannot continue. We add an exception management statement to our program. The call, which may throw an exception is written into the `try` block, and the action which takes place in case of exception is written into the `catch` block.

```java
Scanner reader = new Scanner(System.in);

System.out.print("Write a number: ");

try {
    int num = Integer.parseInt(reader.nextLine());
} catch (Exception e) {
    System.out.println("You haven't written a proper number.");
}
```

```output
Write number: ~~5~~
```

```output
Write number: ~~oh no!~~
You haven't written a proper number.
```

In case of exception, we move from the chunk of code defined by the `try` keyword to the `catch` chunk. Let's see this by adding a print statement after the `Integer.parseInt` line in the `try` chunk.

```java
Scanner reader = new Scanner(System.in);

System.out.print("Write a number: ");

try {
    int num = Integer.parseInt(reader.nextLine());
    System.out.println("Looks good!");
} catch (Exception e) {
    System.out.println("You haven't written a proper number.");
}
```

```output
Write a number: ~~5~~
Looks good!
```

```output
Write a number: ~~I won't!~~
you haven't written a proper number.
```

String *I won't!* is given as parameter to the method `Integer.parseInt`, which throws an exception if the `String` parameter can't be changed into a number. Note that the code in the `catch` chunk is executed only in case of exception -- otherwise the program do not arrive till there.

Let's make something more useful out of our number translator: let's do a method which keeps on asking to type a number till the user does it. The user can *return only* if they have typed the right number.

```java
public int readNumber(Scanner reader) {
    boolean running = true;
    while (running) {
        System.out.print("Write a number: ");

        try {
            int num = Integer.parseInt(reader.nextLine());
            return num;
        } catch (Exception e) {
            System.out.println("You haven't written a proper number.");
        }
    }
}
```

The method `readNumber` could work in the following way:

```output
Write a number: ~~I won't!~~
You haven't written a proper number.
Write a number: ~~Matti has a mushroom on his door.~~
You haven't written a proper number.
Write a number: ~~43~~
```

#### 7.1.1 Throwing Exceptions

Methods and constructors can *throw* exceptions. So far, there are two kinds of exceptions which can be thrown. There are the ones which have to be handled, and the ones which don't have to be dealt with. When we have to handle the exceptions, we do it either in a `try-catch` chunk, or *throwing them from* a `method`.

In the clock exercise of Introduction to Programming (not in the HHS-course), we explained that we can stop our program of one second, by calling the method `Thread.sleep(1000)`. The method may throw an exception, which we must deal with. In fact, we handle the exception using the `try-catch` sentence; in the following example we skip the exception, and we leave empty the `catch` chunk.

```java
try {
    // we sleep for 1000 milliseconds
    Thread.sleep(1000);
} catch (Exception e) {
    // In case of exception, we do not do anything.
}
```

It is also possible to avoid handling the exceptions in a method, and *delegate the responsibility* to the method caller. We delegate the responsibility of a method by using the statement `throws Exception`.

```java
public void sleep(int sec) throws Exception {
    Thread.sleep(sec * 1000);   // now we don't need the try-catch block
}
```

The `sleep` method is called in another method. Now, this other method can either handle the exception in a `try-catch` block or delegate the responsibility forward. Sometimes, we delegate the responsibility of handling an exception till the very end, and even the `main` method delegates it:

```java
public class Main {
   public static void main(String[] args) throws Exception {
       // ...
   }
}
```

In such cases, the exception ends up in Java's virtual machine, which interrupts the program in case there is an error which causes the problem.

There are some exceptions which the programmer does not always have to address, such as the `NumberFormatException` which is thrown by `Integer.parseInt`. Also the `RuntimeExceptions` do not always require to be addressed. These are two examples of exceptions that don’t have to be dealt with. The compiler cannot 'predict' that an exception will occur, so it does not force you to catch the exception.

We can throw an exception by using the `throw` statement. For instance, if we want to throw an exception which was created in the class `NumberFormatException`, we could use the statement `throw new NumberFormatException()`.

Another exception which hasn't got to be addressed is `IllegalArgumentException`. With `IllegalArgumentException` we know that a method or a constructor has received an *illegal* value as parameter. For instance, we use the `IllegalArgumentException` when we want to make sure that a parameter has received particular values.

In the example below we have the constructor public Grade(int grade). A constructor is a special method that will be explained later on when we introduce classes. For now you can consider it as a 'regular' method that expects parameters like any other method.

```java
public class Grade {
    private int grade;

    public Grade(int grade) {
        this.grade = grade;
    }

    public int getGrade() {
        return this.grade;
    }
}
```

Next, we want to validate the value of the constructor parameter of our `Grade` class. The grades in Finland are from 0 to 5. If the grade is something else, we want to *throw an exception*. We can add an if statement to our Grade class constructor, which checks whether the grade is outside range 0-5. If so, we throw an `IllegalArgumentException` telling `throw new IllegalArgumentException("The grade has to be between 0-5");`.

```java
public class Grade {
    private int grade;

    public Grade(int grade) {
        if (grade < 0 || grade > 5) {
            throw new IllegalArgumentException("The grade has to be between 0-5");
        }
        this.grade = grade;
    }

    public int getGrade() {
        return this.grade;
    }
}
```

```java
Grade grade = new Grade(3);
System.out.println(grade.getGrade());

Grade wrongGrade = new Grade(22);
// it causes an exception, we don't continue
```

```output
3
Exception in thread "..." java.lang.IllegalArgumentException: The grade has to be between 0-5
```

#### 7.1.2 The Exception Information

The `catch` block tells how we handle an exception, and it tells us what exception we should be prepared for: `catch (Exception e)`. The exception information is saved into the `e` variable.

```java
try {
    // the code, which may throw an exception
} catch (Exception e) {
    // the exception information is saved into the variable e
}
```

The class `Exception` can provide useful methods. For instance, the method `printStackTrace()` prints a path which tells us where the exception came from. Let's check the following error printed by the method `printStackTrace()`.

```output
Exception in thread "main" java.lang.NullPointerException
  at package.Class.print(Class.java:43)
  at package.Class.main(Class.java:29)
```

Reading the stack trace happens button up. The lowest is the first call, i.e. the program execution has started from the `main()` method of class `Class`. At line 29 of the main method of `Class`, we called the method `print()`. Line 43 of the method `print` caused a `NullPointerException`. Exception information are extremely important to find out the origin of a problem.

{% include week09/exercise/001.md %}
{: .exercises }

