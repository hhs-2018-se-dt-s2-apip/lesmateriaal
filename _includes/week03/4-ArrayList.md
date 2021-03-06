<!-- 6.6 was 3.4 -->
## 6.6 ArrayList or an "object container"
Often during programming, we would like to keep many different strings in memory. A very bad idea would be to define a variable for each of them:

```java
String word1;
String word2;
String word3;
// ...
String word10;
```

This would be such a good-for-nothing solution that it does not almost need an explanation -- think of this approach for a word count of 100 or 1000!

Just like other modern programming languages, Java gives us different tools to store many objects neatly in our programs. Now, we take a closer look at `ArrayList`, which is probably the most used object container in Java.

The following lines of code make use of an ArrayList that holds specifically objects of type String. A couple of strings are stored into the list.

```java
import java.util.ArrayList;

public class ListProgram {

    public static void main(String[] args) {
        ArrayList<String> wordList = new ArrayList<String>();

        wordList.add("First");
        wordList.add("Second");
    }
}
```

In the above main program method, the first row creates a new ArrayList called `wordList`, which can be used as a container for String variables. The type of the ArrayList is `ArrayList<String>`, which means that the ArrayList is meant for storing Strings. The list is created using the command `new ArrayList<String>();`.

**Note**: to make the ArrayList work, we must first write an import statement at the beginning of the program either `import java.util.ArrayList;` or import `java.util.*;`

When the list is created, two strings are added by calling the list method `add`. The list will not run out of space, so theoretically the list can contain any amount of Strings (as long as they fit in the computer's memory).

Internally an ArrayList is -- as its name suggests -- a list. The added strings automatically go to the end of the ArrayList.

### 6.7 Methods of ArrayLists

ArrayList provides us with many useful methods:

```java
public static void main(String[] args) {
    ArrayList<String> teachers = new ArrayList<String>();

    teachers.add("Anthony");
    teachers.add("Barto");
    teachers.add("Paul");
    teachers.add("John");
    teachers.add("Martin");
    teachers.add("Matt");

    System.out.println("the number of teachers " + teachers.size() );

    System.out.println("first teacher on the list " + teachers.get(0));
    System.out.println("third teacher on the list " + teachers.get(2));

    teachers.remove("Barto");

    if (teachers.contains("Barto")) {
        System.out.println("Barto is on the teachers list");
    } else {
        System.out.println("Barto is not on the teachers list");
    }
}
```

First a list of strings is created and then 6 names added to it. `size` tells us the amount of strings in the list. **Note**: when the method is called, the call should have the following format: `teachers.size()`. First comes the name of the object, then follows a dot followed by the name of the method.

The strings will be in the list in the order in which they were added to it. By calling the method `get(i)`, we get the value from the index (location) i in the list. The indexing of items in the list starts from 0. This means that the first added string is located at index 0, the second at index 1, and so on.

We can remove strings from lists through the method `remove`. The method can be used in two ways. First, `remove("characters")` removes the string given as a parameter. Second, `remove(3)` removes the 4th String from the list.

At the end of the example, the method contains is called. This method is used for asking the list if it contains the string given as a parameter. If it does, the method returns the value `true`.

Program output:

```output
the number of teachers 6
first teacher on the list Anthony
third teacher on the list Paul
Barto is not on the teachers list
Note! The methods remove and contains assume that the objects stored in the ArrayList do have an equals method. We will get back to this later in the course.
```

#### 6.7.1 Going through an ArrayList

In the following example 4 names are added to the list. Then the whole list is printed:

```java
public static void main(String[] args) {
    ArrayList<String> teachers = new ArrayList<String>();

    teachers.add("Anthony");
    teachers.add("Paul");
    teachers.add("John");
    teachers.add("Martin");

    System.out.println( teachers.get(0) );
    System.out.println( teachers.get(1) );
    System.out.println( teachers.get(2) );
    System.out.println( teachers.get(3) );
}

```
This solution works, but is really clumsy. What if there were more items in the list? Or less? What if we would not know how many items there are?

First, we create a temporary version:

```java
public static void main(String[] args) {
    ArrayList<String> teachers = new ArrayList<String>();

    teachers.add("Anthony");
    teachers.add("Paul");
    teachers.add("John");
    teachers.add("Martin");
    teachers.add("Matt");

    int place = 0;
    System.out.println( teachers.get(place) );
    place++;
    System.out.println( teachers.get(place) );  // place = 1
    place++;
    System.out.println( teachers.get(place) );  // place = 2
    place++;
    System.out.println( teachers.get(place) );  // place = 3
}
```

Using our old friend the while command, we can increment the variable `place` by one until it gets too big:

```java
public static void main(String[] args) {
    ArrayList<String> teachers = new ArrayList<String>();

    teachers.add("Anthony");
    teachers.add("Paul");
    teachers.add("John");
    teachers.add("Martin");
    teachers.add("Matt");

    int place = 0;
    while ( place < teachers.size() )  // remember why place <= teachers.size() doesn't work?
        System.out.println( teachers.get(place) );
        place++;
    }
}
```
Now, printing works regardless of the amount of items in the list.

Using a while loop, and "self indexing" the locations in the list, is usually not the best way to go through a list. A much more recommended way is to use the for-each loop described below.

#### 6.7.2 For-each

Even though the command is usually referred to as for-each, the real name of the command is only `for`. There are two versions of for, the traditional and the "for-each". The latter is used now.

Going through items in an ArrayList with for-each is easy:

```java
public static void main(String[] args) {
    ArrayList<String> teachers = new ArrayList<String>();

    teachers.add("Anthony");
    teachers.add("Paul");
    teachers.add("John");
    teachers.add("Martin");
    teachers.add("Matt");

    for (String teacher : teachers) {
        System.out.println( teacher );
    }
}
```
As we can see, the indexes of the list can be ignored if we go through the content of the list "automatically".

In the code block of the for command (inside { }) a variable `teacher` is used. It is defined in the for row, on the left side of the colon. What happens is that every item in the list `teachers` becomes the value of the variable `teacher`, one by one. It means that when for is entered, the first `teacher` is *Anthony*, the second execution of for makes the `teacher` become *Paul* etc.

Even though the for command might seem a bit strange at first, you should definitely get used to use it!

{% include week03/exercise/015.md %}
{% include week03/exercise/016.md %}
{: .exercises }


#### 6.7.3 Ordering, reversing and shuffling a list

Items in an ArrayList are easy to order by size. Ordering by size means an alphabetic order when the list items are of type String. Ordering is done as follows:

```java
public static void main(String[] args) {
    ArrayList<String> teachers = new ArrayList<String>();

    // ...

    Collections.sort(teachers);

    for (String teacher : teachers) {
        System.out.println( teacher );
    }
}
```

Output:

```output
Anthony
Barto
John
Martin
Matt
Paul
```

We give the list as a parameter for the method `Collections.sort`. The import line `import java.util.Collections;` or `import java.util.*;` needs to be at the beginning of the program in order to get tools of Collections working in our program.

Collections also includes other useful methods:

- `shuffle` shuffles the list items, can be useful for example in games
- `reverse` reverses the order of list items

{% include week03/exercise/017.md %}
{% include week03/exercise/018.md %}
{: .exercises }


#### 6.7.4 ArrayList as a parameter for a method

ArrayList can be given to a method as a parameter:

```java
public static void print(ArrayList<String> list) {
    for (String word : list) {
        System.out.println( word );
    }
}

public static void main(String[] args) {
    ArrayList<String> list = new ArrayList<String>();
    list.add("Java");
    list.add("Python");
    list.add("Ruby");
    list.add("C++");

    print(list);
}
```

The type of the parameter is defined as an ArrayList of String variables the same way a String ArrayList is defined:

Note that the name of the parameter can be anything:

```java
public static void print(ArrayList<String> printed) {
    for (String word : printed) {
        System.out.println( word );
    }
}

public static void main(String[] args) {
    ArrayList<String> programmingLanguages = new ArrayList<String>();
    programmingLanguages.add("Java");
    programmingLanguages.add("Python");
    programmingLanguages.add("Ruby");
    programmingLanguages.add("C++");

    ArrayList<String> countries = new ArrayList<String>();
    countries.add("Finland");
    countries.add("Sweden");
    countries.add("Norway");

    print(programmingLanguages);    // method is given the list programmingLanguages
as a parameter

   print(countries);                 //  method is given the list countries as a parameter
}
```

The program now includes two lists, *programmingLanguages* and *countries*. First the printing method is given the list *programmingLanguages*. The method `print` internally refers to the list given as a parameter with the name *printed*! Next, the printing method is given the list *countries*. Now, the method uses again the name *printed* referring to the parameter list.

{% include week03/exercise/019.md %}
{% include week03/exercise/020.md %}
{: .exercises }

As we notice from the example above, an ArrayList can be printed as it is. The print formatting is not usually what is sought after, so we are forced to handle the printing ourself. For example, with the help of the `for` command.

#### 6.7.5 Numbers in an ArrayList
ArrayLists can be used to store any type of values. If the stored variables are of integer type, there are a couple of details to remember. An integer ArrayList is defined like this: `ArrayList<Integer>`, instead of writing `int` you must write `Integer`.

The method `remove` does not work like expected when the list consists of int numbers::

```java
public static void main(String[] args) {
    ArrayList<Integer> numbers = new ArrayList<Integer>();

    numbers.add(4);
    numbers.add(8);

    // tries to remove the number from the index 4, does not work as expected!
    numbers.remove(4);

    // this removes the number 4 from the list
    numbers.remove(Integer.valueOf(4));
}
```

`numbers.remove(4)` tries to remove the item in the index 4 from the list. There are only 2 items in the list, so the command generates an error. We must use a slightly more complicated command if the number 4 needs to be removed: `numbers.remove( Integer.valueOf(4) );`

ArrayLists can also be used to store `doubles` (decimal numbers) and characters (`char` variables). The lists can be defined as follows:

```java
        ArrayList<Double> doubles = new ArrayList<Double>();
        ArrayList<Character> characters = new ArrayList<Character>();
```

{% include week03/exercise/021.md %}
{% include week03/exercise/022.md %}
{: .exercises }

#### 6.7.6 ArrayList as return value of a method

ArrayList can also be returned from a method as a return value. In the next example, a method creates an ArrayList, adds three integers into the list and then returns the list. Pay attention to how the main program assigns the list returned by the method as a value into a variable that has the same type as the return value:

```java
public class Main {

    public static ArrayList<Integer> addNumbersToList(int num1, int num2, int num3){
        ArrayList<Integer> list = new ArrayList<Integer>();

        list.add(num1);
        list.add(num2);
        list.add(num3);

        return list;
    }

    public static void main(String[] args) {
        ArrayList<Integer> numbers = addNumbersToList(3, 5, 2);

        for (int number : numbers) {
            System.out.println( number );
        }
    }
}
```

{% include week03/exercise/023.md %}
{% include week03/exercise/024.md %}
{% include week03/exercise/025.md %}
{: .exercises }
