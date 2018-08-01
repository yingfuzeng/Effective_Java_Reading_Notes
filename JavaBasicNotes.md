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




































