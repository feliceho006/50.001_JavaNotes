## Static Typing
- Java vs. Python: Java requires declaration of the variables, specifying the types of 
variables 
- The variable type stipulates: (i) the set of values that can be taken and (ii) the 
operations that can be performed on those values 
- Java is a statically-typed language
• The types of all variables are known at compile time 
• Can perform type checking statically (checking before the program even 
runs) 
• In dynamically-typed languages like Python, this type checking is deferred until execution time (while the program is running) 
• Many ideas in this course / modern programming language is to eliminate bugs from the code, and static typing is one idea

## Operations for ArrayList and LinkedList are similar 
(both implemented the List interface) 
Underlying mechanisms are different: 
- ArrayList stores elements in an array; if the capacity is exceeded, a larger new array will be created and all the elements are copied to the new array 
- LinkedList stores elements in a linked list data structure 
- Have different performance for various operations, e.g. ArrayList is more efficient to support random access through an index

## Inheritance 
•Programming constructs to allow inheriting code from one class (superclass) to another class (subclass) 
• Enables you to define a general class (superclass) and later extend it to more specialized classes (subclass) 

Superclasses and Subclasses 
- Example: GeometricObject, Circle 
- Class Circle extended from Class GeometricObject 
- Use keyword extends 
- Superclass / parent class / base class 
- Subclass / child class / derived class / extended class 
- Subclass inherits all accessible data fields and methods from the superclass, except constructors

In a subclass inherited from a superclass, you can
- Add new properties 
- Add new methods 
- Override the methods of the superclass

Superclasses and Subclasses 
- A subclass is not a subset of its superclass; often, a subclass contains more information and methods than its superclass 
- Inheritance is used to model is-a relationship (Circle is a GeometricObject) 
- Java allows only single inheritance: A Java subclass inherits only from one superclass 
(multiple inheritance can be achieved through interface)

Super 
- Superclass’s constructors are not inherited 
- Invoked explicitly or implicitly using super keyword 
- If the keyword super is not explicitly used, the superclass’s no-arg constructor is automatically invoked 

Superclass’s constructor is always invoked 
- A constructor may invoke an overloaded constructor or its superclass constructor. If neither is invoked explicitly, the compiler puts super() as the first statement in the constructor

super 
- To call a superclass constructor 
• Must use super to call the superclass constructor 
•Invoke the superclass constructor’s name causes a syntax error 
• super needs to appear first in the constructor 
• Call to constructors (this() / super()) must be the first statement in the constructor 
• Keyword super can also be used to call a superclass method (why you need this? Aren’t they inherited?)

Constructor chaining 
- Constructing an instance of a class invokes all the superclasses’ constructors along the 
inheritance chain 

![[Pasted image 20201208161946.png]]

Overriding Methods 
- An instance method can be overridden only if it is accessible. Thus a private method cannot be overridden, because it is not accessible outside its own class. If a method defined in a subclass is private in its superclass, the two methods are completely unrelated. 
- You can only override instance methods. You can hide instance attributes / static methods / static attributes (overriding vs. hiding)

![[Pasted image 20201208162027.png]]
![[Pasted image 20201208162011.png]]
![[Pasted image 20201208162033.png]]



## Casting Object 

- Casting can be used to convert an object of one class type to another within an inheritance hierarchy. In the preceding section, the statement m(new Student()); assigns the object new Student() to a parameter of the Object type. This statement is equivalent to: 

		Object o = new Student(); // Implicit casting 
		m(o)

## Down-casting 
- Casting from superclass to subclass Explicit casting must be used when casting an 
object from a superclass to a subclass. This type of casting may not always succeed. 
		
		Object y = new Circle(); 
		Circle x = (Circle)y; 
		(Declared type vs actual type) 

## The instanceof Operator 

Use the instance of operator to test whether an object is an 
instance of a class: 

		Object myObject = new Circle(); 
		... // Some lines of code 
			/** Perform casting if myObject is an instance of Circle */ 
		if (myObject instanceof Circle) { 
			System.out.println("The circle diameter is " + 
			((Circle)myObject).getDiameter()); 
			... 
			}

![[Pasted image 20201208161932.png]]

## Abstract Class 
-  Inheritance: derives new classes from existing classes 
- Superclass: more general; Subclass: more specific 
• Example: GeometricObject models common features of 
geometric objects 
- We can compute areas and perimeters for all geometric objects, it is better to define getArea() and getPerimeter() methods in the GeometricObject class 
- But these methods cannot be implemented in GeometricObject, as their implementation depends on specific type of geometric object (Circle or Rectangle) 
• Solution: Can define them as abstract methods in GeometricObject, provide concrete implementation in the concrete subclass 
- GeometricObject becomes an abstract class
- Cannot create instance of abstract class using the new operator 
- An abstract method is defined without implementation 
- Implementation provided by subclass 
- A class that contains abstract methods must be defined as an abstract class 
- Practical advantage of abstract class: generic programming

## Interface 
- Interface is a class-like programming construct that contains only constants and abstract methods 
- In many ways similar to abstract class, as we will see 
- But its intent is to specify common behavior / characteristics of objects of related classes or unrelated classes, e.g., comparable, eatable, etc 

## Comparable Interface 
- Suppose you want to design a generic method to sort the objects of the same type: circles, rectangles, students, fruits 
- We need common behavior for the objects: comparable 
- Java provide the Comparable interface for this purpose 
- Classes that implement the Comparable interface become comparable
- Implements Comparable\<E>: provides implementation for the abstract method 
public int compareTo(E o) 
- Comparable interface is a generic interface, the generic type E is replaced by a concrete type when implementing the interface 
• Classes Integer, String, Date, etc all implement Comparable, thus they are comparable
- Comparator interface can be used to: 
 •Provide addition way of ordering 
• Comparable\<E>.compareTo() defines the “natural” ordering for E 
• Comparato\<E>.compare() defines additional, alternative ordering for E 
• Enable comparison for objects which their classes do not implement comparable 

![[Pasted image 20201208161859.png]]

![[Pasted image 20201208161908.png]]

## Abstract Class vs. Interface 

- All classes share the same root, Object; but there is no single root for interfaces 
- Like a class, a variable of an interface type can reference any instance of the class that 
implements the interface 
- If a class implements an interface, this interface plays the similar role as a superclass
- If c is an instance of Class2, c is also an instance of Object, Class1, Interface1, Interface1_1, Interface1_2, Interface2_1, Interface2_2

## What is Exception

- Runtime/execution error occurs when a program is running and there is an operation that cannot be carried out 
• E.g. divide by zero 
- An exception is an object that represents such execution error 
- The program throws an exception when such execution error occurs 
- Handle the exception or the program terminates abnormally
- When there is an exception, either the method handles it itself, or let the caller handle it 
• Some code: throw new Exception(); 
• In the try block: code that is executed in the normal circumstance 
• In the catch block: code that is executed during the exception 
• Then, the statement after the catch block is executed

Exception types 

- Exceptions are objects 
- Root class for exception is Throwable 
- Error: system error, not much you can handle; e.g. VirtualMachineError occurs when system runs out of resource
- IOException: opening a nonexistent file etc. 
- RuntimeException: programming errors such as out-of-bounds array, numeric errors 
- ArithmeticException: dividing an integer by zero 
- IndexOutOfBoundsException: index to an array is out of range

Checked and unchecked exception 

- RuntimeException, Error and their subclasses are unchecked exception 
- All other are checked exception 
- Checked exception: compiler forces the programmer to explicitly check and handle them in a try-catch block, or declare in the method header to let caller handle (use throws) 
- Unchecked exception, e.g., ArithmeticException, can occur anywhere in the program

## The finally clause 

- The finally clause is always executed regardless if an exception occurs or not, and if 
the exception is caught or not 
- Use case: file closing, clean up

## Recursion 
- All recursive methods have: 
– Conditional statements such as if-else to select different cases 
– One or more base cases (the simplest case) to stop the recursion 
– Recursive call to ‘reduce’ the original problem to closer to the base cases

![[Pasted image 20201208161738.png]]

## Singleton 
- To ensure there is only one instance of an object, available to a number of other classes 
• E.g., Log file for a pool of applications 
- GoF: “Ensure a class has only one instance and provide a global point of access to it.” 
- A creational pattern: it is used to construct objects

## Observer 
- Useful when you are interested in the state of an object and want to get notified whenever there is any change 
- Subject (Publisher) maintains a list of its dependents (observers / subscribers) 
- Subject notifies them automatically of any state changes
- GoF: “Define a one-to-many dependency between objects so that when one object 
changes state, all its dependents are notified and updated automatically.” 
- A behavioral pattern: form relationships between objects during execution at runtime

![[Pasted image 20201208161754.png]]

Why Observer? 

- Reduce coupling 
- An object (Subject) needs to share its state with other objects, without knowing who 
those objects are


## Visitor 
- Useful if you need to perform operations across a diverse set of objects 
- GoF: “Allows for one or more operation to be applied to a set of objects at runtime, decoupling the operations from the object structure” 
- Provide additional functionality to a class without changing it

![[Pasted image 20201208161806.png]]

Advantage of Visitor 

- Separate out certain logic (e.g., postage calculation) from the items themselves, keeping the item classes simple 
– Item classes only need to implement Visitable 
- Add methods to classes: another concrete class implements Visitor 
– No need to change item classes 
- Enable static checking: code cannot be compiled 
without the visit method of the corresponding type


## Boolean Satisfiability (SAT) 

(x1 ∨ x2) ≡ (¬x1 ⇒ x2) ∧  (¬x2 ⇒ x1)

![[Pasted image 20201208161840.png]]

P ^ (Q ^ R) <=> (P ^ Q) v (P ^ R) 
P ^(Q ^ R) <=> (P v Q) ^ (P v R)
¬ (P ^ Q) <=> (¬P) v (¬ Q) 
¬ (P ^ Q) <=> (¬P) ^ (¬ Q)

- SAT: Decide whether there is an assignment to the variables of a Boolean formula such that the formula is true (satisfied) 
• Yes (if there exists such assignment), satisfiable 
• No (if all assignments cannot make the formula true) 

Propositional (Boolean) Formula 
- Propositional (Boolean) formula f is defined over a set of propositional variables x1, . . . , xn, using the standard propositional connectives ¬, ∧, ∨, → and parenthesis 
– The domain of propositional variables is {0, 1}: 0=False, 1=True 
– Example: f(x1, x2, x3) = ((¬x1 ∧ x2) ∨ x3) ∧ (¬x2 ∨ x3) 
- A formula f in conjunctive normal form (CNF) is a conjunction of disjunctions (clauses) of literals, where a literal is a variable or its complement
- SAT was the first known example of an “NP-complete” problem 
– Cannot be solved in polynomial time in any known way 
- No known algorithm that efficiently solves all SAT instances 
- It is generally believed that no such algorithm can exist (not proven)
- (P∨Q)∧(¬P∨R) is in conjunctive normal form: 
– set of clauses, each containing a set of literals {{P, Q}, {¬P, R}} 
– literal is just a variable, maybe negated 
- can only negate variables, and not clauses

DPLL: Classic SAT algorithm 

![[Pasted image 20201208161818.png]]

- Key idea: unit propagation on top of backtracking search 
- If a clause contains one literal, set that literal to true 
– Necessary for any satisfiable assignment, worst case exponential

