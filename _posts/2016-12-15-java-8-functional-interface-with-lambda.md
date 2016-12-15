---
layout: post
title: Java 8 - Functional interface with lambda
---

Java 8 introduces lots of new elements in the java syntax like lambda and functional interfaces.

These changes, even though just syntactic sugar over the previous syntax, change drastically the way a Java code looks. Someone, who is used to traditional Java and is well versed with it, would easily be baffled looking at those arrows `->` and double quotes `::`.

I would like to explore one of the new elements here. That is the `functional interface`.

Functional interface, also known as, Single Abstract Method (SAM) interface is a well known and already existing construct in Java.
It looks something like this

``` java
public interface Runnable {
    void run();
}
```

So, by definition, SAM or functional interface is an interface in java having only a single method defined in it.
It might extend other interfaces as long as the following conditions are met.

1. There is only one abstract method defined. This is considering both the current interface and its parent. There can be any number of default methods.
2. `java.lang.Object` methods can be present, like `toString` and `equals`. They are redundant.

Runnable interface is a well known example and belongs to java.lang package.

Till java 7, to execute something in a new thread, something like this would be used.

``` java
Thread t = new Thread(
    new Runnable() {
        @Override
        public void run() {
            System.out.println("Hello, parallel World!");
        }
    }
);
t.start();
```

It uses an anonymous class which implements the Runnable interface. But, as we can see, the real executable statement here is in the line 5. The other lines do not more than cluttering the code. This obviously makes the syntax heavy.

As an improvement, in Java 8, one can use the following lambda syntax to initialise a functional interface.

``` java
Thread t = new Thread(() -> System.out.println("Hello, world!"));
t.run();

```

Here the lambda expression `() -> System.out.println()` is actually the implementation of the abstract `run` method of Runnable interface.

As we can see, the syntax is way more lighter.
And the real executable line is clearly visible without the clutter.

In a way, it can be said that java 8 has given new life to functional interfaces.


**Pro Tip** :
Use annotation `@FunctionalInterface` while defining a functional interface to get compile time errors and warning.

**Example**

One more code sample for methods with arguments.

A sample functional interface

``` java
@FunctionalInterface
public interface Printable {
    void print(String a, String b);
}
```

A function expection a Printable object and the calling main method.

``` java

public class DemoFunctionalInterface {
    public static void callPrintable(Printable p) {
        p.print("Apple", "Ball");
    }
    public static void main(String[] args) {
        callPrintable((a, b) -> System.out.println("Printing " + a + " " + b));
    }
}

```

This main method would print `Printing Apple Ball`.

---
Reference

1. [State of the lambda](http://cr.openjdk.java.net/~briangoetz/lambda/lambda-state-4.html)
2. [java.lang.Runnable](https://docs.oracle.com/javase/7/docs/api/java/lang/Runnable.html)
3. [Translation of lambda expressions](http://cr.openjdk.java.net/~briangoetz/lambda/lambda-translation.html)
4. [Functional interface : Recreation in Java 8](https://dzone.com/articles/introduction-functional-1)
5. [Defender or default methods](http://cr.openjdk.java.net/~briangoetz/lambda/Defender%20Methods%20v4.pdf)
6. [java.lang.FunctionalInterface](http://docs.oracle.com/javase/8/docs/api/index.html?java/lang/FunctionalInterface.html)
