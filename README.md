# Null Values

## Learning Goals

- Define a `null` value
- Explain the `NullPointerException`

## What is a Null Value?

The **null value** is used to represent the absence of a value. The `null`
keyword is a reserved word in Java and is neither a type nor an object. It was
created as a way to point a reference variable to nothing.

Let's look at the different types of variables again: primitive types and
reference types.

As we recall, primitive types are predefined types in Java. These data types
also have an underlying default value. For example, an uninitialized `int` will
default to 0 and an uninitialized `boolean` will default to false:

```java
int firstNumber = 8;
int secondNumber;
double thirdNumber = 4.5;
double fourthNumber;

System.out.println(firstNumber);
System.out.println(secondNumber);
System.out.println(thirdNumber);
System.out.println(fourthNumber);
```

The above will have an output like this:

```text
8
0
4.5
0.0
```

So if primitive data types have a default value, what about reference types?
Do they have a default value? The answer is they do - and it's `null`. The
`null` value is the default value for all reference types (objects and `String`
data types). This means, in memory, if we do not initialize the reference type
when we first declare it, the variable in the stack will point to `null` in the
heap. Let's see what happens when we don't initialize a reference
variable!

## Instance and Static Variable Initialization

```java
public class Person {

    private String name;

    public static void main(String[] args) {
        Person p1 = new Person();
        System.out.println(p1.name);
    }
}
```

Consider the instance variable `name`.  Since `name` is not assigned
an explicit value, it is assigned the default value `null`.

![null value](https://curriculum-content.s3.amazonaws.com/6676/java-multipleclasses/null.png
)

The output of the above will look like this:

```text
null
```

## Initialization of local variables

Instance variables are initialized
to a default value; however, local variables are not.
If we update the `main` method to declare a local
variable `favoriteColor`, the method won't compile
because the variable has not been assigned a value.

```java
public class Person {

    private String name;  //initialized to null

    public static void main(String[] args) {
        Person p1 = new Person();
        System.out.println(p1.name);

        String favoriteColor ;    //uninitialized
        System.out.println(favoriteColor);  //compiler error at this line
    }
}
```

To compile, we must assign the local variable a value.
If we want, we can  assign `null` like so:

```java
public class Person {

    private String name;  //initialized to null

    public static void main(String[] args) {
        Person p1 = new Person();
        System.out.println(p1.name);

        String favoriteColor = null ;    //initialized to null
        System.out.println(favoriteColor);  //no error 
    }
}
```

The output of the above will look like this:

```text
null
null
```

Notice that the `null` is in all lowercase letters. The casing of the word
matters. If the code were to be written `String favoriteColor = NULL` it would not
compile.

The `null` value is only to be used with reference types and not primitives. If
we were to assign a primitive type to `null`, we would get an error about the
type being incompatible. However, we will see in a subsequent lesson
on type casting that we
can use the `null` value with the wrapper classes.

```java
int x = null;    // Will result in an error at compilation

Integer y = null;    // this is okay since Integer is a reference type
```

## NullPointerException

The `NullPointerException` is a runtime exception that we may see occur in our
programs from time to time. This is a more common exception to be on the lookout
for! `NullPointerException` is thrown when we try to use an object that has a
value of `null`. Consider the following:

```java
public class Cat {

    public void purr() {
        System.out.println("Purr");
    }

    public static void main(String args[]) {
        Cat tom = new Cat();
        Cat garfield = null;

        garfield.purr();    // Would throw a NullPointerException
    }
}
```

Another example of this is attempting to call a `String` method:

```java
public class Person {

    private String name;  //initialized to null

    public static void main(String[] args) {
        Person p1 = new Person();
        System.out.println(p1.name);

        String favoriteColor = null ;    //initialized to null
        System.out.println(favoriteColor);  //no error 
        System.out.println(favoriteColor.toLowerCase()); //throws NullPointerException
    }
}
```