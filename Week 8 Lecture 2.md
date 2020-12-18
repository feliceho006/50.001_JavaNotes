# Week 8 Lecture 2

*// felia's edits*

The id attribute allows you to access the widget throughout the whole java project package.

To reference that widget in a java class:
```java=
Textview myTextView = findviewbyid(R.id.myTextView);
```

### Random Class

In Java, random number generator need to be initialised with a seed. 
- For sequence of same number, same seed
- Otherwise, use date object to keep changing seed

```java
Random r = new Random();
r.nextInt(); // Gives you the next integer from 0 to 2^32 (exclusive)
r.nextInt(n); // Gives you the next integer from 0 to n (exclusive)
r.nextDouble(); // Gives you the next double from 0 to 1.0

Date d = new Date();
Random r = new Random(d.getTime());
```

### Nested classes
A nested class is essentially a class within a class.

```java=
public class OuterClass{
    //your code
    
    class InnerClass{
        //your code
    }
}
```

##### Inner class
A nested class that is not **static** is called an inner class.

The inner class can only be instantiated in the context of the outer(enclosing) class, otherwise the inner class 

- Inner classes have access to all methods and variables of the outer class.

Like this:
```java=
public class OuterClass{
    int a;
    
    OuterClass(){
        a = 10;
    }
    
    void outerPrintA(){
        System.out.println(a);
    }
    
    class InnerClass{
        int c;
        
        InnerClass(){
            c = 100;
        }
        
        void innerPrintA(){
            System.out.println(a);
        }
        
        OuterClass giveBackOuter(){
            return OuterClass.this;
        }
    }
}

// instantiate OuterClass
OuterClass outer = new OuterClass();
// instantiate InnerClass
OuterClass.InnerClass inner = outer.new InnerClass();
```

What if the inner class is private?
```java=
public class OuterClass{
    int a;
    
    OuterClass(){
        a = 10;
    }
    
    void outerPrintA(){
        System.out.println(a);
    }
    // now the inner class is private, and not accessible by the outer class
    private class InnerClass{
        int c;
        
        InnerClass(){
            c = 100;
        }
        
        void innerPrintA(){
            System.out.println(a);
        }
        
        OuterClass giveBackOuter(){
            return OuterClass.this;
        }
    }
}


// instantiate OuterClass
|| OuterClass outer = new OuterClass(); ||
// instantiate InnerClass
|| OuterClass.InnerClass inner = outer.new InnerClass(); ||

> Error

// It will no longer work because the outer class is unable to "see" the inner class
```

##### Static Nested class

When the nested class is declared static:
- can only access static variables and static methods
- can be instantiatedd w/o instance of outer class

```java=
public class OuterClass{
    //code

    static class InnerClass{
        //code
    }
}

OuterClass.InnerClass inner = new OuterClass.InnerClass();
```

##### Nested interface and Anonymous Class
Since interfaces are inherently **static**, in this code any object that implements that inerface can be passed to the class method.

```java=
public class Foo{
    //this is the nested interface
    interface Bar{
        void drink();
    }
    
    Foo(){
    }
    
    void thirsty(Bar bar){
        bar.drink();
    }
}

public class TestFoo{
    
    public static void main(String[] argv){
        Foo f = new Foo();
        // Bar bar is now C()
        f.thirsty(new C());
    }
    
    //object that is implementing Bar
    static class C implements Foo.Bar{
        @Override
        public void drink(){
            System.out.println("gulp");
        }
    }
}
```

If this inner class is used *only once*, we use an alternative: **Anonymous Inner Class** to avoid declaring too many inner classes.
- do not need to name the class thats implementing the interface
- do not need to assign variable name to the class that implements the interface
```java=
public class TestFoo_1{
    
    public static void main(String[] argv){
        Foo f = new Foo();
        // this is done for setOnClickListener in buttons as well
        f.thirsty(new Foo.Bar(){
            @Override
            public void drink(){
                System.out.println("Gulp");
            }
        });
    }
}
```

##### Delegation
From the above, what happens when `thirsty()` is executed depends on the object that is implementing the interface Foo.Bar.
> The behaviour of `thirsty()` is **delegated** to objects that implement the interface.

Design principle:
- Program to a supertype: Since input to `thirsty()` is an interface, it can accept any object that implements `Foo.bar`
- Favour composition over inheritance: `thirsty()` can accept any object that implement `Foo.Bar`, the objects of `Foo` class become more flexible and can change behaviour at runtime.

##### Design by Composition vs Design by Inheritance

**Design by Composition**
```java=
class Foo{
    interface Bar{
        void drink();
    }
    interface Baz{
        void eat();
    }
    void thirsty(Bar bar){
        bar.drink();
    }
    void hungry(Baz baz){
        baz.eat();
    }
}
```

**Design by Inheritance**
```java=
class Foo{
    void thirsty(){};
    void hungry(){};
}
class Foo2 extends Foo{
    @Override
    void thirsty(){...};
}
class Foo3 extends Foo{
    @Override
    void hungry(){...};
}

``` 
Design by Composition is more maintainable as compared to Design by Inheritance (don't need to keep changing the parent class).



