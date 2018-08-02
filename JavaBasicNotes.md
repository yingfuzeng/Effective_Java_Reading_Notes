# Notes of Reading Java Tutorial
## Class related
In general, class declarations can include these components, in order:

1. Modifiers such as public, private, and a number of others that you will encounter later.
2. The class name, with the initial letter capitalized by convention.
3. The name of the class's parent (superclass), if any, preceded by the keyword extends. A class can only extend (subclass) one parent.
4. A comma-separated list of interfaces implemented by the class, if any, preceded by the keyword implements. A class can implement more than one interface.  The class body, surrounded by braces, {}.

```java
	public double calculateAnswer(double wingSpan, int numberOfEngines,
	                              double length, double grossTons) {
	    //do the calculation here
	}
```

**Method naming convention**: 

Although a method name can be any legal identifier, code conventions restrict method names. By convention, method names should be a verb in lowercase or a multi-word name that begins with a verb in lowercase, followed by adjectives, nouns, etc. In multi-word names, the first letter of each of the second and following words should be capitalized. Here are some examples:
*run
runFast
getBackground
getFinalData
compareTo
setX
isEmpty*

**Overloading Methods**: 

Overloaded methods are differentiated by the number and the type of the arguments passed into the method. In the code sample, `draw(String s)` and `draw(int i)` are distinct and unique methods because they require different argument types.  Note the compiler does not consider return type when differentiating methods, so you cannot declare two methods with the same signature even if they have a different return type.

**Arbitrary Number of Arguments**

You can use a construct called varargs to pass an arbitrary number of values to a method. 

```java
	public Polygon polygonFrom(Point... corners) {
	    int numberOfSides = corners.length;
	    double squareOfSide1, lengthOfSide1;
	    squareOfSide1 = (corners[1].x - corners[0].x)
		...
```

It works just like Arrays.

**Class Constructors** 

As with methods, the Java platform differentiates constructors on the basis of the number of arguments in the list and their types.  The compiler automatically provides a no-argument, default constructor for any class without constructors. This **default** constructor will call the no-argument constructor of the superclass. In this situation, the compiler will complain if the superclass doesn't have a no-argument constructor so you must verify that it does. If your class has no explicit superclass, then it has an implicit superclass of Object, which does have a no-argument constructor.

**Passing Primitive Data Type verses Reference Data Type Arguments.**

Primitive arguments, such as an int or a double, are passed into methods by value. This means that any changes to the values of the parameters exist only within the scope of the method. When the method returns, the parameters are gone and any changes to them are lost.

```java
	public static void passMethod(int p) {
	        p = 10;
	}             
        int x = 3;        
        passMethod(x);                 
        System.out.println("After invoking passMethod, x = " + x);	
```

The out put is `3`.

Reference data type parameters, such as objects, are also passed into methods by value. This means that when the method returns, the passed-in reference still references the same object as before. However, the values of the object's fields can be changed in the method, if they have the proper access level.

**Creating Objects**
The *new* operator instantiates a class by allocating memory for a new object and returning a reference to that memory. The *new* operator also invokes the object constructor.

You can also declare a reference variable on its own line. For example:

`Point originOne;`
If you declare originOne like this, its value will be undetermined until an object is actually created and assigned to it. Simply declaring a reference variable does not create an object. For that, you need to use the new operator, as described in the next section. You must assign an object to originOne before you use it in your code. Otherwise, you will get a compiler error.

**The garbage collector**:

Some object-oriented languages require that you keep track of all the objects you create and that you explicitly destroy them when they are no longer needed. Managing memory explicitly is tedious and error-prone. The Java platform allows you to create as many objects as you want (limited, of course, by what your system can handle), and you don't have to worry about destroying them. The Java runtime environment deletes objects when it determines that they are no longer being used. This process is called garbage collection.

An object is eligible for garbage collection when there are **no more references to that object**. References that are held in a variable are usually dropped when the variable goes out of scope. Or, you can explicitly drop an object reference by setting the variable to the special value null. **Remember that a program can have multiple references to the same object; all references to an object must be dropped before the object is eligible for garbage collection**.

The Java runtime environment has a garbage collector that periodically frees the memory used by objects that are no longer referenced. The garbage collector does its job automatically when it determines that the time is right.

**Returning a Class or Interface**

When a method uses a class name as its return type, the class of the type of the returned object must be either a **subclass** of, or the exact class of, the return type. It is also called *covariant
return type*.  If the return type is an **interface name**, the object returned must implement the specific interface.

**Using `this`**

1. The most common reason for using the this keyword is because a field is shadowed by a method or constructor parameter.

```java
public class Point {
    public int x = 0;
    public int y = 0;       
    //constructor
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
	}
```

2. Using `this` with a Constructor


```java 
 public class Rectangle {
    private int x, y;
    private int width, height;        
    public Rectangle() {
        this(0, 0, 1, 1);
    }
    public Rectangle(int width, int height) {
        this(0, 0, width, height);
    }
    public Rectangle(int x, int y, int width, int height) {
        this.x = x;
        this.y = y;
        this.width = width;
        this.height = height;
    }
    ...
}
```

**Access levels**

- At the top level—public, or package-private (no explicit modifier).
- At the member level—public, private, protected, or package-private (no explicit modifier).
If a class has no modifier (the default, also known as package-private), it is visible only within its own package (packages are named groups of related classes).   For members, there are two additional access modifiers: *private* and *protected*. The private modifier specifies that the member can only be accessed in its own class. The *protected* modifier specifies that the member can only be accessed within its own package (as with package-private) and, in addition, by a *subclass* of its class in another package.

![Access level modifiers](/Users/yingfuzeng/Documents/JavaBook/Effective_Java_Reading_Notes/pics/accessLevel.png)

Tips for choosing an access level:

- Use the most restrictive access level that makes sense for a particular member. **Use private    unless you have a good reason not to**.
- Avoid public fields except for constants.  Public fields tend to link you to a particular implementation and **limit your flexibility in changing your code**.

**Class variables and `static`**

When a number of objects are created from the same class blueprint, they each have their own distinct copies of instance variables. In the case of the Bicycle class, the instance variables are cadence, gear, and speed. Each Bicycle object has its own values for these variables, stored in different memory locations.  Sometimes, you want to have variables that are common to all objects. This is accomplished with the `static` modifier. Fields that have the static modifier in their declaration are called *static fields* or *class variables*.  They are associated with the class, rather than with any object.  Static fields or methods can be called without the need for creating an instance.

`ClassName.methodName(args)`

*Static Initialization Blocks*: To provide complex initialization for static fields (normal instance variables can use constructors), Java uses *Static Initialization Blocks*.  A static initialization block is a normal block of code enclosed in braces, { }, and preceded by the static keyword. Here is an example:

```
static {
    // whatever code is needed for initialization goes here
}
```

There is an alternative to static blocks — you can write a private static method.


In **Scala**, the approach is different, since there is no *static* keywords.  What you do is define a companion object (Object with the same name as the Class), and put all "static" members 
in it.  Also note, companion object and class can access each other's private members.


**Nested Classes**

A nested class is a member of its enclosing class. Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private. Static nested classes do not have access to other members of the enclosing class. As a member of the OuterClass, a nested class can be declared *private*, *public*, *protected*, or package private.

Compelling reasons for using nested classes include the following:

- **It is a way of logically grouping classes that are only used in one place**: If a class is useful to only one other class, then it is logical to embed it in that class and keep the two together. Nesting such "helper classes" makes their package more streamlined.

- **It increases encapsulation:** Consider two top-level classes, A and B, where B needs access to members of A that would otherwise be declared private. By hiding class B within class A, A's members can be declared private and B can access them. In addition, B itself can be hidden from the outside world.

- **It can lead to more readable and maintainable code:** Nesting small classes within top-level classes places the code closer to where it is used.


As with instance methods and variables, an **inner class** is associated with an instance of its enclosing class and has direct access to that object's methods and fields. Also, because an inner class is associated with an instance, it **cannot** define any static members itself.

To instantiate an inner class, you must first instantiate the outer class. Then, create the inner object within the outer object with this syntax:

`OuterClass.InnerClass innerObject = outerObject.new InnerClass();`

There are two additional types of inner classes. You can declare an inner class within the body of a method. These classes are known as **local classes**. You can also declare an inner class within the body of a method without naming the class. These classes are known as **anonymous classes**.

**Anonymous classes**:

Anonymous classes enable you to make your code more concise. They enable you to declare and instantiate a class at the same time. They are like local classes except that they do not have a name. Use them if you need to use a local class only once.

An anonymous class is** an expression**. The syntax of an anonymous class expression is like the invocation of a constructor, except that there is a class definition contained in a block of code.

Consider the instantiation of the frenchGreeting object:

```
		HelloWorld frenchGreeting = new HelloWorld() {
            String name = "tout le monde";
            public void greet() {
                greetSomeone("tout le monde");
            }
            public void greetSomeone(String someone) {
                name = someone;
                System.out.println("Salut " + name);
            }
        };
```

And another example:

```
		btn.setOnAction(new EventHandler<ActionEvent>() {
 
            @Override
            public void handle(ActionEvent event) {
                System.out.println("Hello World!");
			}
			});
```


###Lambda Expressions
Java's way of passing function as values.  The previous section, Anonymous Classes, shows you how to implement a base class without giving it a name. Although this is often more concise than a named class, for classes with only one method, even an anonymous class seems a bit excessive and cumbersome. Lambda expressions let you express instances of single-method classes more compactly.












